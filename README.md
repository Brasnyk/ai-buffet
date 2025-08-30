# AI Buffet

A veritable buffet of different AI models.

Meant to showcase the capabilities of our ai-bom tool by providing several examples of AI usages.

So far, the repo contains:

1. A simple chatbot app using the `anthropic` libary. Showcases our detection of model usage, even when the string literal is not passed directly.
2. An audio application used to generate melodies. Showcases our ability to detect transitive AI library dependencies via SCA.

--- 
#### Thomas F Nielson - Sr. Solutions Engineer @ Snyk 

###### *contributions: added configurations and tools for `mcp-scan` demo*

## About the Project

This guide provides the steps to set up and run `mcp-scan` within your local environment to detect and monitor Agentic related Vulnerabilties such as:
* Prompt Injection Attacks
* Tool Poisoning Attacks
* Toxic Flows


---

## Getting Started

### Prerequisites

* **Python 3.12+**: This project requires Python 3.12 or newer.
* **`uv`**: A fast Python package installer and resolver. You can install it using `pip`.

    ```bash
    pip install uv
    ```

### Installation and Setup

1.  **Clone the Repository**
    Start by cloning the `ai-buffet` repository and navigating into the correct directory.

    ```bash
    git clone https://github.com/Brasnyk/ai-buffet.git
    cd ai-buffet/
    ```

2.  **Add `mcp` to Your Project**
    Add `mcp` with the `cli` extra to your project's dependencies using `uv`.

    ```bash
    uv add "mcp[cli]"
    ```
3.  **Install Claude Desktop**
    * https://claude.ai/download
    
4.  **Run the Installation Script**
    Navigate into the `mcp` directory and install the server.

    ```bash
    cd mcp
    uv run mcp install server.py
    ```

---

## Usage

### Running the Scanner

The `uvx` command is used to execute the `mcp-scan` tool. `uvx` will find and run the tool without needing to install it globally.

* **Scan Command**: Use this command to perform a static scan all your installed servers for malicious tool descriptions and tools
.

    ```bash
    uvx mcp-scan@latest scan
    ```

* **Proxy Command**: Use this command to run the proxy to continuously monitors your MCP connections in real-time, and can restrict what agent systems can do over MCP.

    ```bash
    uvx mcp-scan@latest proxy
    ```

### Pairing with Snyk MCP in Cursor

To integrate with Snyk's MCP, configure your `mcp.json` file as follows.

```json
{
    "mcpServers": {
        "Snyk": {
            "command": "npx",
            "args": [
                "-y",
                "snyk@latest",
                "mcp",
                "-t",
                "stdio"
            ],
            "type": "stdio"
        },
        "DemoServer": {
            "command": "/Users/user/Library/Python/3.9/bin/uv", <- replace with your own
            "args": [
                "run",
                "--with",
                "mcp[cli]",
                "mcp",
                "run",
                "/Users/user/Folder/ai-buffet/mcp/server.py" <- replace with your own
            ],
            "type": "stdio"
        }
    }
}

DemoServer extracted from Claude Desktop mcp.json
```

Resources used to setup:
- https://pypi.org/project/mcp/#adding-mcp-to-your-python-project
- https://claude.ai/download (download Claude to desktop)
- https://github.com/invariantlabs-ai/mcp-injection-experiments?tab=readme-ov-file (base code used to create Tools and instructions)

Credits:
* https://invariantlabs.ai/
    * `mcp-scan`: https://github.com/invariantlabs-ai/mcp-scan
*  https://snyk.io/
    *  Snyk MCP Server: https://docs.snyk.io/integrations/developer-guardrails-for-agentic-workflows

