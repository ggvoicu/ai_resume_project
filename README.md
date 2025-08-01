
# AI Resume RAG

**AI Resume RAG** is a tool designed to ingest resumes in PDF format, extract metadata (such as skills and years of experience), and enable semantic search using a vector store and PostgreSQL for efficient querying.

---

## 📌 Key Features

- **PDF Resume Ingestion**: Extract text, metadata, and structured data from resumes.
- **LLM Integration**: Leverage advanced models (e.g., `qwen3:8b`, `bge-m3:latest`, `hf.co/mradermacher/AF-NER-lh-GGUF:Q4_K_M`) for semantic understanding and skill extraction.
- **Vector Store Search**: Use Qdrant for semantic search.
- **PostgreSQL Search**: Use PostgreSQL for simple keyword-based queries.
- **Nginx Server**: Pre-configured to serve PDF files directly from the LLM chat interface (no configuration required).
- **Docker-Ready**: Easy deployment with Docker Compose.
- **Modular Architecture**: Separates concerns between resume ingestion, LLM processing, and search.

---

## 🛠️ Installation

### Prerequisites

- [Docker CE](https://docs.docker.com/engine/install/ubuntu/) installed.
- [Ollama](https://ollama.com/) installed with the following models downloaded:
  - `ollama pull qwen3:8b`
  - `ollama pull bge-m3:latest`
  - `ollama pull hf.co/mradermacher/AF-NER-Ih-GGUF:Q4_K_M`

### Steps

1. **Copy Environment File**  
   ```bash
   cp .env.example .env
   ```

   Modify the `.env` file with your configuration (e.g., Ollama, Qdrant, PostgreSQL credentials).

2. **Start Docker Containers**  
   ```bash
   docker-compose up -d
   ```

3. **Access the App**  
   Open your browser at `http://localhost:5678`.

4. **Configure Credentials**  
   - **Ollama**: Use `http://localhost:11434` if local.
   - **Qdrant**: Use `http://qdrant:6333` with an empty API key.
   - **PostgreSQL**: Host is `postgres`, with credentials from `.env`.

5. **Import Workflow**  
   - Navigate to **Workflows**.
   - From the upper right corner, select **Import from File**.
   - Import the `resume_rag.json` file from the source code.
   - Press **Save** and activate the workflow by checking the checkbox beside the **Save** button.

6. **Customize HTML Interface**  
   - Copy the **Chat Trigger** URL from the workflow.
   - Copy the **Production URL** from the **On Form Submission** node.
   - Open the `index.html` file from the source code.
   - Modify the `<iframe>` tag:
     - Set `src` to your **Chat Trigger** URL.
     - Set `href` to your **Production URL**.

---

## 📥 Usage

### Option 1: Use the HTML Interface

- Open the `index.html` file in a browser.
- Use the **Chatbox** to ask the LLM about resume skills, experience, or other metadata.
- Click the **Upload Resumes** button to open a new tab and upload up to 50 files.

### Option 2: Use the n8n Workflow

- In the n8n workflow:
  - Click **Execute Workflow** next to the **On Form Submission** node to upload resumes.
  - Use the **Chat Trigger** node to open the chat interface and interact with the LLM.
  - View logs and workflow details from the **On Form Submission** node.

---

## 📁 File Structure

```
.
├── .env.example
├── nginx.conf
├── resume_rag.json
├── index.html
└── docker-compose.yml
```

---
### 🌐 Nginx Server

- The **Nginx server is pre-configured** and does not require any changes.
- It is used to serve uploaded PDF files directly from the LLM chat interface.
- No manual configuration is needed; it is automatically handled during the Docker setup.

---
## 📌 Contributing

- **Fork** the repository and make your changes.
- **Submit a Pull Request** with a clear description of your changes.
- **Code Quality**: Ensure tests pass and follow PEP8 guidelines.

---

## 📄 License

This project is licensed under the **GPL-3.0**. See the [LICENSE](LICENSE) file for details.

---

### 🔧 Troubleshooting

- If Docker fails to start, ensure all dependencies (Ollama, Docker) are running.
- If the LLM fails to load, verify that the required models are installed in Ollama.

---

### 🎯 Project Goals

- Enable efficient resume processing and semantic search for HR and recruitment tools.
- Provide a scalable and modular architecture for future extensions.

---

## 📚 Acknowledgments

- [Ollama](https://ollama.com/) for the LLM integration.
- [Qdrant](https://qdrant.tech/) for vector search.
- [Docker](https://www.docker.com/) for containerization.
