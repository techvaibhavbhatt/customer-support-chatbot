# 🤖 Customer Support Chatbot (RAG + LangGraph)

### An AI-powered customer support chatbot that answers questions using a knowledge base instead of generating unsupported information.

## 📌 Overview

Customer Support Chatbot is an AI-powered application built using **Retrieval-Augmented Generation (RAG)** and **LangGraph**.

The chatbot helps users get answers to common customer support questions related to orders, refunds, payments, delivery, and account issues.

Instead of relying only on an LLM's general knowledge, the application retrieves relevant information from a customer support knowledge base and uses that information to generate accurate, context-aware responses.

The project also supports conversational memory, topic-based retrieval, and human handoff when the available information is insufficient.

## 🎥 Demo

Watch the chatbot in action:

[▶️ View Project Demo](https://github.com/user-attachments/assets/0cba991a-a77e-460a-9a48-641ea12293a8)

## ✨ Key Features

- **RAG-based Question Answering:** Retrieves relevant information from a knowledge base before generating answers.
- **Topic Classification:** Identifies whether a question relates to orders, refunds, delivery, payments, or another support category.
- **Conversational Memory:** Maintains conversation context so users can ask follow-up questions.
- **Vector Search:** Uses ChromaDB to find semantically relevant support information.
- **Human Handoff:** Recognizes when the available knowledge is insufficient and recommends connecting with a human support agent.
- **Web Interface:** Provides an interactive chatbot UI using Streamlit.
- **REST API:** Exposes chatbot functionality through FastAPI.

## 🏗️ System Architecture

```text
             User Question
                   |
                   v
             Streamlit UI
                   |
                   v
              FastAPI
                   |
                   v
             LangGraph Agent
                   |
                   v
            Topic Classification
                   |
                   v
           Knowledge Base Search
                   |
                   v
             ChromaDB
                   |
                   v
         Relevant Context Retrieval
                   |
                   v
            LLM (Perplexity)
                   |
                   v
          Response Generation
                   |
                   v
             Final Answer
                   |
                   v
              User
```

If the retrieved information is insufficient, the chatbot can recommend human support instead of guessing.

## 🔄 How It Works

1. **User Input:** The user submits a question through the Streamlit interface.
2. **API Request:** FastAPI receives the question and forwards it to the LangGraph workflow.
3. **Topic Classification:** The agent identifies the topic to improve knowledge base retrieval.
4. **Information Retrieval:** ChromaDB searches for relevant support information using vector similarity.
5. **Context Processing:** Retrieved information is passed to the language model.
6. **Response Generation:** Perplexity Sonar generates a response based on the retrieved context.
7. **Conversation Memory:** Previous conversation context is maintained to support follow-up questions.
8. **Human Handoff:** If sufficient information is unavailable, the chatbot avoids making unsupported claims and suggests human assistance.

## 🧠 Understanding the RAG Pipeline

The application follows a Retrieval-Augmented Generation workflow.

| Component          | Responsibility                                     |
| ------------------ | -------------------------------------------------- |
| Retrieval          | Finds relevant information from the knowledge base |
| Context Processing | Prepares retrieved information for the LLM         |
| Generation         | Produces a natural-language response               |
| Validation         | Helps avoid unsupported answers                    |

### Knowledge Base

The chatbot uses the **Bitext Customer Support Dataset**, containing approximately 27,000 customer support question-and-answer pairs.

The dataset is processed and indexed using `ingest_demo.py`.

The resulting embeddings are stored in ChromaDB for semantic retrieval.

## 🛠️ Tech Stack

| Technology            | Purpose                                |
| --------------------- | -------------------------------------- |
| Python                | Core application logic                 |
| LangGraph             | Agent workflow and conditional routing |
| Perplexity Sonar      | Language model                         |
| Sentence Transformers | Local text embeddings                  |
| ChromaDB              | Vector database                        |
| FastAPI               | Backend REST API                       |
| Streamlit             | Frontend interface                     |
| Docker Compose        | Application packaging                  |

## 📂 Project Structure

```text
customer-support-chatbot/
│
├── kbase.py          # Knowledge base creation
├── bot.py            # LangGraph agent workflow
├── api.py            # FastAPI backend
├── app.py            # Streamlit frontend
├── ingest_demo.py    # Dataset ingestion
│
├── requirements.txt  # Python dependencies
├── .env.example      # Environment variables example
├── Dockerfile
├── docker-compose.yml
│
└── README.md
```

## ⚙️ Installation & Setup

### Prerequisites

- Python 3.10+
- Conda or Python virtual environment
- Perplexity API key

### 1. Clone the Repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL

cd customer-support-chatbot
```

### 2. Create a Virtual Environment

Using Conda:

```bash
conda create -n supportbot python=3.11 -y

conda activate supportbot
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure API Key

Set your Perplexity API key:

```bash
export PPLX_API_KEY="your-api-key"
```

For Windows PowerShell:

```powershell
$env:PPLX_API_KEY="your-api-key"
```

Never upload your API key to GitHub.

### 5. Start the Backend

Open the first terminal:

```bash
uvicorn api:app --reload --port 8000
```

### 6. Start the Frontend

Open another terminal:

```bash
streamlit run app.py --server.headless true
```

### 7. Open the Application

| Service           | URL                        |
| ----------------- | -------------------------- |
| Streamlit UI      | http://localhost:8501      |
| FastAPI Backend   | http://localhost:8000      |
| API Documentation | http://localhost:8000/docs |

## 🧪 Example Use Cases

The chatbot can handle questions such as:

**Order Support**

- Where is my order?
- How can I track my shipment?

**Refund Support**

- What is your refund policy?
- How long does a refund take?

**Payment Support**

- Why did my payment fail?
- What should I do if I was charged twice?

**Human Support**

- I need help with an issue that is not covered in the knowledge base.

## 📚 What I Learned

Building this project helped me understand:

- How Retrieval-Augmented Generation works in practical applications.
- How to create and query a vector database.
- How LangGraph manages agent state and conditional workflows.
- How conversational memory improves multi-turn interactions.
- Why metadata filtering can improve retrieval relevance.
- How to connect an AI workflow with a REST API and frontend.
- How to handle cases where the knowledge base does not contain an answer.

## 🔮 Future Improvements

- Stream responses token by token.
- Integrate real order-tracking APIs.
- Store conversation history in a persistent database.
- Add user authentication and session management.
- Improve retrieval quality using reranking.
- Add feedback collection to evaluate answer quality.
- Deploy the application to a cloud platform.

## 🎯 Project Goal

The goal of this project was to understand how modern AI-powered customer support systems work internally.

It demonstrates practical implementation of RAG, vector search, conversational memory, agent workflows, and API integration.

---

**Built with Python, LangGraph, RAG, FastAPI, and Streamlit.**
