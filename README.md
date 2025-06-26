# 🔍 AI-Powered Search Chatbot

This project is a **Flask-based web chatbot** that uses **Retrieval-Augmented Generation (RAG)** to answer user queries from internal documents (indexed using Pinecone). It integrates:

- **LangChain** for orchestration
- **Ollama** (e.g., `gemma3:4b`) as the local LLM
- **Hugging Face Transformers** for embeddings
- **Pinecone** as the vector database
- **Flask** as the web backend

---

## 🚀 Features

- Upload and search internal documents (PDF, Word, etc.)
- Ask natural language questions
- Semantic search using vector embeddings
- RAG pipeline combining retrieval + LLM answer generation
- Web-based UI (via `index.html`)

---

## 🛠️ Tech Stack

| Layer            | Tool/Library                |
|------------------|-----------------------------|
| LLM              | [Ollama](https://ollama.com/) (`gemma3:4b`) |
| Embeddings       | Hugging Face Transformers   |
| Vector Store     | [Pinecone](https://www.pinecone.io/) |
| Framework        | Flask                       |
| Orchestration    | LangChain                   |
| Prompting        | Custom system prompt + human input |
| Environment Vars | `dotenv`                    |

---

## 📁 Folder Structure

```

project-root/
│
├── app.py                        # Flask app and RAG pipeline
├── requirements.txt              # Python dependencies
├── .env                          # Environment variables
│
├── src/
│   ├── helper.py                 # Helper for downloading embeddings
│   └── prompt.py                 # Custom system prompt for LLM
│
├── templates/
│   └── index.html                # Basic chat UI (if implemented)

````

---

## ⚙️ Setup Instructions

### 1. Clone the repo

```bash
git clone https://github.com/your-repo/chatbot-rag-pinecone.git
cd chatbot-rag-pinecone
````

### 2. Create `.env` file

```env
PINECONE_API_KEY=your_pinecone_api_key
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

> **Note**: You may need `certifi` to fix SSL issues:

```bash
pip install certifi
```

### 4. Run Ollama (if not already running)

```bash
ollama run gemma3:4b
```

> Or make sure `gemma3:4b` is available locally via:

```bash
ollama pull gemma3:4b
```

### 5. Run the app

```bash
python app.py
```

Then go to [http://localhost:8080](http://localhost:8080)

---

## 🔄 RAG Workflow (High Level)

1. **User Input** → from the web form (`POST /chat`)
2. **Retriever** → fetches top-k similar document chunks using Pinecone
3. **Prompt Template** → combines user input + retrieved context
4. **LLM** → `gemma3:4b` generates the final answer
5. **Response** → returned to frontend in JSON

---

## 🧠 Example Usage

```
User: What is the role of the human resource function?

Bot: The human resource function’s roles include initiating and developing HR policies, implementing and monitoring those policies, and facilitating staff recruitment. Additionally, the function assists in establishing the organization’s structure.
```

---

## 📝 Notes

* If you want to add more documents, use Pinecone upsert with `embeddings.embed_documents()`.
* You can replace Ollama with another LLM (e.g. OpenAI or Claude) by modifying the `ChatOllama` line.
* Ensure that your `.env` and Pinecone index are correctly set up before running.

---

## 📌 Requirements

* Python 3.9+
* Pinecone account & API key
* Ollama installed locally
* Internet connection (for initial embedding downloads)


