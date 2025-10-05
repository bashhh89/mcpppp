```
1. Install GitHub Copilot Chat extension in VS Code.

2. In your EasyPanel terminal, find the AnythingLLM container and install its MCP server:
   docker ps
   docker exec -it <ANYTHINGLLM_CONTAINER> bash
   npm install -g @raqueljezweb/anythingllm-mcp-server
   exit

3. Add `.vscode/mcp.json` in your workspace with:
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

4. In VS Code: open Command Palette → "GitHub Copilot Chat: Start MCP Servers" → paste your AnythingLLM API key (`ETTJW5V-A5NMCBA-JDVSAEG-649PF7T`).

5. Verify in Copilot Chat:
   • `@docmost create page "MCP Test"`
   • `@anythingllm list workspaces"`
```