

  # How Integuru Performs Integrations

Integuru uses an intelligent process to analyze web interactions and build automated integrations. Here's an overview of how it works:

## 1. Capturing Web Activity

Integuru starts by examining a HAR (HTTP Archive) file. This file contains a detailed record of all the web requests and responses that occur when you perform an action on a website, like logging in or submitting a form.

## 2. Identifying the Key Action

The system first identifies the specific URL responsible for the main action you want to automate. It does this by analyzing the list of URLs in the HAR file and determining which one matches your intended task.

## 3. Analyzing Dynamic Parts

Integuru then examines the details of the web requests related to your action. It looks for dynamic elements - pieces of data that change between different users or sessions. These could be things like:

- User IDs
- Session tokens 
- Timestamps

The system is smart enough to ignore common elements that don't need special handling, like user agents or encoding information.

## 4. Building a Graph Representation

As Integuru analyzes the requests, it constructs a graph - think of it like a map of the integration. Each node in this graph represents a step in the process, such as:

- The main action request
- Requests for dynamic data
- Cookie information

The system connects these nodes to show how different parts of the integration depend on each other.

## 5. Simplifying the Integration

Integuru works to make the integration as simple as possible. It looks for the most straightforward way to obtain necessary data, reducing the number of steps required.

## 6. Handling Special Cases

The system can recognize and handle special situations, like JavaScript files or HTML responses, ensuring it focuses on the essential parts of the integration.

## 7. Generating the Final Integration

Once Integuru has mapped out all the necessary steps and data, it can generate code to automate the entire process. This code handles retrieving dynamic data, making requests in the correct order, and completing the desired action.

By breaking down complex web interactions into a structured graph, Integuru creates reliable, efficient integrations that can adapt to changing session data and user-specific information.

  