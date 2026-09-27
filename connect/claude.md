# Connect Claude to Wahlu

Wahlu's hosted MCP server is `https://mcp.wahlu.com/mcp`. It uses Streamable HTTP and signs you in to Wahlu in your browser with OAuth, so you never paste an API key into Claude.

## Claude (claude.ai and Claude Desktop)

1. Open **Customize → Connectors**.
2. Click **+**, then **Add custom connector**.
3. Name it `Wahlu` and paste `https://mcp.wahlu.com/mcp` as the remote MCP server URL. Leave **Advanced settings** empty.
4. Click **Add**, then **Connect**, and sign in to Wahlu.
5. In a chat, turn Wahlu on from the **+** button under **Connectors**.

On Team and Enterprise plans, an organisation owner first adds the connector in **Organization settings → Connectors** (**Add**, then **Custom → Web**). Members then click **Connect** next to it. Free plans allow one custom connector. See Anthropic's [custom connector guide](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).

Wahlu's listing in the Claude directory is coming soon; until then, add it as a custom connector.

## Claude Code

### With the plugin (recommended)

The plugin adds the Wahlu MCP server and four skills: `plan-a-week`, `idea-to-scheduled-post`, `repurpose-video` and `weekly-recap`.

```text
/plugin marketplace add wahlu/agent-examples
/plugin install wahlu@wahlu
```

Then run `/mcp`, select **wahlu** and sign in to Wahlu in the browser that opens.

### Just the MCP server

```bash
claude mcp add --transport http wahlu https://mcp.wahlu.com/mcp
```

Add `--scope user` before `wahlu` to use it in every project. Run `/mcp`, select **wahlu** and sign in. See the [Claude Code MCP docs](https://code.claude.com/docs/en/mcp).

### Local server (for files on your computer)

The hosted server can't read files on your computer. To upload local files, run Wahlu's local MCP server with an API key from **Settings → API Keys** in the Wahlu app:

```bash
claude mcp add --scope user wahlu-local --env WAHLU_API_KEY=your-key -- npx -y @wahlu/mcp-server
```

It has the same tools, plus `upload_media_from_file`.

## What you'll see when you sign in

1. **Continue as:** confirm your Wahlu account.
2. **Choose a workspace** and the **brands** Claude may use.
3. **Permissions:** untick anything you don't want to allow. Permissions that change data or publish are labelled.
4. Select **Allow access**.

## Check it works

Ask Claude: "Use Wahlu to tell me which workspace, brands and permissions you can see." It should call `get_context`, which only reads.

To disconnect, remove the grant at [auth.wahlu.com/connections](https://auth.wahlu.com/connections), then remove the connector from Claude.
