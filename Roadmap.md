# ⚔️ THE CRUSADER KNIGHT’S TRIAL ⚔️  
## *The Codebase Agent Campaign (30-Day Siege)*

> *“A knight is not judged by his vows, but by what still stands after the siege.”*

**Mission:**  
Forge an end-to-end AI system that ingests a codebase and generates faithful API documentation —  
under time pressure, resource limits, and real-world constraints.

**Total Campaign Length:** 30 Days  
**Daily Commitment:** ~3 Hours  
**Victory Condition:** A deployed, observable, defensible system

---

## 🏰 CAMPAIGN RULES (NON-NEGOTIABLE)

- One system. One codebase. One month.
- Scope cuts are honorable. Half-built systems are not.
- Elegance is secondary to survivability.
- Every level must end with something that *runs*.

---

# 🗺️ LEVEL I — THE MUSTERING OF ARMS
### *“A knight does not march unarmed.”*

**🗓️ Days:** 1–2  
**Goal:** Establish the battlefield and raise the banner.

---

* [ ] **Task 1: Raise the Banner (Project Skeleton)**
  * Create a new Git repository
  * Set up Python virtual environment
  * Create `README.md` and `DECISIONS.md`
  * Define folder structure
  * **Arms Issued:** `git`, `python`, `venv`

* [ ] **Task 2: Choose the Enemy Fortress**
  * Select ONE medium-sized open-source Python repository
  * Lock it. No switching.
  * Record why it was chosen.

* [ ] **Task 3: Write the Oath of Constraints**
  * Max cost (rough)
  * Max scope
  * Non-goals
  * Time limit acknowledged

🏁 **Level Complete When:**  
Repo clones, environment runs, constraints are written.

---

# 🗺️ LEVEL II — THE SCOUTS AND MAPMAKERS
### *“Know the terrain before you charge.”*

**🗓️ Days:** 3–4  
**Goal:** Gain vision over the codebase.

---

* [ ] **Task 1: Build the Cloning Script**
  * Clone repository from URL
  * Store in temp directory
  * Clean up after run
  * **Tools:** `GitPython`

* [ ] **Task 2: Scan the Terrain**
  * Recursively find `.py` files
  * Ignore virtual envs, tests if needed
  * Output list of file paths
  * **Tools:** `pathlib`, `os.walk`

* [ ] **Task 3: First Intelligence Report**
  * Count files
  * Identify complexity hotspots
  * Write findings in `DECISIONS.md`

🏁 **Level Complete When:**  
You can list every target file deterministically.

---

# 🗺️ LEVEL III — THE SCHOLARS OF CODE (AST)
### *“Strike where the structure lies.”*

**🗓️ Days:** 5–7  
**Goal:** Break code into semantic units worthy of memory.

---

* [ ] **Task 1: Parse a Single Scroll**
  * Parse one `.py` file using AST
  * Print the tree
  * Understand node hierarchy

* [ ] **Task 2: Identify Sacred Symbols**
  * Extract `FunctionDef` and `ClassDef`
  * Ignore everything else

* [ ] **Task 3: Extract the Relics**
  * For each unit, extract:
    - Name
    - Docstring
    - Source code
  * **Tools:** `ast`, `ast.NodeVisitor`, `ast.get_source_segment`

* [ ] **Task 4: Forge the Canonical Chunk Format**
  * Output structured JSON:
    ```json
    {
      "type": "function",
      "name": "",
      "file": "",
      "docstring": "",
      "source": ""
    }
    ```

🏁 **Level Complete When:**  
You can turn the entire repo into semantic chunks.

---

# 🗺️ LEVEL IV — THE FORGE OF MEMORY (EMBEDDINGS)
### *“Steel remembers.”*

**🗓️ Days:** 8–9  
**Goal:** Convert meaning into vectors.

---

* [ ] **Task 1: Choose the Alloy**
  * Select ONE embedding model
  * CPU-friendly
  * Lock the decision

* [ ] **Task 2: Forge the Embedding Function**
  * Input: code chunk
  * Output: vector
  * Mean pooling only
  * **Tools:** `transformers`, `torch`

* [ ] **Task 3: Bind Metadata to Steel**
  * Preserve filename, symbol name, type

🏁 **Level Complete When:**  
Chunks become searchable vectors.

---

# 🗺️ LEVEL V — THE VAULT OF RELICS (VECTOR DB)
### *“What is not stored is forgotten.”*

**🗓️ Days:** 10–11  
**Goal:** Create long-term memory.

---

* [ ] **Task 1: Establish the Vault**
  * Set up local vector database
  * **Tool of Choice:** `ChromaDB`

* [ ] **Task 2: Upsert the Arsenal**
  * Insert vectors + metadata
  * Ensure idempotency

* [ ] **Task 3: Trial Search**
  * Query by function name
  * Validate relevance

🏁 **Level Complete When:**  
You can retrieve meaningful code by similarity.

---

# 🗺️ LEVEL VI — THE SEEKER’S RITUAL (RAG)
### *“Ask, and the vault shall answer.”*

**🗓️ Days:** 12–14  
**Goal:** Answer questions truthfully using retrieved code.

---

* [ ] **Task 1: Build the Query Embedder**
  * Use SAME model as code embeddings

* [ ] **Task 2: Retrieve Top-K Chunks**
  * Implement similarity search
  * Print retrieved snippets

* [ ] **Task 3: Write the Sacred Prompt**
  * Persona: Senior Technical Writer
  * Rule: NO hallucinations
  * If answer missing → say so

* [ ] **Task 4: CLI Invocation**
  ```bash
  python ask.py "How does authentication work?"
🏁 **Level Complete When:**  
End-to-end RAG works via command line.

---

## 🗺️ LEVEL VII — THE HERALD’S VOICE (LLM)
> *“Words are weapons.”*

**🗓️ Days:** 15–16  
**Goal:** Generate faithful documentation.

---

* [ ] **Task 1: Connect to an LLM**
  * API-based or local
  * Record cost assumptions

* [ ] **Task 2: Chain the Ritual**
  * Query → Retrieve → Prompt → Generate

* [ ] **Task 3: Hallucination Trials**
  * Ask unanswerable questions
  * Confirm refusal behavior

🏁 **Level Complete When:**  
The agent speaks only what the code supports.

---

## 🗺️ LEVEL VIII — THE BANNER OF INTERFACE (UI)
> *“Let others witness your work.”*

**🗓️ Days:** 17–19  
**Goal:** Make the system usable.

---

* [ ] **Task 1: Build the Backend API**
  * `/ingest`
  * `/query`
  * **Tool:** FastAPI

* [ ] **Task 2: Build the War Table (UI)**
  * Repo input
  * Query input
  * Output display
  * **Tool:** Streamlit

* [ ] **Task 3: State Management**
  * Persist loaded agent
  * Prevent accidental resets

🏁 **Level Complete When:**  
A stranger can use the system.

---

## 🗺️ LEVEL IX — THE WATCHTOWER (OBSERVABILITY)
> *“What you cannot see will kill you.”*

**🗓️ Days:** 20–23  
**Goal:** Understand system behavior.

---

* [ ] **Task 1: Add Tracing / Logging**
  * Retrieved chunks
  * Prompt
  * Response

* [ ] **Task 2: Create the Golden Scrolls**
  * 5–7 test questions
  * Expected answers

* [ ] **Task 3: Run Evaluation**
  * Faithfulness
  * Relevance
  * Failure modes

🏁 **Level Complete When:**  
You can explain **why** answers are good or bad.

---

## 🗺️ LEVEL X — THE FINAL SIEGE (DEPLOYMENT)
> *“What survives the world is truth.”*

**🗓️ Days:** 24–30  
**Goal:** Package, deploy, and defend.

---

* [ ] **Task 1: Containerize the Backend**
  * Write `Dockerfile`

* [ ] **Task 2: Compose the Army**
  * Backend + Vector DB
  * `docker-compose.yml`

* [ ] **Task 3: One-Command Victory**
  ```bash
  docker-compose up
* [ ] **Task 4: Write the Chronicle**
  
   * Honest README
   * Known limitations
   * Design decisions
   * What you would change next campaign
