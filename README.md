# GenAI Code Debugger : AI-powered debugging that finds, explains, and fixes bugs

**GenAI Code Debugger** is an intelligent Python code debugging system that combines deterministic AST-based analysis with a locally hosted Qwen 2.5 Coder model through Ollama. It analyzes code, logs, and user queries to identify bugs, explain their causes, and suggest fixes using a multi-pass LLM pipeline with RAG-based context retrieval.

---

## Features

- Deterministic AST-based detection of common Python bugs
- AI-powered detection and explanation of semantic and runtime issues
- Multi-pass LLM analysis for improved debugging accuracy
- RAG-based retrieval of relevant debugging knowledge and context
- Critique-and-refine stage to validate and improve generated results
- Automatic deduplication and renumbering of detected bugs
- FastAPI backend for code debugging through REST APIs
- React + Vite frontend for interactive code analysis
- Local LLM execution using Qwen 2.5 Coder through Ollama

---

## Tech Stack

**Frontend:**
- React
- Vite
- JavaScript

**Backend:**
- Python
- FastAPI

**AI & LLM:**
- Qwen 2.5 Coder
- Ollama
- LLM-based code analysis
- RAG

**Static Analysis:**
- Python AST

**Retrieval:**
- FAISS
- Chroma

**API:**
- REST API
- JSON

---

## How It Works

The debugging pipeline combines traditional static analysis with LLM-based reasoning:

1. **AST Analysis**  
   Python code is analyzed using the AST module to detect known structural bug patterns.

2. **LLM Analysis**  
   The code, logs, detected issues, and retrieved context are passed to the local Qwen 2.5 Coder model for deeper analysis.

3. **Second Pass Analysis**  
   Longer code snippets can go through an additional analysis pass to identify further issues.

4. **Critique & Refinement**  
   The generated response is reviewed to identify missed issues, incorrect fixes, or hallucinations.

5. **Deduplication**  
   Repeated bug reports are merged and the final issues are consistently renumbered.

---

## Supported Bug Patterns

- `=+` used instead of `+=`
- Mutable module-level state
- Division without zero checks
- `max()` / `min()` on potentially empty containers
- Date-string comparison issues
- Call-chain division issues
- Counter reassignment and return-flow issues
- Other semantic bugs identified through LLM analysis and logs

---

## Setup Instructions

### 1. Clone the Repository

    git clone https://github.com/an-iqbal/genai-code-debugger.git
    cd genai-code-debugger

### 2. Backend Setup

    cd backend
    python -m venv venv

Activate the virtual environment:

**Windows:**

    venv\Scripts\activate

**macOS/Linux:**

    source venv/bin/activate

Install the required packages:

    pip install -r requirements.txt

### 3. Configure Ollama

Install Ollama and pull the required model:

    ollama pull qwen2.5-coder:7b-instruct

Start Ollama:

    ollama serve

Create a `.env` file inside the `backend` directory:

    OLLAMA_URL=http://localhost:11434/api/generate
    MODEL=qwen2.5-coder:7b-instruct

### 4. Build the Knowledge Base

    python scripts/build_knowledge_base.py
    python scripts/build_index.py

### 5. Run the Backend

    uvicorn main:app --reload --port 8000

The backend will be available at:

    http://localhost:8000

### 6. Run the Frontend

Open a new terminal:

    cd frontend
    npm install
    npm run dev

The frontend will be available at:

    http://localhost:5173

---

## API Usage

### `POST /debug`

**Request:**

    {
      "query": "Identify all the bugs",
      "code": "total = 0\n\ndef process(x):\n    total =+ x\n",
      "logs": "total shows 5 after 3 calls — expected 15"
    }

The API returns detected AST issues along with the LLM-generated analysis, critique, and refined final answer.

---

## Project Highlights

- Combines **deterministic static analysis with LLM reasoning**
- Uses **RAG to provide relevant debugging context**
- Runs the LLM **locally** through Ollama
- Uses a **multi-pass architecture** to improve analysis quality
- Provides an interactive **React frontend and FastAPI backend**
- Designed to reduce hallucinated fixes through automated critique and refinement

---

## Contact

Have questions or suggestions? I’d love to hear from you!

- Anwar Iqbal: [anwariqbal.work@gmail.com](mailto:anwariqbal.work@gmail.com)

---

## Contributing

Contributions are welcome! Feel free to submit issues or open pull requests to improve the project.
