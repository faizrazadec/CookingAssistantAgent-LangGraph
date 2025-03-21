# Cooking Assistant Agent Using LangGraph  

## Use Case
1. User ask the general Question. But user gets the refusal as the user query is not related to Cooking Assistant.
[Use_Case_1](backend/data/use_case_1.png)

This project implements a **Cooking Assistant Agent** powered by a **StateGraph** for decision-making, **Nodes and Edges** for workflow and **FastAPI** for endpoint exposure. The assistant classifies user queries, determines their relevance to cooking, and provides relevant recipes or explanations. The project is designed with modularity and scalability in mind.

---

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