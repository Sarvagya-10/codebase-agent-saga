# 🚀 The Codebase Agent Saga 🚀

**Project:** Codebase-to-API Documentation Generator Agent
**Mission:** To build an end-to-end AI agent that can ingest a source code repository, understand its structure, and generate high-quality API documentation on command.
**Total Sprint:** 60 Days

---

### 🗺️ Level 1: The Repository Ingester

**🗓️ Deadline:** November 1 - November 6
**Goal:** Create the "eyes" of the agent. Ingest a remote code repository and identify all target files.

* [ ] **Task 1: Setup Project Skeleton**
    * Create a new Git repository for this project.
    * Set up a Python virtual environment (e.g., `python -m venv .venv`).
    * Create your `README.md` and this `TODO.md`.
    * **Tools to Learn:** `git`, `python venv`

* [ ] **Task 2: Select Target Repository**
    * Find a medium-sized, open-source Python repository to be your test subject (e.g., `requests`, `flask`, or a smaller one).

* [ ] **Task 3: Build the Cloner Script**
    * Write a Python script (`ingest.py`) that can clone a repository from a given URL into a temporary directory.
    * **Tools to Learn:** `GitPython` (library)

* [ ] **Task 4: Build the File Scanner**
    * Extend the script to walk the cloned directory and find all files with a specific extension (e.g., `.py`).
    * The script should output a list of file paths.
    * **Tools to Learn:** `pathlib` (for `rglob`) or `os.walk`

---

### 🗺️ Level 2: The Semantic Chunker (AST)

**🗓️ Deadline:** November 7 - November 12
**Goal:** Go beyond simple text splitting. Disassemble the code into its semantic building blocks. This is the most critical and novel step.

* [ ] **Task 1: Understand Abstract Syntax Trees (AST)**
    * Read about AST and how Python uses it to represent code structure.
    * **Tools to Learn:** Python's `ast` (documentation)

* [ ] **Task 2: Parse a Single File**
    * Write a script that reads one `.py` file, parses it, and prints the tree.
    * **Tools to Learn:** `ast.parse()`, `ast.dump()`

* [ ] **Task 3: Isolate Target Nodes**
    * Write a "visitor" or a script to traverse the tree and extract only the nodes for functions and classes.
    * **Tools to Learn:** `ast.NodeVisitor`, `ast.FunctionDef`, `ast.ClassDef`

* [ ] **Task 4: Extract Metadata & Source**
    * For each function/class node, extract:
        1.  The function/class name.
        2.  The arguments (and their types, if available).
        3.  The docstring.
        4.  The *exact source code* of just that function/class.
    * **Tools to Learn:** `ast.get_source_segment()` (for source code)

* [ ] **Task 5: Integrate & Structure**
    * Your pipeline from Level 1 should now output a structured `list` of `JSON` objects, where each object is a semantic "chunk" (a function or class) with its metadata.

---

### 🗺️ Level 3: The Embedding Forge

**🗓️ Deadline:** November 13 - November 18
**Goal:** Convert the semantic code chunks (text) into numerical vectors (meaning).

* [ ] **Task 1: Select a Code Embedding Model**
    * Research and choose an embedding model specialized for code (e.g., `microsoft/codebert-base`, `BAAI/bge-large-en-v1.5`).
    * **Tools to Learn:** `Hugging Face Hub` (for finding models)

* [ ] **Task 2: Load the Model**
    * Write a script to download and load your chosen model from Hugging Face.
    * **Tools to Learn:** `transformers.AutoTokenizer`, `transformers.AutoModel`

* [ ] **Task 3: Create the Embedding Function**
    * Write a function that takes a code snippet (from Level 2's output) and returns its vector embedding.
    * Pay attention to mean pooling to get a single vector for the entire snippet.

* [ ] **Task 4: Integrate the Pipeline**
    * The main script now `Ingests` -> `Chunks (AST)` -> `Embeds`. The output is a list of `(metadata, vector)` tuples.

---

### 🗺️ Level 4: The Vector Database (The Vault)

**🗓️ Deadline:** November 19 - November 24
**Goal:** Build a searchable "memory" for the agent by storing all code vectors.

* [ ] **Task 1: Choose & Run the Vector DB**
    * Select a local-first, open-source DB.
    * **Tools to Learn:** `ChromaDB` (easiest start) or `Qdrant` / `Milvus` (via Docker)

* [ ] **Task 2: Connect and Create a "Collection"**
    * Write a script to connect to your DB and create a new "collection" (e.g., named after the repository).

* [ ] **Task 3: Build the "Upsert" Script**
    * Write a script that takes the `(metadata, vector)` tuples from Level 3 and "upserts" (updates/inserts) them into the database.
    * The `metadata` (filename, function name) is just as important as the `vector`.

* [ ] **Task 4: Run the Full Indexing Pipeline**
    * Run the complete `Ingest` -> `Chunk` -> `Embed` -> `Store` pipeline on your target repository.

---

### 🗺️ Level 5: The Retrieval Layer (The Seeker)

**🗓️ Deadline:** November 25 - November 30
**Goal:** Given a natural language query, find the most relevant code chunks from "The Vault."

* [ ] **Task 1: Build the Query Embedder**
    * The user's query (e.g., "how to use the user registration function?") must be embedded using the *exact same model* from Level 3.

* [ ] **Task 2: Implement Similarity Search**
    * Write a function that takes a query, embeds it, and searches the Vector DB for the "Top-K" (e.g., 5) most similar code chunks.

* [ ] **Task 3: Introduce the Orchestrator**
    * Start using a framework to manage this RAG (Retrieval-Augmented Generation) flow.
    * **Tools to Learn:** `LangChain` or `LlamaIndex` (for their `VectorStoreRetriever` abstractions)

* [ ] **Task 4: Test Retrieval**
    * Manually test with queries like "user class" or "database connection" and print the retrieved code snippets. Are they relevant?

---

### 🗺️ Level 6: Prompt Engineering (The Soul)

**🗓️ Deadline:** December 1 - December 6
**Goal:** Craft the "brain" and "personality" of the agent. This defines its task and output format.

* [ ] **Task 1: Create the System Prompt**
    * Write the master prompt template. It must include:
        * **Persona:** "You are a Senior Technical Writer, an expert in Python."
        * **Task:** "You will be given a user's question and several relevant code snippets. Your job is to write clear, concise API documentation answering the question."
        * **Rules:** "ONLY use the provided code snippets. Do NOT invent functions. If the answer is not in the snippets, say so."

* [ ] **Task 2: Create the User Prompt Template**
    * This template will dynamically include the user's question and the retrieved code chunks (from Level 5).
    * **Tools to Learn:** `LangChain` (for `PromptTemplate` / `ChatPromptTemplate`)

* [ ] **Task 3: Enforce Structured Output (Advanced)**
    * Instead of just Markdown, try to force the LLM to output a `JSON` object.
    * **Tools to Learn:** `Pydantic` (for defining the output schema)

---

### 🗺️ Level 7: The LLM (The Voice)

**🗓️ Deadline:** December 7 - December 12
**Goal:** Connect all the pieces to a Large Language Model to generate the final answer.

* [ ] **Task 1: Get LLM Access**
    * Get an API key for a model (e.g., `OpenAI`, `Anthropic`, `Gemini`).
    * (Alternatively, set up a local model with `Ollama` and `Llama 3`).

* [ ] **Task 2: Build the "RAG Chain"**
    * Using your orchestrator, chain all the steps together:
        1.  `Input(Question)` ->
        2.  `Retrieve(Code Chunks)` ->
        3.  `Format(Prompt)` ->
        4.  `Invoke(LLM)` ->
        5.  `Parse(Output)`
    * **Tools to Learn:** `LangChain Expression Language (LCEL)`

* [ ] **Task 3: Run End-to-End!**
    * Run your first *full query* from a command-line script. Input a question, and watch it print the generated documentation. This is the "Hello, World!" moment for your agent.

---

### L️ Level 8: The Frontend (The Face)

**🗓️ Deadline:** December 13 - December 18
**Goal:** Create a simple, interactive web app so others (or just you) can use your agent.

* [ ] **Task 1: Design the UI**
    * Plan a simple UI: Title, text input for GitHub URL, "Ingest" button, text input for query, "Generate" button, and a display area.

* [ ] **Task 2: Build the UI**
    * Use the fastest, easiest tool for the job.
    * **Tools to Learn:** `Streamlit`

* [ ] **Task 3: Manage State**
    * The "Ingest" button needs to run the Level 4 pipeline and *save* the resulting RAG chain. This is the hardest part of the frontend.
    * **Tools to Learn:** `Streamlit` (specifically `st.session_state` to store the agent)

* [ ] **Task 4: Connect the Agent**
    * Wire the "Generate" button to call the `agent.invoke()` method from Level 7 and display the streaming response in the UI.

---

### 🗺️ Level 9: Observability & Evaluation (The Conscience)

**🗓️ Deadline:** December 19 - December 24
**Goal:** Move from "it works" to "I know *how* and *why* it works."

* [ ] **Task 1: Set Up Tracing**
    * Integrate an observability tool to see the agent's internal thought process (e.g., what chunks did it retrieve? what was the exact prompt?).
    * **Tools to Learn:** `LangSmith` (it's built for LangChain and is free to start)

* [ ] **Task 2: Run Traced Queries**
    * Use your Streamlit app and watch the traces appear in your LangSmith dashboard. Debug any strange or inefficient steps.

* [ ] **Task 3: Create a "Golden Set"**
    * Create a small test file (`test_queries.json`) with 5-10 questions and the "perfect" answers you'd expect.

* [ ] **Task 4: Run Basic Evaluation**
    * Run your agent against the "Golden Set" and manually score its `Faithfulness` (did it hallucinate?) and `Answer Relevance`.

---

### 🗺️ Level 10: Infra & Deployment (The World)

**🗓️ Deadline:** December 25 - December 30
**Goal:** Package your agent to be run anywhere, by anyone. This is the final boss.

* [ ] **Task 1: Decouple UI from Backend**
    * Rewrite the agent logic (Level 7) as a self-contained API.
    * **Tools to Learn:** `FastAPI` (to create endpoints like `/ingest` and `/query`)

* [ ] **Task 2: Containerize the Backend**
    * Write a `Dockerfile` for your FastAPI application.
    * **Tools to Learn:** `Docker`

* [ ] **Task 3: Containerize the Full Stack**
    * Write a `docker-compose.yml` file that launches *two* services:
        1.  Your FastAPI app.
        2.  Your Vector Database (e.g., the official `qdrant/qdrant` or `milvusdb/milvus` image).
    * **Tools to Learn:** `Docker Compose`

* [ ] **Task 4: Deploy!**
    * (Stretch Goal) Deploy your containerized application to a cloud service.
    * **Tools to Learn:** `AWS (ECS/Fargate)`, `GCP (Cloud Run)`, or `Hugging Face Spaces`

---

## 🏆 PROJECT COMPLETE (December 31, 2025) 🏆

You did it. You've not only learned 10 distinct, high-demand technologies, but you've *integrated* them into a single, complex, and incredibly impressive portfolio project. You are no longer just a "student"; you are an AI Engineer.
