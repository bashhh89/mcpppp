# VS Code Teammate Brief — MCP setup (Docmost + AnythingLLM)

1) **Prerequisites**
   - Ensure the **GitHub Copilot Chat** extension is installed in VS Code (not just Copilot).
   - Docker must be running on EasyPanel so you can locate the AnythingLLM container.

2) **API Key**
   You already have your AnythingLLM API key:
   `ETTJW5V-A5NMCBA-JDVSAEG-649PF7T`

3) **Locate Your AnythingLLM Container**
   In your EasyPanel terminal, run:

   ```bash
   docker ps
   ```

   Identify the container name or ID for AnythingLLM (it’ll be in your EasyPanel “folder storage” group).

4) **Install MCP Server**
   Exec into your AnythingLLM container (replace CONTAINER with its name/ID):

   ```bash
   docker exec -it CONTAINER bash
   npm install -g @raqueljezweb/anythingllm-mcp-server
   exit
   ```

5) **VS Code MCP Config**
   Create or replace `.vscode/mcp.json` in your workspace with:

   ```json
   {
     "inputs": [
       {
         "type": "promptString",
         "id": "anythingllm-api-key",
         "description": "AnythingLLM API Key",
         "password": true
       }
     ],
     "servers": {
       "docmost": {
         "type": "http",
         "url": "https://ahmad-docmost-web.lb2esz.easypanel.host/api",
         "headers": {}
       },
       "anythingllm": {
         "type": "stdio",
         "command": "anythingllm-mcp-server",
         "args": [],
         "env": {
           "ANYTHINGLLM_BASE_URL": "https://chat.qandu.me",
           "ANYTHINGLLM_API_KEY": "${input:anythingllm-api-key}",
           "MCP_DEBUG": "true"
         }
       }
     }
   }
   ```

6) **Start & Test in VS Code**
   - Open **Command Palette** → “GitHub Copilot Chat: Start MCP Servers” → paste your API key.
   - In Copilot Chat pane (`Ctrl+Alt+I`), test:
     - `@docmost create page "MCP Test"`
     - `@anythingllm list workspaces`

7) **Reference**
   - AnythingLLM MCP docs: see the “MCP Compatibility” section at https://docs.anythingllm.com/mcp-compatibility/overview

That covers Docker, EasyPanel, Copilot Chat, your API key, and the MCP setup. Let me know if anything needs tweaking.

---

• Docmost API docs: https://ahmad-docmost-web.lb2esz.easypanel.host/api

• For issues, ping Ahmad on Slack (or email basheer@qandu.me)
