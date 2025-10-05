# Quick 5-step setup for VS Code developer

You need to connect two running services — Docmost (wiki) and AnythingLLM (chat AI) — so VS Code can issue AI-driven commands to the wiki.

1. Install the GitHub Copilot Chat extension in VS Code (not just Copilot).

2. Install the AnythingLLM MCP server inside the AnythingLLM Docker container on EasyPanel:

```bash
docker ps
docker exec -it <CONTAINER> bash
npm install -g @raqueljezweb/anythingllm-mcp-server
exit
```

3. Add `.vscode/mcp.json` to the project with:
- Docmost’s public API: `https://ahmad-docmost-web.lb2esz.easypanel.host/api`
- AnythingLLM’s MCP server CLI (`anythingllm-mcp-server`) and the API key

4. In VS Code run: “GitHub Copilot Chat: Start MCP Servers” and paste the AnythingLLM API key when prompted.

5. Test in Copilot Chat:
- `@docmost create page "Test"`
- `@anythingllm list workspaces`

Result: VS Code will be able to communicate with AnythingLLM and Docmost via MCP so you can manage the wiki and AI from one place.
