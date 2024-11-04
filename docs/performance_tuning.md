

  # Optimizing Integuru Performance

This guide provides recommendations for tuning Integuru to achieve optimal performance for your specific use case. We'll cover adjusting key parameters, selecting appropriate language models, and optimizing HAR file processing for large datasets.

## Adjusting Parameters

### max_steps

The `max_steps` parameter controls the maximum number of steps Integuru will take when executing a task. Adjusting this can significantly impact performance:

- Lower values (e.g. 5-10): Faster execution, but may not complete complex tasks
- Default (20): Balances speed and task completion for most use cases
- Higher values (30+): Allows for more complex tasks, but increases runtime

Recommendation: Start with the default of 20 and adjust based on task complexity and time constraints.

```python
# Example: Setting max_steps to 30
asyncio.run(call_agent(..., max_steps=30))
```

## Choosing the Right LLM Model

Integuru supports multiple language models, each with different capabilities and performance characteristics:

- `gpt-4o` (default): Best for complex reasoning and high-quality outputs
- `o1-preview`: Faster, suitable for simpler tasks or when speed is critical

To switch models:

```python
from integuru.util.LLM import LLMSingleton

# Use GPT-4
LLMSingleton.set_default_model("gpt-4o")

# Switch to o1-preview
LLMSingleton.switch_to_alternate_model()
```

Consider your specific requirements when choosing:

| Model | Strengths | Use Cases |
|-------|-----------|-----------|
| gpt-4o | Complex reasoning, high accuracy | Detailed analysis, code generation |
| o1-preview | Speed, efficiency | Quick responses, simple tasks |

## Optimizing HAR File Processing

For large HAR files, consider these optimization strategies:

1. **Filtering**: Adjust the `excluded_keywords` and `excluded_extensions` in `har_processing.py` to remove unnecessary requests:

```python
excluded_keywords = (
    "google", "taboola", "datadog", "sentry",
    # Add more keywords to exclude
)

excluded_extensions = (
    ".png", ".jpg", ".css",
    # Add more extensions to exclude
)
```

2. **Chunking**: For extremely large HAR files, implement a chunking mechanism to process the file in smaller segments:

```python
def process_har_in_chunks(har_file_path, chunk_size=1000):
    with open(har_file_path, 'r') as file:
        har_data = json.load(file)
    
    entries = har_data['log']['entries']
    for i in range(0, len(entries), chunk_size):
        chunk = entries[i:i+chunk_size]
        # Process this chunk
        process_entries(chunk)
```

3. **Parallel Processing**: Utilize multiprocessing to handle large datasets:

```python
from multiprocessing import Pool

def process_entries_parallel(har_file_path, num_processes=4):
    with open(har_file_path, 'r') as file:
        har_data = json.load(file)
    
    entries = har_data['log']['entries']
    with Pool(num_processes) as p:
        results = p.map(process_entry, entries)
```

## Performance Benchmarks

Here are some rough performance expectations for different configurations:

| Configuration | HAR File Size | Task Complexity | Approx. Runtime |
|---------------|---------------|-----------------|-----------------|
| Default (gpt-4o, max_steps=20) | < 1MB | Simple | 30-60 seconds |
| Default (gpt-4o, max_steps=20) | 1-10MB | Moderate | 2-5 minutes |
| Optimized (o1-preview, max_steps=10) | < 1MB | Simple | 15-30 seconds |
| Optimized (o1-preview, max_steps=10) | 1-10MB | Moderate | 1-3 minutes |
| Complex (gpt-4o, max_steps=50) | 10-100MB | High | 10-30 minutes |

Note: Actual performance may vary based on specific tasks, network conditions, and computational resources.

## Conclusion

Tuning Integuru for optimal performance involves balancing the `max_steps` parameter, selecting the appropriate language model, and optimizing HAR file processing. Start with the default configuration and adjust based on your specific needs and performance requirements. Monitor execution times and output quality to find the best configuration for your use case.

  