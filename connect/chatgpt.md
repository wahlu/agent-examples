# Connect ChatGPT to Wahlu

ChatGPT connects to Wahlu's hosted MCP server, `https://mcp.wahlu.com/mcp`, and signs you in to Wahlu with OAuth. Never paste a Wahlu API key into ChatGPT.

Wahlu's listing in the ChatGPT app directory is coming soon. Until then, add it with developer mode on the ChatGPT website. The ChatGPT desktop apps don't have this setting.

1. On [chatgpt.com](https://chatgpt.com), open **Settings → Security and login** and turn on **Developer mode**.
2. Go to [chatgpt.com/plugins](https://chatgpt.com/plugins) and select the **+** button.
3. Name it `Wahlu`, paste `https://mcp.wahlu.com/mcp` as the MCP server URL and choose **OAuth** if asked how to authenticate.
4. Create the connection and sign in to Wahlu when asked: confirm the account, choose a workspace and brands, check the permissions, then select **Allow access**.
5. Start a new conversation and add Wahlu from the tools menu.

Whether developer mode is available depends on your ChatGPT plan and workspace settings; a workspace admin may need to allow it. See OpenAI's [connection guide](https://developers.openai.com/plugins/deploy/connect-chatgpt).

## What you get in ChatGPT

Alongside text answers, Wahlu shows compact cards for your connected accounts, media library, a post you've drafted, your calendar and a post's status.

## Check it works

Ask: "Use Wahlu to show which brands you can see, then show the latest media for the brand I pick." Both steps only read.

To disconnect, remove the grant at [auth.wahlu.com/connections](https://auth.wahlu.com/connections), then remove the app in ChatGPT.
