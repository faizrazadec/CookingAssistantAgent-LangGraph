# Cooking Assistant Agent Using LangGraph  

## Use Cases
1. User ask the general Question. But user gets the refusal as the user query is not related to Cooking Assistant.

<p align="center">
  <img src="backend/data/use_case_1.png" alt="Use Case 1" />
</p>

2. User asked `How to cook chicken curry`. and gets the recipe that will work on the available tools to the user.

<p align="center">
  <img src="backend/data/use_case_2.png" alt="Use Case 2" />
</p>

3. User asked for a recipe that needs oven, but get's the recipe that will cook the same thing using fry pan as oven is not in our available tools.

<p align="center">
  <img src="backend/data/use_case_3_1.png" alt="Use Case 3" />
  <img src="backend/data/use_case_3_2.png" alt="Use Case 3" />
  <img src="backend/data/use_case_3_3.png" alt="Use Case 3" />
</p>

---

## Prerequisites  
- Python 3.12 or above  
- `pip` (Python package manager)  
- Tavily API Key, Langsmith API Key and OpenAI API Key  

## Technology Stack  
- **Python**: Core programming language.  
- **FastAPI**: Lightweight web framework for building RESTful APIs.  
- **LangChain**: Framework for building AI-powered applications.  
- **LangGraph**: A custom state graph implementation for workflow.  
- **Tavily API**: Integrated for recipe search results. 
- **Docker**: Docker is a containerisation platform – it is a toolkit that allows you to build, deploy and manage containerised applications 
- **Streamlit**: Light weight UI framework for AI applications.
- **AWS**: Cloud for the deployment.

### LangGraph
LangGraph — is a low-level orchestration framework for building controllable agents. While langchain provides integrations and composable components to streamline LLM application development, the LangGraph library enables agent orchestration — offering customizable architectures, long-term memory, and human-in-the-loop to reliably handle complex tasks. To learn more about langgraph, visit langgraph official [git repo](https://github.com/langchain-ai/langgraph).

#### Why use LangGraph?
LangGraph is built for developers who want to build powerful, adaptable AI agents. Developers choose LangGraph for:

- Reliability and controllability. Steer agent actions with moderation checks and human-in-the-loop approvals. LangGraph persists context for long-running workflows, keeping your agents on course.
- Low-level and extensible. Build custom agents with fully descriptive, low-level primitives – free from rigid abstractions that limit customization. Design scalable multi-agent systems, with each agent serving a specific role tailored to your use case.
- First-class streaming support. With token-by-token streaming and streaming of intermediate steps, LangGraph gives users clear visibility into agent reasoning and actions as they unfold in real time.

#### LangGraph in Cooking Assistant
Langgraph is used to orchecterate the agent and to implement the workflow of the agent with more control, there are many other frameworks for the agent to build on, but they run agents automonously and have limited control. But langgraph pplay more role in providing hte more control in agents workflow.

<p align="center">
  <img src="backend/data/workflow.png" alt="Work FLow" />
</p>

"The Cooking Assistant begins with the classifier_agent, which assesses the user's query for cooking relevance.  Irrelevant queries are immediately routed to the refusal node, providing a rejection message.  Relevant queries proceed to the researcher_agent, a powerful ReAct agent. This agent utilizes web search to gather information, enabling it to think, observe, and act in response to the user's cooking-related needs.  Both paths ultimately converge at the end node, concluding the interaction."

Here's why this is better:

    Stronger Opening: Starts with a clear, direct statement of the system's purpose.
    Concise Node Names: Uses the node names directly, avoiding unnecessary "the" (e.g., "the classifier_agent" becomes "classifier_agent").
    Active Language: Uses strong verbs ("assesses," "routed," "utilizes") to convey action and capability.
    Benefit-Oriented: Emphasizes what the system does for the user ("providing a rejection message," "enabling it to...respond").
    Flow Emphasis: Highlights the branching logic and convergence at the end.
    Professional Tone: Maintains a professional and technical tone.
    Reduced Redundancy: Avoids repeating phrases like "the user provides a query."
    Focus on ReAct: Explicitly mentions the ReAct agent, highlighting its advanced capabilities.

Optional Enhancements (depending on context):

    Mentioning LangGraph: If you want to emphasize the technology, you could add a phrase like "Orchestrated by LangGraph..." at the beginning.
    Tool Specifics: If the web search tool has a specific name or characteristic, you could mention it (e.g., "leveraging the Tavily search tool").
    Output Format: If there's a specific format for the researcher's output (e.g., recipe steps, ingredient lists), you could mention it.

By using active language, focusing on benefits, and streamlining the description, you can create a more impactful explanation of your Cooking Assistant's workflow.

### Docker
Docker is a software platform that allows you to build, test, and deploy applications quickly. Docker packages software into standardized units called containers that have everything the software needs to run including libraries, system tools, code, and runtime. To learn more about docker, visit there official [doc](https://docs.docker.com/).


## Table of Contents
1. [Features](#features)  
2. [Technology Stack](#technology-stack)  
3. [Setup and Installation](#setup-and-installation)  
4. [Usage](#usage)  
5. [Project Structure](#project-structure)  
6. [API Endpoints](#api-endpoints)  
7. [Development Best Practices](#development-best-practices)  
8. [Testing](#testing)  
9. [Future Enhancements](#future-enhancements)  

---

## Features  
-   **Query Classification:** Classifier Agent determines if a user query is related to cooking or not.
-   **Recipe Retrieval:** Researcher Agent (React Agent) retrieves recipes and cooking information using the Tavily search tool.
-   **API Endpoint:** Provides a FastAPI endpoint for easy integration with web applications.
-   **Modular Design:** Organized code for maintainability and scalability.

---

## Technology Stack  
- **Python**: Core programming language.  
- **FastAPI**: Lightweight web framework for building RESTful APIs.  
- **LangChain**: Framework for building AI-powered applications.  
- **LangGraph**: A custom state graph implementation for decision-making.  
- **Tavily API**: Integrated for recipe search results.   

---

## Setup and Installation  

### Prerequisites  
- Python 3.8 or above  
- `pip` (Python package manager)  
- Tavily API Key, Langsmith API Key and OpenAI API Key  

### Steps  

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/faizrazadec/CookingAssistantAgent-LangGraph.git
   cd CookingAssistantAgent-LangGraph
   ```

2. **Create a Virtual Environment**:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate   # On Windows: .\env\Scripts\activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Set Environment Variables**:
   Create a `.env` file in the root directory:
   ```
   OPENAI_API_KEY=your_openai_api_key
   TAVILT_API_KEY=your_tavily_api_key
   ```

5. **Run the FastAPI Server**:
   ```bash
   uvicorn fastapi_app:app --host 0.0.0.0 --port 8000   # or Just Run the main.py file
   ```

6. **Test the API**:
   Use `curl`, Postman, or your preferred HTTP client to test the API (see [API Endpoints](#api-endpoints)).

---

## Usage  

### Example Request (Using `curl`):
#### Relevant Query:
```bash
curl -X POST "http://localhost:8000/query" -H "Content-Type: application/json" -d '{"user_input": "How do I bake a chocolate cake?"}'
```

#### Response:
```json
{
  "response": "To bake a chocolate cake, you will need..."
}
```

#### Irrelevant Query:
```bash
curl -X POST "http://localhost:8000/query" -H "Content-Type: application/json" -d '{"user_input": "What is the capital of France?"}'
```

#### Response:
```json
{
  "response": "Your Query is not related to Cooking."
}
```

---

## Project Structure  
```plaintext
CookingAssistantAgent-LangGraph/
├── backend/
│   ├── agents/
│   │   ├── api.py           # FastAPI endpoints
│   │   ├── langgraph_utils.py # LangGraph logic
│   │   ├── prompts.py       # Prompt templates
│   │   ├── logger.py        # Logging setup
│   │   └── ...
│   ├── Dockerfile
│   ├── docker-compose.yaml
├── main.py                # Main application entry point
├── requirements.txt       # Project dependencies
├── .env                   # Environment variables
├── .env.template          # Template for .env file
├── README.md               # Project documentation
```

---

## API Endpoints  

### 1. **POST /query**  
- **Description**: Handles user queries and determines whether to provide cooking-related responses or issue a refusal.  
- **Request**:  
  - Content-Type: `application/json`  
  - Body:  
    ```json
    {
      "user_input": "Your cooking-related question here"
    }
    ```
- **Response**:  
  - Success (Relevance):  
    ```json
    {
      "response": "Detailed cooking instructions or explanation."
    }
    ```
  - Refusal (Irrelevance):  
    ```json
    {
      "response": "Your Query is not related to Cooking."
    }
    ```

---

## Development Best Practices  

### Coding  
- Follow **PEP 8** style guidelines.  
- Use **docstrings** for documenting functions and classes.  
- Modularize code into reusable components (e.g., `graph_module.py`).  

### Logging  
- Log critical information for debugging and analytics using `logger`.  
- Avoid logging sensitive data such as API keys.  

### Testing  
- Write unit tests for the StateGraph logic and FastAPI endpoints.  
- Use tools like `pytest` and `httpx` for testing.  

### Environment Variables  
- Use a `.env` file for API keys and sensitive configurations.  
- Never hard-code sensitive information in the source code.  

---

## Testing  

1. **Unit Testing**:  
   Use `pytest` to test individual components, such as:  
   - StateGraph decision-making.  
   - Classifier and researcher agents.  

   Example:  
   ```bash
   pytest tests/
   ```

2. **API Testing**:  
   Use tools like `curl`, Postman, or `pytest-httpx` to test the `/query` endpoint.  

3. **Manual Testing**:  
   Test the API by running the server locally and sending requests.

---

## Future Enhancements  

1. **Authentication**:  
   Add API key-based authentication to secure endpoints.

2. **Advanced Query Classification**:  
   Implement multi-class classification to handle more query types.

3. **Enhanced Output**:  
   Return recipe links or step-by-step instructions with multimedia content.  

4. **Dockerization**:  
   Package the project into a Docker container for easy deployment.  

5. **Cloud Deployment**:  
   Deploy the API on AWS, Google Cloud, or Azure.  

---

## Contributing  

1. Fork the repository.  
2. Create a new branch:  
   ```bash
   git checkout -b feature-name
   ```
3. Commit your changes:  
   ```bash
   git commit -m "Add a new feature"
   ```
4. Push to the branch:  
   ```bash
   git push origin feature-name
   ```
5. Submit a pull request.  

---

## License  
This project is licensed under the [MIT License](LICENSE).

---

Feel free to modify the README for your specific use case. Let me know if you'd like help setting up automated testing or deployment!
