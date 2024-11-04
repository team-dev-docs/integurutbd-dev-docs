

  # Integuru API Reference

This document provides a comprehensive API reference for Integuru, detailing the main classes and functions that users can interact with to create custom integration scripts and applications.

## IntegrationAgent

The `IntegrationAgent` class is the core component of Integuru, responsible for identifying and processing integration steps.

### Constructor

```python
IntegrationAgent(prompt: str, har_file_path: str, cookie_path: str)
```

- `prompt`: A string describing the integration task.
- `har_file_path`: Path to the HAR file containing network requests.
- `cookie_path`: Path to the file containing cookie information.

### Main Methods

#### end_url_identify_agent

```python
end_url_identify_agent(state: AgentState) -> AgentState
```

Identifies the URL responsible for a specific action based on the given prompt.

#### input_variables_identifying_agent

```python
input_variables_identifying_agent(state: AgentState) -> AgentState
```

Identifies input variables present in the cURL command.

#### dynamic_part_identifying_agent

```python
dynamic_part_identifying_agent(state: AgentState) -> AgentState
```

Identifies dynamic parts present in the cURL command.

#### url_to_curl

```python
url_to_curl(state: AgentState) -> AgentState
```

Identifies the master cURL command responsible for the action.

#### find_curl_from_content

```python
find_curl_from_content(state: AgentState) -> AgentState
```

Finds the cURL command that contains the dynamic parts.

### Example Usage

```python
from integuru.agent import IntegrationAgent

agent = IntegrationAgent(
    prompt="Log in to the user account",
    har_file_path="path/to/har/file.har",
    cookie_path="path/to/cookie/file.txt"
)

# Initialize the agent state
state = AgentState()

# Run the agent pipeline
state = agent.end_url_identify_agent(state)
state = agent.url_to_curl(state)
state = agent.dynamic_part_identifying_agent(state)
state = agent.input_variables_identifying_agent(state)
state = agent.find_curl_from_content(state)
```

## DAGManager

The `DAGManager` class manages the Directed Acyclic Graph (DAG) representation of the integration steps.

### Constructor

```python
DAGManager()
```

### Main Methods

#### add_node

```python
add_node(
    node_type: Literal["cookie", "master", "cURL", "not found"],
    content: Optional[dict] = None,
    dynamic_parts: Optional[List[str]] = None,
    extracted_parts: Optional[List[str]] = None,
    input_variables: Optional[Dict[str, str]] = None
) -> str
```

Adds a new node to the DAG and returns the node ID.

#### update_node

```python
update_node(node_id: str, **attributes: Optional[List[str]])
```

Updates the attributes of an existing node.

#### add_edge

```python
add_edge(from_node_id: str, to_node_id: str)
```

Adds an edge between two nodes in the DAG.

#### detect_cycles

```python
detect_cycles() -> Optional[List]
```

Detects cycles in the DAG and returns the list of nodes involved in the cycle, if any.

#### get_node

```python
get_node(node_id: str) -> Optional[Dict]
```

Retrieves the attributes of the specified node.

### Example Usage

```python
from integuru.models.DAGManager import DAGManager

dag_manager = DAGManager()

# Add nodes
login_node = dag_manager.add_node(
    node_type="cURL",
    content={"key": "login_request", "value": "login_response"},
    dynamic_parts=["session_token"]
)

dashboard_node = dag_manager.add_node(
    node_type="cURL",
    content={"key": "dashboard_request", "value": "dashboard_response"}
)

# Add edge
dag_manager.add_edge(login_node, dashboard_node)

# Update node
dag_manager.update_node(login_node, extracted_parts=["user_id"])

# Check for cycles
cycles = dag_manager.detect_cycles()
if cycles:
    print("Cycle detected:", cycles)
else:
    print("No cycles in the DAG")
```

## LLMSingleton

The `LLMSingleton` class provides a singleton instance for managing the Language Model (LLM) used in Integuru.

### Main Methods

#### get_instance

```python
@classmethod
get_instance(cls, model: str = None) -> ChatOpenAI
```

Returns a singleton instance of the ChatOpenAI model.

#### set_default_model

```python
@classmethod
set_default_model(cls, model: str)
```

Sets the default model to use when no specific model is requested.

#### revert_to_default_model

```python
@classmethod
revert_to_default_model(cls)
```

Reverts to the default model.

#### switch_to_alternate_model

```python
@classmethod
switch_to_alternate_model(cls) -> ChatOpenAI
```

Switches to an alternate model (o1-preview) and returns its instance.

### Example Usage

```python
from integuru.util.LLM import LLMSingleton

# Get the default LLM instance
llm = LLMSingleton.get_instance()

# Set a custom default model
LLMSingleton.set_default_model("gpt-3.5-turbo")

# Get an instance with the new default model
new_llm = LLMSingleton.get_instance()

# Switch to the alternate model
alternate_llm = LLMSingleton.switch_to_alternate_model()

# Use the LLM in your application
response = llm.invoke("What is the capital of France?")
print(response)
```

This API reference provides an overview of the main components of Integuru: IntegrationAgent, DAGManager, and LLMSingleton. By using these classes and their methods, you can create custom integration scripts and applications that leverage Integuru's capabilities for identifying and processing integration steps, managing the integration flow, and utilizing language models for decision-making.

  