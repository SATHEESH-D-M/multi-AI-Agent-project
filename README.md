# Multi AI Agent App

### Project Structure

```bash
.
├── Dockerfile
├── LICENSE
├── README.md
├── app
│   ├── backend
│   │   └── api.py
│   ├── common
│   │   ├── custom_exception.py
│   │   └── logger.py
│   ├── config
│   │   └── settings.py
│   ├── core
│   │   └── ai_agent.py
│   ├── frontend
│   │   └── ui.py
│   └── main.py
├── requirements.txt
└── setup.py
```

### Tech Stack

- Streamlit for interactive frontend
- FastAPI for backend API
- LangChain & LangGraph for AI agent orchestration
- Docker for containerized deployment

### About the Project

This project is a **Multi AI Agent Application** designed to run multiple AI agents collaboratively or independently. Each agent can process user queries, optionally use external search tools, and generate intelligent responses. The system is modular, allowing easy integration of new AI models or tools.

#### Core Components

- **AI Agent (**``**)**: Handles interactions with AI models using `ChatGroq`. Supports optional external search with `TavilySearchResults`. Wraps the logic in a reactive agent via `LangGraph`.

- **Backend (**``**)**: FastAPI-based backend exposing `/chat` endpoint. Validates model names, calls AI agent logic, and returns AI responses.

- **Frontend (**``**)**: Streamlit frontend that starts backend in a separate thread and allows users to interact with multiple AI agents.

- **Orchestrator (**``**)**: Launches both backend and frontend together.

- **Configuration (**``**)**: Loads environment variables (API keys) and stores allowed AI model names.

#### Agents in the System

1. **LLM Agent (ChatGroq)**: The main AI model that generates responses.
2. **LangGraph React Agent**: Maintains conversation state, orchestrates tools, and manages AI interactions.
3. **Tool Agent (TavilySearchResults)**: Optional search tool that provides external knowledge to the AI agent.

Together, these form a **multi-agent workflow** where AI reasoning, tool integration, and state management are combined.

### Adding the `.env` File

Create a `.env` file in the root directory with the following keys:

```env
GROQ_API_KEY=your_groq_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here
```

- Replace the placeholders with your actual API keys.
- This file is mandatory for authenticating the AI models and search tool.

### How It Works End-to-End

1. User inputs a message in the Streamlit frontend.
2. Frontend sends request to FastAPI `/chat` endpoint.
3. Backend calls `get_response_from_ai_agents` with model, system prompt, and messages.
4. The AI agent may query external tools if enabled.
5. LangGraph React Agent generates the response, returning it to the backend.
6. Backend sends the final AI response to the frontend.
7. Frontend displays the AI-generated message.

### Implementation Steps

1. Clone the repository.
2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Add the `.env` file with your API keys.
4. Start the backend API:

```bash
uvicorn app.main:app --reload
```

5. Launch the frontend:

```bash
streamlit run app/frontend/ui.py
```

6. Interact with multiple AI agents via the frontend.

### Docker Deployment

- Build the Docker image:

```bash
docker build -t multi-ai-agent-app .
```

- Run the container:

```bash
docker run -p 8501:8501 multi-ai-agent-app
```

This setup allows you to run the multi-agent AI system in a self-contained environment.

