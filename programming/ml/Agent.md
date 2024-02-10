(Somewhat specific to [langchain](https://python.langchain.com/docs/modules/agents/concepts))

The core idea of an 'agent' is to use a language model as a reasoning engine to decide when/how to use predefined 'tools'. The LLM then uses output from the selected tool(s) as context for responding to user queries (RAG).

An Agent is usually powered by a combination of a language model (e.g. ChatGPT), a prompt (which can be parameterized), and an output parser.

In the langchain model, discrete objects/steps (e.g. outputs, intermediate results from previous tool calls) have known data representations, often dataclasses.

The agent, managed by an AgentExecutor, works recursively: an action is called, and if the result is not a terminal state, the result is passed to the next action call as additional context. This continues until a terminal state is returned from an action.

