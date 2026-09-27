# Connect Codex to Wahlu

Codex CLI, the IDE extension and the Codex desktop app share one MCP configuration, so you only set Wahlu up once.

## Local server with an API key (works today)

1. In the Wahlu app, open **Settings → API Keys** in your workspace and create a key. Give it only the permissions and brands it needs.
2. Add the server from a terminal:

   ```bash
   codex mcp add wahlu --env WAHLU_API_KEY=your-key -- npx -y @wahlu/mcp-server
   ```

3. Restart Codex and check the server with `codex mcp list` or `/mcp`.

This runs Wahlu's MCP server on your computer with Node.js. It includes `upload_media_from_file`, so Codex can upload images and videos from your disk. See the [Codex MCP guide](https://learn.chatgpt.com/docs/extend/mcp).

Keep the key out of files you commit. To revoke it, delete it under **Settings → API Keys**.

## Hosted server with sign-in

Codex can also add remote Streamable HTTP servers:

```bash
codex mcp add wahlu --url https://mcp.wahlu.com/mcp
codex mcp login wahlu
```

Wahlu identifies apps with a Client ID Metadata Document and does not support dynamic client registration. If Codex reports that registration isn't supported, remove the entry with `codex mcp remove wahlu` and use the local server above.

## Check it works

Ask Codex: "Call Wahlu's get_context and tell me which brands and permissions you have." It only reads.
