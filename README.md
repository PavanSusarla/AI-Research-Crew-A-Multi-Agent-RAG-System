# AI-Research-Crew-A-Multi-Agent-RAG-System
This project demonstrates a multi-agent system that performs retrieval-augmented generation (RAG) using CrewAI and LangChain, orchestrating multiple specialized AI agents to research, synthesize, and refine high-quality answers autonomously.

It simulates a collaborative “research team” of AI agents that plan, retrieve, analyze, and review information sequentially.

⚙️ Core Components
Component	Description
CrewAI	A multi-agent coordination framework used to define agents, their roles, tasks, memory, and execution flow.
LangChain	Provides vector store, embedding, and retriever support for document-based retrieval.
FAISS	Efficient vector similarity search for document embeddings.
OpenAI API	Supplies the language model for reasoning and synthesis.
SerperDevTool (CrewAI Tool)	Enables web search integration for dynamic information retrieval.
RAGTool (Custom)	Custom retrieval-augmented generation tool that pulls relevant content from a local knowledge base.
Streamlit UI	Simple web interface for user interaction.
🧩 System Architecture
🧩 Step 1: Document Processing

Text data is ingested using a LangChain TextLoader.

It’s split into chunks via RecursiveCharacterTextSplitter.

FAISS builds an in-memory vector store of embeddings (using OpenAIEmbeddings).

🧩 Step 2: Tool Creation

A RAGTool retrieves the top-k most relevant chunks for any query.

A SerperDevTool adds web search capability.

🧩 Step 3: Agents (Crew Members)

Each agent has a distinct role, LLM, memory, and toolset:

Planner Agent – Decomposes the main user query into smaller subtasks.

Research Agent – Retrieves data from RAGTool and web search.

Analyzer Agent – Synthesizes retrieved information into a coherent draft.

Reviewer Agent – Evaluates and refines the draft for accuracy, clarity, and tone.

🧩 Step 4: Crew Execution

Crew runs in sequential mode, meaning each agent’s output feeds into the next.

Execution is bounded by:

max_iterations=3
max_execution_time=300


Agents share memory (VectorStoreRetrieverMemory) for context continuity.

🧩 Step 5: Evaluation

A lightweight evaluator scores the final answer on:

Relevance

Accuracy

Coherence

🧩 Step 6: Streamlit Frontend

Users can input a query and see:

Final AI-generated answer

(Optionally) Evaluation metrics

🔍 Technical Highlights

✅ Multi-agent orchestration with CrewAI
✅ Context retrieval with FAISS + LangChain Embeddings
✅ Web search integration using SerperDevTool
✅ Custom RAG tool wrapped with CrewAI-compatible @tool() decorator
✅ End-to-end execution limited by time (300s) and iterations (3)
✅ Memory persistence for contextual continuity across agents
✅ Optional Streamlit UI for live demo

🧑‍💻 Tech Stack

Language: Python 3.11+

Libraries:

crewai>=0.36.0

crewai_tools>=0.12.0

langchain>=0.2.11

langchain_openai

faiss-cpu

streamlit

requests

Model: gpt-3.5-turbo or gpt-4-turbo (via langchain_openai.OpenAI)

🧩 Example Use Case

User enters:
“Explain the evolution of AI from the 1950s to now.”

The system executes:

Planner → Breaks query into subtasks (e.g., 1950s–1980s, 1990s–2010s, post-2010s).

Researcher → Pulls documents and searches the web.

Analyzer → Synthesizes a timeline-based explanation.

Reviewer → Refines style and correctness.

Final Output:
A coherent 3–4 paragraph summary explaining the evolution of AI by decade.

🧾 Possible Resume Line

Multi-Agent RAG Framework (CrewAI + LangChain):
Built a multi-agent system using CrewAI, LangChain, and FAISS where agents collaborate to plan, retrieve, synthesize, and review answers autonomously. Integrated OpenAI LLMs, vector-based retrieval, and web search tools. Implemented iteration and time-limited task orchestration with contextual memory for robust automated research.

🧠 Possible Future Enhancements

Integrate Google Search API or Wikipedia API instead of DuckDuckGo.

Add ReAct-style reasoning for dynamic task planning.

Replace OpenAI with local models via Ollama or Hugging Face.

Log agent decisions and intermediate outputs for explainability.
