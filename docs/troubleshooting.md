

  # Integuru Troubleshooting Guide

This guide addresses common issues users might encounter when using Integuru, focusing on HAR file processing, API interactions, and graph building. Follow the step-by-step solutions and learn how to interpret error messages.

## HAR File Processing Issues

### Problem: Invalid HAR File Format

**Symptoms:** 
- Error message: "Invalid HAR file format"
- Integuru fails to process the HAR file

**Solution:**
1. Ensure your HAR file is properly formatted JSON.
2. Open the HAR file in a text editor and check for any obvious syntax errors.
3. Validate the HAR file using an online JSON validator.
4. If the file was exported from a browser, try re-exporting it or use a different browser.

### Problem: Missing Required HAR Data

**Symptoms:**
- Error message: "Missing required data in HAR file"
- Incomplete or empty results after processing

**Solution:**
1. Verify that your HAR file contains the necessary `log` and `entries` sections.
2. Ensure each entry has `request` and `response` objects.
3. Check that the HAR file includes all network requests related to your integration.

## API Interaction Issues

### Problem: API Rate Limiting

**Symptoms:**
- Error message: "API rate limit exceeded"
- Integuru fails to complete API requests

**Solution:**
1. Implement exponential backoff in your API requests.
2. Reduce the frequency of API calls if possible.
3. Contact the API provider to request a higher rate limit if needed.

### Problem: Authentication Failures

**Symptoms:**
- Error message: "Authentication failed" or "Unauthorized"
- Integuru cannot access required API endpoints

**Solution:**
1. Double-check your API credentials (API key, client ID, client secret).
2. Ensure your authentication tokens are not expired.
3. Verify that your account has the necessary permissions for the API endpoints.
4. Check if the API requires additional headers or parameters for authentication.

## Graph Building Issues

### Problem: Missing Nodes or Edges

**Symptoms:**
- Incomplete graph visualization
- Missing connections between API calls

**Solution:**
1. Review the `DAGManager` logs to identify which nodes or edges are not being added.
2. Ensure that all relevant API calls are captured in your HAR file.
3. Check if the `dynamic_part_identifying_agent` is correctly identifying all dynamic parts.
4. Verify that the `find_curl_from_content` method is properly linking related API calls.

### Problem: Incorrect Node Types

**Symptoms:**
- Nodes are categorized incorrectly in the graph
- Unexpected behavior in graph analysis

**Solution:**
1. Review the node type assignment logic in the `IntegrationAgent` class.
2. Ensure that the `add_node` method in `DAGManager` is receiving the correct node type.
3. Check if the `url_to_curl` and `find_curl_from_content` methods are correctly identifying node types.

## Interpreting Error Messages

When encountering error messages, follow these general steps:

1. **Read the full error message:** Error messages often contain valuable information about the nature and location of the problem.

2. **Identify the error type:** Is it a file processing error, API error, or graph building error?

3. **Check related code:** Based on the error type, examine the relevant sections of code (e.g., `parse_har_file` for HAR processing errors).

4. **Review input data:** Verify that your input data (HAR files, API credentials) is correct and complete.

5. **Consult logs:** Check Integuru's log files for additional context and details about the error.

6. **Search documentation:** Look for similar issues in the Integuru documentation or community forums.

If you encounter persistent issues or errors not covered in this guide, please contact Integuru support with detailed information about your problem, including error messages, input data, and steps to reproduce the issue.

  