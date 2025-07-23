# Code Style Guide for "Snippy" Project

This style guide outlines the coding standards and best practices for the "Snippy" project, an Azure Functions Python v2 application. It highlights Python coding standards, Azure Functions best practices, async patterns, logging conventions, error handling, and specific patterns used in Azure AI Agents integration. The guide is designed to ensure code consistency, readability, and maintainability across the codebase.

## Naming Conventions

### General Naming Rules
- Use `snake_case` for variable and function names.
- Classes and exceptions should use `CamelCase`.
- For constants, use `UPPER_SNAKE_CASE`.

### Azure-Specific Naming
- Names related to Azure components, such as clients and services, should be prefixed with the component name (e.g., `azure_client`, `ai_agent_service`).

### Examples
```python
def fetch_data_from_db():
    # Function name using snake_case
    pass

class AgentServiceClient:
    # Class name in CamelCase
    pass

API_KEY = os.getenv("API_KEY")
# Constant in UPPER_SNAKE_CASE
```

## Code Organization

### Modules and Packages
- Organize code into modules and packages by functionality (e.g., authentication, database operations).
- Keep functions and classes cohesive within each module.

### Azure Functions Organization
- Use the blueprint model to structure Azure Functions.
- Group related functions in a blueprint file.

### Examples
```python
# Blueprint file structure
from azure.functions import Blueprint

bp = Blueprint()

@bp.function_name
async def run_agent():
    # Function logic
    pass
```

## Documentation Standards

### Docstrings
- Use Google-style docstring summaries for all public functions and classes.
- Include descriptions of parameters, return types, and any raised exceptions.

### Examples
```python
def process_request(request: dict) -> dict:
    """
    Process incoming request and return response.

    Args:
        request (dict): The request data.

    Returns:
        dict: Processed response.

    Raises:
        ValueError: If request is invalid.
    """
    pass
```

## Error Handling

### Try/Catch Blocks
- Use try/catch blocks for handling expected errors gracefully.
- Always log errors with details before raising them to help in debugging.

### Examples
```python
try:
    result = ai_agent.perform_task()
except Exception as e:
    logging.error(f"An error occurred: {e}")
    raise
```

## Logging Practices

### Logging Levels
- Use `INFO` level logging for general application flow.
- Use `ERROR` level logging to capture exceptions and unexpected events.

### Examples
```python
import logging

logging.info("Starting Azure agent service...")
logging.error("Failed to perform operation", exc_info=True)
```

## Async Patterns

### Async/Await Usage
- Always use async functions for I/O-bound tasks, such as database or network calls.
- Use `await` with coroutine calls.

### Examples
```python
async def fetch_data():
    response = await aiohttp_client.get(url)
    data = await response.json()
    return data
```

## Azure AI Agents Integration

### Authentication
- Use `DefaultAzureCredential` for authenticating Azure services.

### Agent Setup
- Properly configure clients and agents with necessary credentials and parameters.

### Examples
```python
from azure.identity import DefaultAzureCredential
from azure.ai.agents import AgentService

credential = DefaultAzureCredential()
agent_service_client = AgentService(credential=credential)

agent = agent_service_client.create_agent()
```

## Environment Variables for Configuration

- Configuration settings should be accessed via environment variables to keep sensitive data secure.
- Use `os.getenv()` to fetch configuration data.

### Examples
```python
database_url = os.getenv("DATABASE_URL")
```

By adhering to this style guide, developers working on the "Snippy" project can ensure a high standard of code quality and consistency across the codebase. These practices will facilitate collaboration and support the long-term maintainability of the project.
