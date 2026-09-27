# Connect Gemini CLI to Wahlu

## Local server with an API key (works today)

1. In the Wahlu app, open **Settings → API Keys** in your workspace and create a key with only the permissions and brands you need.
2. Export it in your shell profile so it stays out of config files:

   ```bash
   export WAHLU_API_KEY=your-key
   ```

3. Add Wahlu to `~/.gemini/settings.json` (every project) or `.gemini/settings.json` (one project):

   ```json
   {
     "mcpServers": {
       "wahlu": {
         "command": "npx",
         "args": ["-y", "@wahlu/mcp-server"],
         "env": {
           "WAHLU_API_KEY": "$WAHLU_API_KEY"
         }
       }
     }
   }
   ```

4. Start `gemini` and run `/mcp` to check that **wahlu** is connected and lists its tools.

See the [Gemini CLI MCP docs](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md).

## Hosted server with sign-in

Gemini CLI can connect to remote servers with `httpUrl`:

```json
{
  "mcpServers": {
    "wahlu": {
      "httpUrl": "https://mcp.wahlu.com/mcp"
    }
  }
}
```

Then run `/mcp auth wahlu` to sign in. Wahlu doesn't support dynamic client registration, so if sign-in fails with a registration error, use the local server above.

## Check it works

Ask: "Use Wahlu's get_context and tell me which brands and permissions you have." It only reads.
