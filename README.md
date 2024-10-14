# Agentic-Design-Patterns

https://www.deeplearning.ai/the-batch/how-agents-can-improve-llm-performance/?ref=dl-staging-website.ghost.io

The four design patterns for AI agentic workflow:

- Reflection: The LLM examines its own work to come up with ways to improve it. 
- Tool Use: The LLM is given tools such as web search, code execution, or any other function to help it gather information, take action, or process data.
- Planning: The LLM comes up with, and executes, a multistep plan to achieve a goal (for example, writing an outline for an essay, then doing online research, then writing a draft, and so on).
- Multi-agent collaboration: More than one AI agent work together, splitting up tasks and discussing and debating ideas, to come up with better solutions than a single agent would.

## Reflection Design Pattern

You may have had the experience of prompting ChatGPT/Claude/Gemini, receiving unsatisfactory output, delivering critical feedback to help the LLM improve its response, and then getting a better response. What if you automate the step of delivering critical feedback, so the model automatically criticizes its own output and improves its response? This is the crux of Reflection. 

And we can go beyond self-reflection by giving the LLM tools that help evaluate its output; for example, running its code through a few unit tests to check whether it generates correct results on test cases or searching the web to double-check text output. Then it can reflect on any errors it found and come up with ideas for improvement.

Further, we can implement Reflection using a multi-agent framework. I've found it convenient to create two different agents, one prompted to generate good outputs and the other prompted to give constructive criticism of the first agent's output. The resulting discussion between the two agents leads to improved responses.

Reflection is a relatively basic type of agentic workflow, but I've been delighted by how much it improved my applications’ results in a few cases. I hope you will try it in your own work. If you’re interested in learning more about reflection, I recommend these papers:

- “Self-Refine: Iterative Refinement with Self-Feedback,” Madaan et al. (2023)

- “Reflexion: Language Agents with Verbal Reinforcement Learning,” Shinn et al. (2023)

- “CRITIC: Large Language Models Can Self-Correct with Tool-Interactive Critiquing,” Gou et al. (2024)
