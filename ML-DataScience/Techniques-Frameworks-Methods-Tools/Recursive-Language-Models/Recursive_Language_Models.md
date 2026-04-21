# Why is “long-context” research so unsatisfactory?

"Context rot" is (as defined by anthropic \[1]):

> \[when] the number of tokens in the context window increases, the model’s ability to accurately recall information from that context decreases

But people have noticed that context rot is this weird thing that happens when your Claude Code history gets bloated, or you chat with ChatGPT for a long time - it’s almost like, as the conversation goes on, the model gets…dumber?

The natural solution is something along the lines of, “well maybe if I split the context into two model calls, then combine them in a third model call, I’d avoid this degradation issue”. <ins>Authors have taken this intuition as the basis for a recursive language model.</ins>

---
# **Recursive Language Models (RLMs)**

A recursive language model is a thin wrapper around a LM that can spawn (recursive) LM calls for intermediate computation - from the perspective of the user or programmer, it is the same as a model call.

In other words, you query a RLM as an “API” like you would a LM, i.e. `rlm.completion(messages)` is a direct replacement for `gpt5.completion(messages)`. RLM takes a **context-centric view** rather than a **problem-centric view** of input decomposition. This framing retains the functional view that we want a system that can answer a particular **query** over some associated **context**.

 A recursive language model call replaces a language model call. <ins>It provides the user the illusion of near infinite context</ins>, while under the hood a language model manages, partitions, and recursively calls itself or another LM over the context accordingly to avoid context rot.

![Recursive Language Models 1](https://i.imgur.com/VWmDzZi.png)

Under the hood, a RLM provides only the **query** to the LM (which we call the **root LM**, or LM with depth=0), and allows this LM to interact with an **environment**, which stores the (potentially huge) **context**.

We choose the **environment** to be a loop where the LM can write to and read the output of cells of a Python REPL Notebook (similar to a Jupyter Notebook environment) that is pre-loaded with the **context** as a variable in memory. The **root LM** has the ability to call a recursive LM (or LM with depth=1) inside the REPL **environment** as if it were a function in code, allowing it to naturally peek at, partition, grep through, and launch recursive sub-queries over the **context**.

Our instantiation of the RLM framework provides the root LM the ability to analyze the context in a Python notebook environment, and launch recursive LM calls (depth=1) over any string stored in a variable. The LM interacts by outputting code blocks, and it receives a (truncated) version of the output in its context. When it is done, it outputs a final answer with `FINAL(…)` tags or it can choose to use a string in the code execution environment with `FINAL_VAR(…)`.

When the **root LM** is confident it has an answer, it can either directly output the answer as `FINAL(answer)`, or it can build up an answer using the variables in its REPL environment, and return the string inside that answer as `FINAL_VAR(final_ans_var)`.

![Recursive Language Models 3](https://i.imgur.com/K9VJHZq.png)

This setup yields several benefits that are visible in practice:
1. The context window of the root LM is rarely clogged — because it never directly sees the entire context, its input context grows slowly.
2. The root LM has the flexibility to view subsets of the context, or naively recurse over chunks of it. For example, if the query is to find a needle-in-the-haystack fact or multi-hop fact, the root LM can use `regex` queries to roughly narrow the context, then launch recursive LM calls over this context. This is particularly useful for arbitrary long context inputs, where indexing a retriever is expensive on the fly!
3. The context can, in theory, be any modality that can be loaded into memory. The root LM has full control to view and transform this data, as well as ask sub-queries to a recursive LM.

---

# What is happening under the hood?

Based on \[2]:

## Step 1: Context lives in the environment

```py
# Instead of:  
response = llm("Here's 10M tokens... answer this")
```

```py
# RLM does:  
context = "..." # 10M tokens stored as variable  
# Model never sees this directly in its prompt!
```

## Step 2: Model explores programmatically

```py
# The RLM can do things like:  
print(context[:1000]) # Peek at first 1000 chars  
print(len(context)) # Check total length
```

```py
# Search with regex  
import re  
matches = re.findall(r'festival.*celebration', context)# Filter smartly  
relevant = [  
    line for line in context.split('\n')   
    if 'magic number' in line.lower()  
]
```

## Step 3: Spawn recursive sub-models

```py
# When it finds something interesting:  
chunk = context[50000:100000]  
answer = llm_query(f"Extract dates: {chunk}")
```

```py
# Batch process:  
results = []  
for i in range(0, len(context), 100000):  
    chunk = context[i:i+100000]  
    result = llm_query(f"Find patterns: {chunk}")  
    results.append(result)final = llm_query(f"Synthesize: {results}")
```

## Step 4: Return the answer

```py
FINAL(synthesized_answer)
```

---
# Real world example

Let’s trace through a real example from the original paper \[3]. 
**Task:** Answer using 1,000 documents (≈8.3M tokens):

> “This vegetable stew uses fish… What are the first and last names of the person who won the beauty pageant at the thirteenth anniversary of this festival?”

## What GPT-5 Does (Naive):

- Can't fit 8.3M tokens  
- Even chunked, loses connections  
- Score: 0% (literally cannot attempt)

## What RLM(GPT-5) Does:

**Turn 1:** Probe the corpus

```py
# Search for keywords  
festival_docs = []  
for i, doc in enumerate(documents):  
    if re.search(r'festival|celebration', doc, re.I):  
        festival_docs.append((i, doc))print(f"Found {len(festival_docs)} docs")  
print(documents[6][:500])  # Looks promising!
```

**Turn 2:** Deep dive with recursive call

```py
doc = documents[6]  
analysis = llm_query(f"""  
Find info about:  
- Festival name and location  
- Beauty pageant winners  
- Dates  
Context: {doc}  
""")  
# Returns: "Maria Dalmacio won..."
```

**Turn 3:** Verify and return

```py
verify = llm_query(f"Confirm Maria Dalmacio: {analysis}")  
FINAL("Maria Dalmacio")
```

---

# How RLMs Think: Emergent Behaviors

Without special training, RLMs develop smart strategies:

## 1. Smart Filtering

```py
# Uses model priors:  
matches = re.findall(r'La Union|festival', context)  
# Narrows 1M+ lines to ~100 relevant ones
```

## 2. Intelligent Chunking

```py
# Semantic batching:  
for batch in chunks(lines, size=100):  
	label = llm_query(f"Classify: {batch}")
```

## 3. Answer Verification

```py
# Fresh sub-LLMs avoid context rot:  
answer = llm_query("What's the answer?")  
verify = llm_query(f"Is '{answer}' correct?")
```

## 4. Long Output Generation

```py
# Bypasses output limits:  
parts = []  
for section in data:  
	part = llm_query(f"Process {section}")  
	parts.append(part)

FINAL_VAR(parts)  # Returns variable!
```


---

# Everything has limitations!

## 1. Inefficient Decomposition

**Qwen3-Coder**: Thousands of sub-calls for simple tasks  
**GPT-5**: Sometimes too conservative

Example: Qwen made a separate call **per line** (1000+ calls) when 10–20 batches would suffice.

## 2. Answer Verification Loops

Iteration 1: Correct answer  
Iteration 2: Verify (correct)  
Iteration 3: Verify again  
...  
Iteration 6: Returns wrong answer

## 3. Synchronous Execution

All sub-calls blocking/sequential. With async: 10–100x faster possible.

## 4. REPL Brittleness

Must wrap answers in `FINAL()` tags. Sometimes forgets or wraps intermediate thoughts.

---

# Practical experimentation

After everything i presented above, i had to try and experiment with this new (potential) new paradigm in LLMs. There is an official repo for this at \[4] This is what i experimented:

- **My goal:** Summarize content of a specific page present in a long PDF.
- **Why:** Long context are a challenge to LLMs. Achieving strong performance generally requires implementing a retrieval-augmented generation (RAG) system that retrieves only the sections of lengthy documents pertinent to the task.


**Selected PDF for the experiment:** On The Origin Of Species by Charles Darwin \[5].

```python
rlm = RLM(

    backend="openai",  # or "portkey", etc.

    backend_kwargs={
        "model_name": "gpt-5-mini",
        "api_key": os.getenv("OPENAI_API_KEY"),
        "base_url": "https://openrouter.ai/api/v1",
    },

    environment="local",

    environment_kwargs={
        "setup_code": f"import shutil; shutil.copy(r'{PDF_PATH}', 'On-the-Origin-of-Species.pdf')",
    },

    max_depth=1,
    logger=logger,
    verbose=True,  # For printing to console with rich, disabled by default.
)
```



## Question

The selected question was:

> In your workspace there is a PDF file called 'On-the-Origin-of-Species.pdf'. Open it using PyPDF2 and summarize the content on page 52.


**Why?**
- Tradicional LLMs can't do this. LLM's have no logic on pagination unless you pass all text together with pagination.
- Partial selection of content without looking at the whole document
- It enables the us to see the points where this approach is really good (execute code in a sandbox environment to find what it needs)


## Steps executed


- First it checks the request


```
╭─ ▸ Code Execution  (0.000s) ────────────────────────────────────────────────────────────────────────────────────╮
│ Code:                                                                                                           │
│ # Inspect the provided context variable                                                                         │
│ print("Context length:", len(context))                                                                          │
│ print("Context content:")                                                                                       │
│ print(context)                                                                                                  │
│                                                                                                                 │
│ Output:                                                                                                         │
│ Context length: 135                                                                                             │
│ Context content:                                                                                                │
│ In your workspace there is a PDF file called 'On-the-Origin-of-Species.pdf'. Open it using PyPDF2 and summarize │
│ the content on page 52.                                                                                         │
│                                                                                                                 │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```


- Open on the requested page


```
╭─ ▸ Code Execution  (0.056s) ────────────────────────────────────────────────────────────────────────────────────╮
│ Code:                                                                                                           │
│ # Attempt to find and read 'On-the-Origin-of-Species.pdf' and extract text from page 52.                        │
│ import os                                                                                                       │
│                                                                                                                 │
│ pdf_filename = 'On-the-Origin-of-Species.pdf'                                                                   │
│ print("Working directory contents:", os.listdir('.'))                                                           │
│                                                                                                                 │
│ if not os.path.isfile(pdf_filename):                                                                            │
│     print(f"File '{pdf_filename}' not found in the current directory.")                                         │
│ else:                                                                                                           │
│     print(f"Found '{pdf_filename}'. Attempting to extract page 52 text...")                                     │
│                                                                                                                 │
│     page_text = None                                                                                            │
│     # Try PyPDF2 first, then pypdf as fallback                                                                  │
│     try:                                                                                                        │
│         import PyPDF2                                                                                           │
│         print("Using PyPDF2 to read PDF...")                                                                    │
│         with open(pdf_filename, 'rb') as f:                                                                     │
│             reader = PyPDF2.PdfReader(f)                                                                        │
│             num_pages = len(reader.pages)                                                                       │
│             print("Number of pages in PDF:", num_pages)                                                         │
│             page_index = 51  # page 52 -> zero-based index 51                                                   │
│             if page_index < num_pages:                                                                          │
│                 page = reader.pages[page_index]                                                                 │
│                 # PyPDF2 has .extract_text()                                                                    │
│                 try:                                                                                            │
│                     page_text = page.extract_text()                                                             │
│                 except Exception as e:                                                                          │
│                     print("PyPDF2 extract_text failed:", e)                                                     │
│     except Exception as e:                                                                                      │
│         print("PyPDF2 not available or failed to import:", e)                                                   │
│                                                                                                                 │
│     if page_text is None:                                                                                       │
│         try:                                                                                                    │
│             import pypdf                                                                                        │
│             print("Using pypdf to read PDF...")                                                                 │
│             with open(pdf_filename, 'rb') as f:                                                                 │
│                 reader = pypdf.PdfReader(f)                                                                     │
│                 num_pages = len(reader.pages)                                                                   │
│                 print("Number of pages in PDF:", num_pages)                                                     │
│                 page_index = 51                                                                                 │
│                 if page_index < num_pages:                                                                      │
│                     page = reader.pages[page_index]                                                             │
│                     try:                                                                                        │
│                         page_text = page.extract_text()                                                         │
│                     except Exception as e:                                                                      │
│                         print("pypdf extract_text failed:", e)                                                  │
│         except Exception as e:                                                                                  │
│             print("pypdf not available or failed to import:", e)                                                │
│                                                                                                                 │
│     if page_text is None:                                                                                       │
│         try:                                                                                                    │
│             # Try using PyMuPDF (fitz) if available                                                             │
│             import fitz                                                                                         │
│             print("Using PyMuPDF (fitz) to read PDF...")                                                        │
│             doc = fitz.open(pdf_filename)                                                                       │
│             num_pages = doc.page_count                                                                          │
│             print("Number of pages in PDF:", num_pages)                                                         │
│             page_index = 51                                                                                     │
│             if page_index < num_pages:                                                                          │
│                 page = doc.load_page(page_index)                                                                │
│                 page_text = page.get_text("text")                                                               │
│         except Exception as e:                                                                                  │
│             print("PyMuPDF (fitz) not available or failed to import:", e)                                       │
│                                                                                                                 │
│     if page_text is None:                                                                                       │
│         print("Unable to extract page text with available PDF libraries.")                                      │
│     else:                                                                                                       │
│         # Save the extracted text to a variable for later use                                                   │
│         extracted_page_text = page_text                                                                         │
│         print("Extracted text (first 1000 chars):")                                                             │
│         print(extracted_page_text[:1000])                                                                       │
│                                                                                                                 │
│ Output:                                                                                                         │
│ Working directory contents: ['On-the-Origin-of-Species.pdf', 'context_0.txt']                                   │
│ Found 'On-the-Origin-of-Species.pdf'. Attempting to extract page 52 text...                                     │
│ Using PyPDF2 to read PDF...                                                                                     │
│ Number of pages in PDF: 377                                                                                     │
│ Extracted text (first 1000 chars):                                                                              │
│ 3.      STRUGGLE        FOR     EXISTENCE.                                                                      │
│ Bears   on      natural selection.      The     term    used    in      a       wide    sense.                  │
│ Geometrical     powers  of      increase.       Rapid   increase        of      naturalised                     │
│ animals and     plants. Nature  of      the     checks  to      increase.                                       │
│ Competition     universal.      Effects of      climate.        Protection      from    the                     │
│ number  of      individuals.    Complex relations       of      all     animals and                             │
│ plants  throughout      nature. Struggle        for     life    most    severe  between                         │
│ individuals     and     varieties       of      the     same    species;        often   severe                  │
│ between species of      the     same    genus.  The     relation        of      organism        to              │
│ organism        the     most    important       of      all     relations.                                      │
│ Before  entering        on      the     subject of      this    chapter,        I       must    make    a       │
│ few     preliminary                                                                                             │
│ remarks,        to      show    how     the     struggle        for     existence       bears   on      Natural │
│ Selection.      It                                                                                              │
│ has     been    seen    in      the     last    chapter that    amongst organic beings  in      a       state   │
│ of      nature                                                                                                  │
│ there   is      some    individual      variability;    indeed  I       am      not     aware   that    this    │
│ has     ever    been                                                                                            │
│ disputed.       It      is      immaterial      for     us      whether a       multitude       of              │
│ doubtful        forms   be      called                                                                          │
│ species or      sub-species     or      varieties;                                                              │
│                                                                                                                 │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```


- Request to summarize and return the result


```
╭─ ▸ Code Execution  (7.373s) ────────────────────────────────────────────────────────────────────────────────────╮
│ Code:                                                                                                           │
│ # Use the available llm_query to produce a concise summary of the extracted page text.                          │
│ prompt = (                                                                                                      │
│     "You are given the OCR/extracted text of page 52 from Charles Darwin's "                                    │
│     "\"On the Origin of Species\" (shown below). Provide a concise summary (3-6 sentences) "                    │
│     "highlighting the main topics, arguments, and their significance for Darwin's theory. "                     │
│     "Do not add any information not present on the page; focus only on the content provided.\n\n"               │
│     "Page text:\n\n" + extracted_page_text                                                                      │
│ )                                                                                                               │
│                                                                                                                 │
│ page52_summary = llm_query(prompt)                                                                              │
│ print("Summary produced:\n")                                                                                    │
│ print(page52_summary)                                                                                           │
│                                                                                                                 │
│ Output:                                                                                                         │
│ Summary produced:                                                                                               │
│                                                                                                                 │
│ Darwin introduces the "struggle for existence" as key to understanding natural selection, after noting that     │
│ individual variability and some well-marked varieties unquestionably exist. He argues that mere variability,    │
│ while necessary, cannot by itself explain how the many exquisite adaptations and co-adaptations of organs,      │
│ organisms, and conditions of life have been perfected, citing examples like the woodpecker, mistletoe,          │
│ parasites, diving beetles, and plumed seeds. He also downplays the importance of rigidly ranking doubtful forms │
│ as species or varieties for the present argument. Finally, he poses the central question of how incipient       │
│ varieties are ultimately converted into distinct species that differ far more from one another than do ordinary │
│ varieties.                                                                                                      │
│                                                                                                                 │
│                                                                                                                 │
│ ↳ 1 sub-call(s)                                                                                                 │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```


- Final answer!


```
╭─ ★ Final Answer ────────────────────────────────────────────────────────────────────────────────────────────────╮
│                                                                                                                 │
│  Darwin introduces the "struggle for existence" as key to understanding natural selection, after noting that    │
│  individual variability and some well-marked varieties unquestionably exist. He argues that mere variability,   │
│  while necessary, cannot by itself explain how the many exquisite adaptations and co-adaptations of organs,     │
│  organisms, and conditions of life have been perfected, citing examples like the woodpecker, mistletoe,         │
│  parasites, diving beetles, and plumed seeds. He also downplays the importance of rigidly ranking doubtful      │
│  forms as species or varieties for the present argument. Finally, he poses the central question of how          │
│  incipient varieties are ultimately converted into distinct species that differ far more from one another than  │
│  do ordinary varieties.                                                                                         │
│                                                                                                                 │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```


---

# Conclusions

This is a very interesting approach that has real world potential for some use cases.

Recursive Language Models represent a compelling shift in how we approach long-context tasks, **not by expanding what a model can hold in memory, but by giving it the tools to navigate large contexts intelligently**. The practical experiment above demonstrates this clearly: rather than attempting to ingest an entire book, the RLM located, extracted, and summarized a specific page with precision, using only a handful of targeted operations.

This paradigm is not a replacement for RAG but more close to an agent with programmatic access to its own retrieval process. The tradeoffs are real: cost, latency, and decomposition quality all depend heavily on the underlying model's reasoning ability. But for tasks where context structure is unknown at indexing time, or where on-the-fly exploration is required, RLMs offer a genuinely novel and practical alternative.

**As models become more capable coders and the cost per token continues to fall, the inefficiencies that currently limit RLMs will shrink, making this a paradigm worth watching closely.**

---

# References

\[1]: [https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)

\[2]: [https://medium.com/@ahmealy/recursive-language-models-how-mit-researchers-cracked-the-context-window-problem-2936d7ea0b88](https://medium.com/@ahmealy/recursive-language-models-how-mit-researchers-cracked-the-context-window-problem-2936d7ea0b88)

\[3]: [https://arxiv.org/pdf/2512.24601](https://arxiv.org/pdf/2512.24601)

\[4]: [https://github.com/alexzhang13/rlm?tab=readme-ov-file](https://github.com/alexzhang13/rlm?tab=readme-ov-file)

\[5]: [https://www.vliz.be/docs/Zeecijfers/Origin_of_Species.pdf](https://www.vliz.be/docs/Zeecijfers/Origin_of_Species.pdf)
