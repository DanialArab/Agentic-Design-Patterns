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

## Tool Use Design Pattern

How large language models can act as agents by taking advantage of external tools for search, code execution, productivity, ad infinitum

Tool Use, in which an LLM is given functions it can request to call for gathering information, taking action, or manipulating data, is a key design pattern of AI agentic workflows. You may be familiar with LLM-based systems that can perform a web search or execute code. Indeed, some large, consumer-facing LLMs already incorporate these features. But Tool Use goes well beyond these examples. 

Early in the history of LLMs, before widespread availability of large multimodal models (LMMs)  like LLaVa, GPT-4V, and Gemini, LLMs could not process images directly, so a lot of work on Tool Use was carried out by the computer vision community. At that time, the only way for an LLM-based system to manipulate an image was by calling a function to, say, carry out object recognition or some other function on it. Since then, practices for Tool Use have exploded. GPT-4’s function calling capability, released in the middle of last year, was a significant step toward a general-purpose implementation. Since then, more and more LLMs are being developed to be similarly facile with Tool Use. 

## Planning Design Pattern

Large language models can drive powerful agents to execute complex tasks if you ask them to plan the steps before they act.

Planning is a key agentic AI design pattern in which we use a large language model (LLM) to autonomously decide on what sequence of steps to execute to accomplish a larger task. For example, if we ask an agent to do online research on a given topic, we might use an LLM to break down the objective into smaller subtasks, such as researching specific subtopics, synthesizing findings, and compiling a report. 

Many tasks can’t be done in a single step or with a single tool invocation, but an agent can decide what steps to take. For example, to simplify an example from the HuggingGPT paper (cited below), if you want an agent to consider a picture of a boy and draw a picture of a girl in the same pose, the task might be decomposed into two distinct steps: (i) detect the pose in the picture of the boy and (ii) render a picture of a girl in the detected pose. An LLM might be fine-tuned or prompted (with few-shot prompting) to specify a plan by outputting a string like "{tool: pose-detection, input: image.jpg, output: temp1 } {tool: pose-to-image, input: temp1, output: final.jpg}". 

## Multi-Agent Collaboration design pattern 

Prompting an LLM to play different roles for different parts of a complex task summons a team of AI agents that can do the job more effectively.

Multi-agent collaboration is the last of the four key AI agentic design patterns that I’ve described in recent letters. Given a complex task like writing software, a multi-agent approach would break down the task into subtasks to be executed by different roles — such as a software engineer, product manager, designer, QA (quality assurance) engineer, and so on — and have different agents accomplish different subtasks.

Dear friends,

Multi-agent collaboration is the last of the four key AI agentic design patterns that I’ve described in recent letters. Given a complex task like writing software, a multi-agent approach would break down the task into subtasks to be executed by different roles — such as a software engineer, product manager, designer, QA (quality assurance) engineer, and so on — and have different agents accomplish different subtasks.

Different agents might be built by prompting one LLM (or, if you prefer, multiple LLMs) to carry out different tasks. For example, to build a software engineer agent, we might prompt the LLM: “You are an expert in writing clear, efficient code. Write code to perform the task . . ..” 

It might seem counterintuitive that, although we are making multiple calls to the same LLM, we apply the programming abstraction of using multiple agents. I’d like to offer a few reasons:

It works! Many teams are getting good results with this method, and there’s nothing like results! Further, ablation studies (for example, in the AutoGen paper cited below) show that multiple agents give superior performance to a single agent. 
Even though some LLMs today can accept very long input contexts (for instance, Gemini 1.5 Pro accepts 1 million tokens), their ability to truly understand long, complex inputs is mixed. An agentic workflow in which the LLM is prompted to focus on one thing at a time can give better performance. By telling it when it should play software engineer, we can also specify what is important in that role’s subtask. For example, the prompt above emphasized clear, efficient code as opposed to, say, scalable and highly secure code. By decomposing the overall task into subtasks, we can optimize the subtasks better.
Perhaps most important, the multi-agent design pattern gives us, as developers, a framework for breaking down complex tasks into subtasks. When writing code to run on a single CPU, we often break our program up into different processes or threads. This is a useful abstraction that lets us decompose a task, like implementing a web browser, into subtasks that are easier to code. I find thinking through multi-agent roles to be a useful abstraction as well.

Emerging frameworks like AutoGen, Crew AI, and LangGraph, provide rich ways to build multi-agent solutions to problems. If you're interested in playing with a fun multi-agent system, also check out ChatDev, an open source implementation of a set of agents that run a virtual software company. I encourage you to check out their GitHub repo and perhaps clone the repo and run the system yourself. While it may not always produce what you want, you might be amazed at how well it does. 

Like the design pattern of Planning, I find the output quality of multi-agent collaboration hard to predict, especially when allowing agents to interact freely and providing them with multiple tools. The more mature patterns of Reflection and Tool Use are more reliable
