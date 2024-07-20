## Concisely

This repository contains a FastAPI application that provides a RESTful API for summarizing text using LangChain's summarization refined chain powered by OpenAI. 

### Features:

* **Summarization API:** A POST endpoint `/summarize` accepts text as input and returns a concise summary.
* **Environment Variables:** Configurable settings like OpenAI API key, base URL, model name, and maximum tokens are managed via environment variables for easy customization.
* **LangChain & OpenAI:** Leverages LangChain for chain composition and OpenAI's powerful language models for text generation.

### Requirements:

* Python 3.7+
* OpenAI API Key (obtain one from [https://platform.openai.com/](https://platform.openai.com/))
* Required packages:
    ```bash
    pip install fastapi uvicorn python-dotenv langchain openai litellm
    ```

### Setup:

1. **Create a `.env` file** in the root directory of the project and add the following lines, replacing the placeholders:
    ```
    OPENAI_API_KEY=your_openai_api_key_here
    OPENAI_API_BASE=https://api.openai.com/v1
    OPENAI_MODEL=text-davinci-003
    MAX_TOKENS=100
    ```

2. **Run the application:**
    ```bash
    uvicorn main:app --reload
    ```

### Usage:

* **Send a POST request to `http://localhost:8000/summarize` with a JSON payload containing the text to summarize:**
    ```json
    {
        "text": "Your long text to summarize goes here..."
    }
    ```

* **The API will return a JSON response containing the generated summary:**
    ```json
    {
        "summary": "The generated summary will be here..."
    }
    ```

### Example:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"text": "This is a long text that I would like to have summarized. ..."}' http://localhost:8000/summarize
```

### Notes:

* The application uses the `refine` chain type, suitable for longer texts.
* The `MAX_TOKENS` environment variable controls the maximum length of the generated summary.
* OpenAI API usage is subject to their rate limits and pricing.

### Using LiteLLM for Other LLMs

To use other LLMs like Gemini or Claude, you can utilize the LiteLLM OpenAI Proxy Server:

1. **Install LiteLLM:**
    ```bash
    pip install litellm
    ```

2. **Configure LiteLLM:**
    * **Start the LiteLLM server:**
        ```bash
        litellm-server --model-name openai/gpt-4 --api-key your_openai_api_key
        ```
        (Replace `openai/gpt-4` with the desired model name, e.g., `anthropic/claude-2` for Claude).

    * **Update your `.env` file:**
        ```
        OPENAI_API_KEY=your_litellm_api_key
        OPENAI_API_BASE=http://localhost:8000
        OPENAI_MODEL=openai/gpt-4
        ```
        (Replace `your_litellm_api_key` with the LiteLLM server's API key, and `openai/gpt-4` with the actual model name).

3. **Run the FastAPI application:**
    ```bash
    uvicorn main:app --reload
    ```

Now, your FastAPI application will use the specified LLM through LiteLLM's proxy.

### Contributions:

Contributions are welcome! Feel free to open issues or submit pull requests.

### License:

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
