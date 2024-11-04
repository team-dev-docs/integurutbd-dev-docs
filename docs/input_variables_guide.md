

  # Using Input Variables with Integuru

Input variables allow you to parameterize your Integuru integrations, making them more flexible and reusable. This guide explains how to use input variables effectively with Integuru.

## What are Input Variables?

Input variables are dynamic values that you can pass to Integuru when running an integration. They allow you to customize the behavior of your integration without modifying the underlying code or configuration.

Common uses for input variables include:

- API keys or authentication tokens
- User IDs or account numbers  
- Date ranges or time periods
- Search terms or filter criteria
- Quantity or amount values

## Specifying Input Variables in the CLI

To use input variables with Integuru, you specify them when running the integration using the `--input_variables` option. The syntax is:

```
integuru --input_variables KEY1 VALUE1 --input_variables KEY2 VALUE2 ...
```

You can specify multiple input variables by repeating the `--input_variables` option.

For example:

```
integuru --prompt "Get recent orders" --input_variables user_id 12345 --input_variables date_from 2023-01-01
```

This passes two input variables:
- `user_id` with a value of `12345`
- `date_from` with a value of `2023-01-01`

## How Input Variables Affect the Integration Process

When you specify input variables, Integuru will:

1. Parse the variables and make them available to the integration agent.
2. Scan the integration steps (API requests, etc.) for places where the variables can be applied.
3. Substitute the variable values into the appropriate places in API requests, headers, etc.
4. Use the variables to customize the integration behavior as needed.

The integration agent (`IntegrationAgent` class) has logic to identify where input variables should be applied and handle the substitution automatically.

## Examples of Using Input Variables

Here are some common use cases for input variables:

### Authentication Tokens

```
integuru --prompt "Fetch user profile" --input_variables auth_token eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

This allows you to pass in a fresh authentication token for each run of the integration.

### Date Ranges

```
integuru --prompt "Get sales report" --input_variables start_date 2023-01-01 --input_variables end_date 2023-03-31
```

You can use this to generate reports for different time periods without modifying the integration code.

### User-specific Data

```
integuru --prompt "Retrieve order history" --input_variables customer_id CUST-1234
```

This enables you to run the same integration for different users by passing in their unique identifier.

### API Keys

```
integuru --prompt "Analyze sentiment of tweets" --input_variables twitter_api_key abc123...
```

You can securely pass API keys as input variables rather than hardcoding them in your integration.

## Best Practices

- Use descriptive names for your input variables to make their purpose clear.
- Consider which parts of your integration might need to vary between runs and make those configurable with input variables.
- For sensitive data like API keys or tokens, always use input variables rather than hardcoding the values.
- Document the required and optional input variables for your integrations so others can easily use them.

By leveraging input variables effectively, you can create more flexible and reusable integrations with Integuru.

  