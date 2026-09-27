# Connect Cursor to Wahlu

Cursor signs in to remote MCP servers with dynamic client registration or a fixed client ID. Wahlu's hosted server uses Client ID Metadata Documents instead, so for now Cursor connects through Wahlu's **local** MCP server, which runs on your computer with Node.js and a Wahlu API key.

1. In the Wahlu app, open **Settings → API Keys** in your workspace and create a key with only the permissions and brands you need.
2. Add this to `~/.cursor/mcp.json` (every project) or `.cursor/mcp.json` (one project):

   ```json
   {
     "mcpServers": {
       "wahlu": {
         "command": "npx",
         "args": ["-y", "@wahlu/mcp-server"],
         "env": {
           "WAHLU_API_KEY": "your-key"
         }
       }
     }
   }
   ```

3. Open **Cursor Settings → MCP** and check that **wahlu** is enabled and lists its tools.

Paste the key yourself and keep project-level config out of version control. See [Cursor's MCP docs](https://cursor.com/docs/context/mcp).

The local server has every hosted tool plus `upload_media_from_file`, so Cursor can upload images and videos from your project.

## Check it works

In Agent mode, ask: "Use Wahlu's get_context to show which brands and permissions this key has." It only reads.
