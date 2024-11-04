

  # Getting Started with Integuru

Welcome to Integuru! This guide will walk you through the process of setting up and using Integuru, a powerful tool for automating web interactions and creating integrations.

## Installation

To get started with Integuru, follow these steps:

1. Ensure you have Python 3.7 or later installed on your system.
2. Install Integuru using pip:

```bash
pip install integuru
```

3. Create a `.env` file in your project directory to store any necessary environment variables.

## Basic Usage

Integuru is primarily used through its Command Line Interface (CLI). Here's how to use the basic features:

### Running Integuru

To run Integuru, use the following command structure:

```bash
python -m integuru --model <model_name> --prompt "<your_prompt>" [additional options]
```

### CLI Options

- `--model`: Specify the LLM model to use (default is "gpt-4o")
- `--prompt`: The prompt for the model (required)
- `--har-path`: Path to the HAR file (default is "./network_requests.har")
- `--cookie-path`: Path to the cookie file (default is "./cookies.json")
- `--max_steps`: Maximum number of steps to execute (default is 20)
- `--input_variables`: Input variables in the format key value (can be used multiple times)
- `--generate-code`: Flag to generate the full integration code

### Example Usage

Here's a basic example of how to use Integuru:

```bash
python -m integuru --model gpt-4 --prompt "Log into my Gmail account and send an email" --input_variables username "myemail@example.com" password "mypassword"
```

## Main Features

1. **Automated Web Interactions**: Integuru can perform complex web tasks based on natural language prompts.
2. **Flexible Model Selection**: Choose from different LLM models to power your automations.
3. **HAR and Cookie Integration**: Use HAR files and cookies to enhance the accuracy of web interactions.
4. **Variable Input**: Pass dynamic variables to your automations for flexible execution.
5. **Code Generation**: Optionally generate full integration code for your automations.

## Advanced Usage

### Using Custom HAR and Cookie Files

To use custom HAR and cookie files:

```bash
python -m integuru --model gpt-4 --prompt "Your prompt here" --har-path "/path/to/your/har_file.har" --cookie-path "/path/to/your/cookies.json"
```

### Generating Integration Code

To generate the full integration code:

```bash
python -m integuru --model gpt-4 --prompt "Your prompt here" --generate-code
```

### Limiting Execution Steps

To limit the number of execution steps:

```bash
python -m integuru --model gpt-4 --prompt "Your prompt here" --max_steps 10
```

## Troubleshooting

- Ensure all required files (HAR, cookies) are in the correct locations.
- Check your `.env` file for any necessary API keys or credentials.
- If you encounter issues, try updating to the latest version of Integuru.

For more detailed information and advanced usage, please refer to our full documentation.

  