# AI Agentic Terms Cheat Sheet

Core vocabulary for LLM agents, retrieval, and tool use.

## Core concepts

| Term | Definition |
|---|---|
| **Agent** | An LLM-driven system that plans, calls tools, observes results, and iterates toward a goal, rather than producing a single response. |
| **Agentic loop** | The repeating cycle an agent runs: perceive/observe → reason → act (tool call) → observe result → repeat until done. |
| **Tool use / function calling** | The model emits a structured call (name + arguments) to an external function; the caller executes it and returns the result to the model. |
| **Tool calling** | Same as function calling; term used interchangeably across vendor docs (OpenAI, Anthropic, Google). |
| **Orchestrator** | The component (code or another LLM call) that manages the agent loop: routes tool calls, tracks state, decides when to stop. |
| **Planner** | A model or module that decomposes a goal into a sequence of steps or sub-tasks before execution. |
| **Multi-agent system** | Multiple specialized agents coordinating on a task, either peer-to-peer or via a supervisor/orchestrator agent. |
| **Supervisor / orchestrator agent** | An agent whose job is to delegate sub-tasks to other agents and combine their outputs. |
| **Sub-agent** | An agent spawned by another agent to handle a bounded piece of work, typically with its own context. |
| **Context window** | The maximum number of tokens (input + output) a model can attend to in one call. |
| **Context engineering** | Deliberately constructing what goes into the context window (system prompt, retrieved docs, tool schemas, history) to get reliable behavior. |
| **System prompt** | The instructions set by the developer that establish the agent's role, constraints, and behavior, distinct from user turns. |
| **Grounding** | Constraining model output to verifiable external information (retrieved documents, tool results, structured data) rather than parametric memory. |
| **Hallucination** | Model output that is fluent but not supported by its training data, context, or retrieved evidence. |
| **Chain of thought (CoT)** | Intermediate reasoning steps a model generates before a final answer, used to improve multi-step reasoning accuracy. |
| **ReAct (Reason + Act)** | An agent pattern that interleaves reasoning traces with tool actions and observations in a single loop (Yao et al., 2022). |
| **Reflection / self-critique** | An agent pattern where the model reviews and critiques its own prior output, then revises it. |

## Retrieval and memory

| Term | Definition |
|---|---|
| **RAG (Retrieval-Augmented Generation)** | Retrieving relevant external documents at query time and inserting them into the prompt so the model generates answers grounded in that content. |
| **Embedding** | A dense vector representation of text (or other data) capturing semantic meaning, used for similarity search. |
| **Vector database / vector store** | A database optimized for storing embeddings and running approximate nearest-neighbor (ANN) similarity search (e.g. Pinecone, Weaviate, Milvus, pgvector). |
| **Chunking** | Splitting source documents into smaller passages before embedding, to fit context limits and improve retrieval precision. |
| **Semantic search** | Retrieval based on embedding similarity rather than exact keyword match. |
| **Hybrid search** | Combining semantic (vector) search with traditional keyword search (e.g. BM25) to improve recall and precision. |
| **Reranking** | A second-pass model that reorders initially retrieved candidates by relevance before they're passed to the generator. |
| **Top-k retrieval** | Returning the k highest-scoring documents/chunks for a query. |
| **Agentic RAG** | RAG where the agent decides when and what to retrieve, can issue multiple retrieval calls, and can reformulate queries, rather than a single fixed retrieval step. |
| **GraphRAG** | RAG variant that retrieves from a knowledge graph instead of (or alongside) a vector store, useful for multi-hop or relational queries. |
| **Short-term memory** | Information held within the current context window / session (conversation history, scratchpad state). |
| **Long-term memory** | Information persisted across sessions, typically stored externally (vector store, database, or file) and retrieved as needed. |
| **Knowledge base** | The corpus of documents an agent or RAG system retrieves from. |

## Tool use and integration

| Term | Definition |
|---|---|
| **MCP (Model Context Protocol)** | An open protocol (Anthropic, 2024) standardizing how LLM applications connect to external tools, data sources, and context providers. |
| **Tool schema** | The structured definition (name, description, parameters as JSON Schema) that tells a model what a tool does and how to call it. |
| **Function calling** | See Tool use / function calling above. |
| **Code execution / code interpreter** | A tool that lets the model write and run code (commonly Python) in a sandbox to compute results or manipulate data. |
| **Sandbox** | An isolated execution environment for running agent-generated code or commands without affecting the host system. |
| **Structured output** | Model output constrained to a defined schema (JSON, XML, etc.), often enforced via grammar constraints or schema validation. |
| **Guardrails** | Programmatic checks (input validation, output filtering, policy enforcement) wrapped around an agent to constrain its behavior. |
| **Human-in-the-loop (HITL)** | A workflow pattern requiring human approval or intervention at defined checkpoints before an agent proceeds. |

## Evaluation and reliability

| Term | Definition |
|---|---|
| **Eval / evaluation harness** | A test suite that scores model or agent outputs against expected results, rubrics, or reference answers. |
| **LLM-as-judge** | Using an LLM to score or compare outputs of another (or the same) LLM, typically against a rubric. |
| **Faithfulness** | In RAG, whether the generated answer is actually supported by the retrieved context (vs. hallucinated). |
| **Groundedness** | Synonym for faithfulness; how well output is anchored to provided evidence. |
| **Task success rate** | The fraction of agent runs that achieve the defined goal, used as a primary agent benchmark metric. |
| **Latency budget** | The maximum acceptable end-to-end response time for an agent task, constraining how many tool calls / loop iterations are feasible. |
| **Token budget** | The maximum tokens (cost/context) allotted to a single agent run or step. |

## Related architectures

| Term | Definition |
|---|---|
| **Prompt chaining** | Breaking a task into a fixed sequence of LLM calls, each feeding the next, without dynamic branching. |
| **Router / routing** | A step (model-based or rule-based) that directs a request to one of several specialized prompts, models, or agents. |
| **Parallelization pattern** | Running multiple LLM calls concurrently (e.g. sectioning a task, or voting across samples) and aggregating results. |
| **Evaluator-optimizer pattern** | One LLM call generates a candidate, another evaluates it against criteria, looping until the evaluator accepts it. |
| **Fine-tuning** | Further training a pretrained model on task-specific data to adjust its weights, as distinct from prompting or RAG. |
| **In-context learning** | The model adapting its behavior from examples or instructions given in the prompt, without weight updates. |
| **Few-shot prompting** | Providing a small number of example input/output pairs in the prompt to steer model behavior. |
