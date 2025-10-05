# AnythingLLM → Docmost Integration Guide

1. Define Docmost as a tool inside AnythingLLM’s MCP servers
- Edit your container’s `plugins/anythingllm_mcp_servers.json` (or open **Agent Skills** page to auto-create it) and add:

```json
{
  "docmost": {
    "command": "http-server",           
    "args": ["--base", "/api", "--url", "https://ahmad-docmost-web.lb2esz.easypanel.host"],
    "env": {},
    "type": "http",
    "endpoints": {
      "list_pages": { "path": "/pages",        "method": "GET" },
      "get_page":   { "path": "/pages/{id}",   "method": "GET" },
      "create_page":{ "path": "/pages",        "method": "POST" },
      "update_page":{ "path": "/pages/{id}",   "method": "PATCH" }
    }
  }
}
```

2. Reload MCP servers in the AnythingLLM UI
- Open **Agent Skills** → click **Refresh** (no container restart needed).

3. Use `@docmost` commands in chat
```
@docmost.create_page
{"title":"AI Test","content":"Created via AnythingLLM"}
@docmost.list_pages
@docmost.get_page{"id":"123"}
```

4. Verify in Docmost
- Visit https://ahmad-docmost-web.lb2esz.easypanel.host → new page appears under **GENERAL** space.

5. Troubleshooting & Reference
- Docmost API endpoint: https://ahmad-docmost-web.lb2esz.easypanel.host/api
- For issues, ping Ahmad on Slack or email basheer@qandu.me

That’s it—AnythingLLM now speaks directly to your Docmost wiki via its public HTTP API.

[1](https://anythingllm.com/download)
[2](https://docs.anythingllm.com)
