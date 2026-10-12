# ORANO Personal Context MCP

The `orano` MCP server gives read-only access to the user's own ORANO library. Use it when the user asks about their saved projects, handoffs, library items or memory facts.

Tools:
- `list_projects`: list the user's projects.
- `get_project`: details for one project.
- `get_project_context`: project context to start coding with.
- `get_pending_handoffs`: handoffs waiting for the user.
- `search_library`: search saved library items.
- `get_memory_facts`: curated memory facts about the user.

Rules: the server is read-only (scope `orano:read`) and each key sees only its owner's data. Never print or store the API key. Docs: https://oranoai.com/mcp
