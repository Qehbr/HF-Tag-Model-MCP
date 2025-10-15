This project provides an **AI-powered bot that automatically tags Hugging Face Hub repositories**. It works by listening to discussion comments. When it detects keywords like "pytorch" or "text-generation", it uses an AI agent to open a Pull Request that adds the relevant tag to the model card.

---

### ## Project Files

* **`server.py`**: The main application. It's a **FastAPI** server that receives webhooks from the Hugging Face Hub and hosts a **Gradio** dashboard for testing and monitoring.
* **`mcp_server.py`**: A backend **MCP server** that provides the agent with tools to interact with the Hugging Face Hub, such as `get_current_tags` and `add_new_tag`. This server is started automatically by `server.py`.
* **`pyproject.toml`**: Defines the project's Python dependencies.
* **`Dockerfile`**: Contains instructions to package the entire application into a portable **Docker container**.

---

### ## How to Use It

1.  **Install Dependencies**:
    Open your terminal and run:
    ```bash
    uv sync
    ```

2.  **Set Up Environment**:
    Create a `.env` file and add your Hugging Face token and a webhook secret.
    ```env
    HF_TOKEN="hf_..."
    WEBHOOK_SECRET="a-secure-random-string"
    ```

3.  **Run the Server**:
    The main server starts the MCP server automatically.
    ```bash
    python server.py
    ```
    You can access the Gradio dashboard at `http://localhost:7860/gradio`.

4.  **Configure the Webhook**:
    Go to your repository's settings on the Hugging Face Hub and add a webhook. Point it to your server's `/webhook` endpoint (use a tool like `ngrok` or `cloudflared` if running locally) and set the same secret you defined in your `.env` file.

The bot is now live. When you create a new comment in a discussion on your repository that mentions a recognized tag, it will automatically process it.