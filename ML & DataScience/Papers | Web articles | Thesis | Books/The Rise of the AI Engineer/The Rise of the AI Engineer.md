---
share: true
path: 'ML & DataScience/Papers | Web articles | Thesis | Books/The Rise of the AI Engineer'
attachment:
  send: true
  folder: 'ML & DataScience/Papers | Web articles | Thesis | Books/The Rise of the AI Engineer/assets'
---

# Information

**Web article link**:  https://www.latent.space/p/ai-engineer
**Date:** 30/06/2023

---
# Content

_“In numbers, there's probably going to be significantly more AI Engineers than there are ML engineers / LLM engineers. One can be quite successful in this role without ever training anything.”_ - [Andrej Karpathy](https://twitter.com/karpathy/status/1674873002314563584)

![](assets/The%20Rise%20of%20the%20AI%20Engineer.png)

There are an increasing in the Models, tools and different applications that AI can have. The author says: "I take this seriously and literally. **I think it** _**is**_ **a full time job**. I think software engineering will spawn a new subdiscipline, specializing in applications of AI and wielding the emerging stack effectively, just as “[site reliability engineer](https://www.enov8.com/blog/the-history-of-sre/)”, “[devops engineer](https://www.bunnyshell.com/blog/history-of-devops/)”, “[data engineer](https://www.freecodecamp.org/news/the-rise-of-the-data-engineer-91be18f1e603/)” and “[analytics engineer](https://www.holistics.io/blog/analytics-engineering-what-we-know/)” emerged. The emerging (and least cringe) version of this role seems to be: **AI Engineer**."

The thousands of Software Engineers working on productionizing AI APIs and OSS models, whether on company time or on nights and weekends, in corporate Slacks or indie Discords, will professionalize and converge on a title - the AI Engineer. **This will likely be the highest-demand engineering job of the decade.**

**There are 10x as many [ML Engineer jobs](https://www.indeed.com/jobs?q=%22machine+learning+engineer%22&l=&vjk=92db5c6fe7c47a89) as [AI Engineer jobs](https://www.indeed.com/jobs?q=%22ai+engineer%22&l=&vjk=9d645e42687689ae) on Indeed, but the higher growth rate of “AI” leads me to predict that this ratio will invert in 5 years.**

![center](assets/The%20Rise%20of%20the%20AI%20Engineer-1.png)


Highly effective AI Engineers do not do the equivalent work of the Andrew Ng Coursera courses, nor do they know PyTorch, nor do they know the difference between a Data Lake or Data Warehouse. **In the near future, nobody will recommend** _**starting**_ **[in AI Engineering by reading Attention is All You Need](https://news.ycombinator.com/item?id=36432772),** just like you do not start driving by reading the schematics for the Ford Model T. Sure, understanding fundamentals and history is always helpful, and does help you find ideas and efficiency/capability gains that are not yet in common consciousness. But sometimes you can just _use_ products and learn their qualities through experience.

---
## Why AI Engineers are Emerging Now

- **Foundation Models**: are “few shot learners”, exhibiting in-context learning and even zero shot transfer capabilities that generalize beyond the original intent of model trainers. In other words, the people creating the models don’t fully know what they are capable of. People who aren’t LLM researchers are able to find and exploit capabilities simply by spending more time with the models, and applying them to a domain that is undervalued by research (e.g. Jasper with copywriting).

> [!ai]+ AI
>
> Foundation models refer to pre-trained models that serve as the base or starting point for various natural language processing (NLP) tasks. These models are usually trained on large amounts of text data and learn to understand and generate human-like text. They can be fine-tuned or used as is for a wide range of applications such as text classification, sentiment analysis, language translation, question answering, and more. Foundation models provide a powerful starting point for building NLP applications by leveraging the knowledge and understanding they have acquired through their training processes.

- **AI Research as a service**: There are ~5000 LLM researchers in the world, but ~50m software engineers. Supply constraints dictate that an “in-between” class of AI Engineers will rise to meet demand.

- **GPU hoarding**: Of course [OpenAI/Microsoft was first](https://news.microsoft.com/source/features/ai/openai-azure-supercomputer/), but Stability AI kicked off the startup GPU arms race by emphasizing their 4,000 GPU cluster. Since then it has become commonplace for new startups like Inflection ($1.3b), Mistral ($113m), Reka ($58m), Poolside ($26m) and Contextual ($20m) to raise huge seed rounds in order to own their own hardware. Dan Gross and Nat Friedman even announced Andromeda, their $100m, 10 exaflop GPU cluster exclusively for startups they invest in. There will be much more capacity for AI Engineers on the other side of the API line to use models, rather than train them.

- **Fire, ready, aim.**: nstead of requiring _data scientists/ML engineers_ do a laborious data collection exercise before training a single domain specific model that is then put into production, a _product manager/software engineer_ can prompt an LLM, and build/validate a product idea, before getting specific data to finetune.

![](assets/The%20Rise%20of%20the%20AI%20Engineer-2.png)

- **Python + JavaScript**: Data/AI is traditionally extremely Python centric, however, there are at least as many JavaScript developers as Python developers, so now tools are increasingly catering to this widely expanded audience.

- **Generative AI vs Classifier ML**:  Where the existing generation of ML might have been focused on fraud risk, recommendation systems, anomaly detection, and feature stores, the AI Engineers are building writing apps, personalized learning tools, natural language spreadsheets, and Factorio-like visual programming languages.

---
##  Software 3.0

6 years ago, Andrej Karpathy wrote a very influential essay describing [Software 2.0](https://karpathy.medium.com/software-2-0-a64152b37c35) - contrasting the “classical stack” of hand-coded programming languages that precisely model logic against the new stack of “machine learned” neural networks that approximate logic, enabling software to solve a lot more problems than could humanly be modeled.

![center](assets/The%20Rise%20of%20the%20AI%20Engineer-4.png)


![center](assets/The%20Rise%20of%20the%20AI%20Engineer-3.png)


Despite what was written and assumed by the author of the article, Karpathy does not agree 100% with this diagram describing software 3.0. Here's his comment:

![center](assets/The%20Rise%20of%20the%20AI%20Engineer-5.png)

Prompt Engineering was both [overhyped](https://www.latent.space/p/why-prompt-engineering-and-generative) _and_ here to stay, but the re-emergence of Software 1.0 paradigms in Software 3.0 applications is both an area of mass opportunity/confusion, and created white space for a mess of startups:

![](assets/The%20Rise%20of%20the%20AI%20Engineer-6.png)

It’s not going to be _just_ human-written code, of course. My recent adventures with [smol-developer](https://twitter.com/swyx/status/1657892220492738560), the larger scoped [gpt-engineer](https://twitter.com/antonosika/status/1667641038104674306), and other code generation agents like [Codium AI](https://www.latent.space/p/codium-agents#details), [Codegen.ai](https://codegen.ai/) and [Morph/Rift](https://morph.so/) will increasingly be a part of the AI Engineer toolkit. As human Engineers learn to harness AI, AIs will increasingly do Engineering as well, until a distant future when we look up one day and can no longer tell the difference.

