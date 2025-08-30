# AI Buffet

A veritable buffet of different AI models.

Meant to showcase the capabilities of our ai-bom tool by providing several examples of AI usages.

So far, the repo contains:

1. A simple chatbot app using the `anthropic` libary. Showcases our detection of model usage, even when the string literal is not passed directly.
2. An audio application used to generate melodies. Showcases our ability to detect transitive AI library dependencies via SCA.

--- 
TFN contribution

# MCP-SCAN

Prereqs:
- $ pip install uv

Get started:
1. $ git clone https://github.com/Brasnyk/ai-buffet.git
2. $ cd ai-buffet/
3. $ uv add "mcp[cli]"
4. $ cd mcp
5. $ uv run mcp install server.py
6. $ uvx mcp-scan@latest scan
7. $uvx mcp-scan@latest proxy

if paired with Snyk MCP in cursor:

mcp.json
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
    }
}

Resources used to setup:
- https://pypi.org/project/mcp/#adding-mcp-to-your-python-project
- https://claude.ai/download (download Claude to desktop)
- https://github.com/invariantlabs-ai/mcp-injection-experiments?tab=readme-ov-file (base code used to create Tools)

