

  # Configuring Integuru: A Comprehensive Guide

Integuru is a powerful tool for automating web interactions and integrations. This guide will walk you through the process of configuring Integuru for various use cases, including command-line options, environment variables, and preparing necessary files.

## Command-Line Options

Integuru provides several command-line options to customize its behavior. Here's a breakdown of the available options:

```bash
integuru --model MODEL --prompt PROMPT [OPTIONS]
```

- `--model MODEL`: Specify the LLM model to use (default is "gpt-4o")
- `--prompt PROMPT`: The prompt for the model (required)
- `--har-path HAR_PATH`: Path to the HAR file (default is "./network_requests.har")
- `--cookie-path COOKIE_PATH`: Path to the cookie file (default is "./cookies.json")
- `--max_steps MAX_STEPS`: Maximum number of steps for the integration (default is 20)
- `--input_variables KEY VALUE`: Input variables in the format key value (can be used multiple times)
- `--generate-code`: Flag to generate the full integration code

### Example Usage

```bash
integuru --model gpt-4 --prompt "Fetch user data from API" --har-path ./my_requests.har --cookie-path ./my_cookies.json --max_steps 30 --input_variables api_key abcdef123456 --generate-code
```

## Setting Up Environment Variables

Integuru uses environment variables for configuration. To set these up:

1. Create a `.env` file in your project root directory.
2. Add your configuration variables:

```
OPENAI_API_KEY=your_openai_api_key_here
ANTHROPIC_API_KEY=your_anthropic_api_key_here
```

3. Integuru will automatically load these variables using the `python-dotenv` library.

## Preparing HAR Files

HAR (HTTP Archive) files are crucial for Integuru to understand the network requests of your web application. To prepare a HAR file:

1. Open your web browser's developer tools (usually F12 or Ctrl+Shift+I).
2. Go to the Network tab.
3. Perform the actions you want to automate on the website.
4. Right-click in the Network tab and select "Save all as HAR".
5. Save the file (default name is `network_requests.har`) in your project directory.

Integuru will process this file, filtering out unnecessary requests and focusing on the essential API calls and interactions.

## Preparing Cookie Data

Cookie data is often necessary for authenticated sessions. To prepare your cookie data:

1. Export your cookies from your browser as a JSON file.
2. Save the file (default name is `cookies.json`) in your project directory.

The cookie file should have the following structure:

```json
[
  {
    "name": "cookie_name",
    "value": "cookie_value",
    "domain": "example.com",
    "path": "/",
    "expires": 1234567890,
    "httpOnly": true,
    "secure": true,
    "sameSite": "Lax"
  },
  // ... more cookies
]
```

Integuru will parse this file and use the cookie data for authenticated requests.

## Best Practices

1. **Security**: Always keep your API keys and sensitive data in the `.env` file and ensure it's not committed to version control.

2. **HAR File Maintenance**: Regularly update your HAR files to reflect any changes in your web application's network requests.

3. **Cookie Management**: For security reasons, only include necessary cookies in your `cookies.json` file and refresh them periodically.

4. **Input Variables**: Use the `--input_variables` option for dynamic data that may change between runs, such as API keys or user-specific information.

5. **Code Generation**: Use the `--generate-code` flag when you want Integuru to produce the full integration code for your use case.

By following this guide, you'll be well-equipped to configure Integuru for a wide range of web automation and integration tasks.

  