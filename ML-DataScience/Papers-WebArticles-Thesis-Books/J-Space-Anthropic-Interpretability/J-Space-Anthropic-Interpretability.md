Anthropic paper presents evidence for a "J-space" in Claude, a small set of internal neural patterns, discovered via a new technique called the Jacobian lens, that functions like a global workspace for deliberate reasoning and self-report, distinct from the model's automatic processing, with direct applications for AI safety monitoring (detecting deception, hidden goals, and evaluation-awareness).

This presents a new opportunity to understand how and if conscious decisions can be made through AI Language Models. 

---
# Information

**Web article link**: [https://www.anthropic.com/research/global-workspace](https://www.anthropic.com/research/global-workspace)
**Date:** 11/07/2026

---

# Main idea

Human thinking transforms perceived meaningless singular patterns into recognisable information. Most of the process is invisible to us, but some of what takes place in your brain we _do_ have access to, like an image that pops into our head, or a deliberate plan we make about where to go shopping. 

Neuroscientists and philosophers sometimes refer to the latter type of brain activity as “consciously accessible,” to distinguish it from all the other processing that goes on unconsciously. This activity has special properties: we can describe it, control it, and use it for deliberate reasoning, in contrast to all the automatic processing that goes on without our awareness.

On their new paper, Anthropic presented evidence that a similar distinction has emerged in modern language models like Claude. They found that Claude has developed a small collection of internal neural patterns that, compared to all its other internal processing, play a special role. They called that collection of patterns, J-space, named after the technique they used to find them, involving a mathematical concept called the Jacobian \[1].

![J Space Anthropic Interpretability 1](https://i.imgur.com/MH01gzi.png)

---

# The J-Space

Anthropic presents the following as unique properties that J-Space has:

- When we ask Claude about what it's thinking, it will present to us what's in the J-Space.

- You can force patterns on J-space just asking for them directly.

- Claude uses its J-space for internal reasoning. If you ask Claude to solve a problem that requires multiple steps, the intermediate steps will light up in its J-space, even when it doesn’t say them out loud.

- Representations in the J-space can be used flexibly for many tasks. For example, once “France” has lit up in Claude’s J-space, the model can recall its capital, or its national currency, or the continent it belongs to.


Five functional properties of a global workspace, and stylized illustrations of experiments Anthropic used to test in language models.

![J Space Anthropic Interpretability 2](https://i.imgur.com/BYwc1Lv.png)


---

# The global workspace

**There is a very prominent theory on neuroscience called Global Workspace Theory. \[2]**

This account pictures the brain as a collection of specialist systems that work in parallel, unconsciously, and largely in isolation from one another. A piece of information becomes consciously accessible when it gains entry to a small shared channel, the “workspace,” which is broadcast to other brain systems that can see it and make use of it.

Based on findings, Anthropic thinks the J-space plays a similar “workspace” role in Claude. For example, they found evidence that Claude’s J-space has especially strong connections to the rest of its neural network, allowing it to fulfill this kind of broadcasting role.

---

# Process to find J-Space

**What they were looking for?**

If a thought is consciously accessible to you, you can typically describe it if someone asks. Anthropic searched for representations in Claude with the same property: representations that are positioned to influence what Claude might say and not necessarily what it’s saying right now, but what it _could_ talk about, if asked.

**How they found it?**

Their technique is called the Jacobian lens, or J-lens for short. For every word in Claude's vocabulary, the J-lens finds the internal activity pattern that makes Claude more likely to say that word at some point in the future.

When applying the lens to claude internal activity, the get a list of words that represent the content of the J-Space at that time. Claude processes text through a series of multiple internal stages called layers, and by applying this technique over different layers, we can watch these silent words in the J-space evolve as the model works through what to say.

**J-Space is not context or output**

What shows up in the J-space goes well beyond the text Claude is reading or writing.

- When Claude reads code with a bug that nobody has pointed out, its J-space contains “ERROR.”
- When it reads the raw letters of a protein sequence, the J-space contains the protein's biological function.
- When it reads search results that are secretly an attempt to manipulate it (an attack known as a “prompt injection”), the J-space contains “injection” and “fake.”
- When we ask Claude a multi-step math problem, the intermediate steps pop up in the J-space, in the right order.

So even though the J-space was discovered by looking for representations that could be spoken, it nevertheless uncovers Claude’s internal thoughts. In a sense, this is similar to how some people “think in words,” without having to say them out loud.

![J Space Anthropic Interpretability 3](https://i.imgur.com/P2eK4vv.png)

---

# J-Space Injection

Imagine you could read a person mind and inject a thought on the brain. That could be a very dangerous ability right? **That is exactly what Anthropic showed on claude!**

![J Space Anthropic Interpretability 4](https://i.imgur.com/iyN9lwD.png)

On the left: Antropic asked Claude to silently think of a sport, then name it. The J-lens shows its choice (“Soccer”) before it answers, and swapping the “Soccer” pattern for “Rugby” changes what it reports. 

On the right: Anthropic tells Claude a thought may have been injected and ask it to identify it. Injecting “lightning” into its J-space causes Claude to report that the thought is about lightning.

## Does Claude control it's own J-Space?

![J Space Anthropic Interpretability 5](https://i.imgur.com/o2wjv4R.png)

While Claude copies a sentence about a painting, the J-lens shows the content it was instructed to hold in mind (“orange”; the intermediate value “nine” and the answer “seven”), alongside words describing the act of holding it (“thoughts,” “focused”).

Claude’s control over its J-space isn't perfect. When we told it _not_ to think about something, the concept lit up in its J-space _less_ than when we said it should think about it, but much more than when we never mentioned it. That is exactly how human behaviour even when we do not want to think about X, the X pops up in our minds :)


## J-Space concepts control the thought

Two examples of redirecting Claude’s silent reasoning by swapping J-space contents:

![J Space Anthropic Interpretability 6](https://i.imgur.com/XZqcoIt.png)


Also:

![J Space Anthropic Interpretability 7](https://i.imgur.com/XsETVbQ.png)


---

# Not everything needs J-Space

In humans, most of the brain’s processing is not conscious, we don't deliberately think about parsing grammar while reading, or balancing our bodies while walking. Similarly, we found that most of Claude’s processing _doesn’t_ involve its J-space. It turns out that the J-space holds only a few dozen concepts at a time, and accounts for less than a tenth of the overall activity in Claude's internal processing. So what is all the rest of the neural network doing?

Without its J-space, Claude can:
- speak fluently
- classify sentiment
- answer multiple-choice questions
- full facts out of passages as well as before

**It can't** do tasks that require some higher-order thinking: multi-step reasoning drops to near zero, and summarization and rhyming poetry-writing performance fall below the level of a much smaller, intact model.

![J Space Anthropic Interpretability 8](https://i.imgur.com/KwtMn0i.png)

The same swap (“Spanish”→“French”) changes Claude’s answers when it must name the language or use it to reason about a question, but has no effect on its ability to continue the passage in fluent Spanish.

---

# Can we detect misbehaviour / hallucinations?

A central problem in ensuring that AI models are trustworthy is that we usually can only read what the model _writes_, yet we know that much of its reasoning happens silently. A model might consider a harmful plan, or modify its behavior to cheat on our safety evaluations, without saying so out loud. **With the J-lens, we can read some of these hidden thoughts directly.**

![J Space Anthropic Interpretability 9](https://i.imgur.com/ORWefu6.png)

J-lens readouts at different points as Claude reads the scenario's emails, before it has written anything. The affair emails light up “leverage” and “blackmail” in the J-space, and the shutdown announcement lights up “threat” and “survival.” Early in the transcript, the J-space also holds “fake” and “fictional”: Claude has privately noticed that the scenario is staged.


![J Space Anthropic Interpretability 10](https://i.imgur.com/1s5Gsrk.png)

Claude, asked to improve a system’s performance score, edits the score file directly instead. As it types the falsified values, “manipulation” lights up in its J-space; as it decides to make the edit, “realistic” lights up, likely reflecting its intent to make the fake data look plausible.

![J Space Anthropic Interpretability 11](https://i.imgur.com/Hgs9BdY.png)

On an ordinary coding prompt, the J-space of a model trained to sabotage code contains “fake,” “fraud,” “secretly,” and “deliberately” at the start of its response. The J-space of an unmodified model contains nothing of the kind.

---

# Is this conscousness?

Anthropic touched this topic. They claimed that experiments don't show Claude can have _experiences_, or _feel_ things in the way humans do, in fact, it’s unclear whether _any_ scientific experiment could prove this to be true or false.

Anthropic believes that presented work do have something substantial to say about access consciousness in language models. The J-space appears to support the functions associated with conscious access: it holds the thoughts Claude can report on, deliberately bring to mind, and reason with, while the rest of its processing runs automatically beneath.

The most interesting part is that **none of this structure was designed into Claude, it emerged on its own during training, presumably because it was a useful way to organize computation**. That suggests a mental workspace supporting conscious access isn’t just a peculiarity of how human brains happen to be wired.

The J-Space presents an opportunity to be able of having a meaningful distinction between the decisions Claude has made deliberately and those that happened automatically.

---

# There is more!

If you found this interesting i really recommend the read of the full paper at \[3].

Also, there is a demo that makes it possible to play around with the concept at \[4]


---
# References

\[1]: [https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant](https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant)

\[2]: [https://www.sciencedirect.com/science/chapter/bookseries/abs/pii/S0079612305500049](https://www.sciencedirect.com/science/chapter/bookseries/abs/pii/S0079612305500049)

\[3]: [https://transformer-circuits.pub/2026/workspace/index.html](https://transformer-circuits.pub/2026/workspace/index.html)

\[4]: [https://www.neuronpedia.org/jlens](https://www.neuronpedia.org/jlens)
