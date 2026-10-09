# ImgVX AI MCP Server

Official [Model Context Protocol](https://modelcontextprotocol.io) server for [ImgVX AI](https://imgvx.com), free image tools that run in the browser.
Connect it to Claude, ChatGPT, Cursor, VS Code, Windsurf, Zapier, Make, n8n or any other MCP client to:

- **Find the right image tool** for a job such as removing a background, upscaling, erasing an object, enhancing or colorizing a photo, compressing to a file size, resizing, cropping or converting HEIC, PNG, JPG, WebP or PDF.
- **Get a link in the user's language**: the most-used tools have pages in 40 languages.
- **List every tool** (87, in 8 categories) and **check pricing** (most tools are free; HD downloads use credits).

It is a hosted server: there is nothing to install, no sign-in and no API key. The tools never touch images.
They return a link, and the user edits the image in their own browser, where it is never uploaded.

| | |
|---|---|
| **URL** | `https://imgvx.com/mcp` |
| **Transport** | Streamable HTTP |
| **Authentication** | None |
| **Tools** | 3, all read-only |
| **Registry name** | `com.imgvx/imgvx-ai` |
| **Docs** | https://imgvx.com/mcp-server/ |

## Setup

### Claude

In Claude (web or desktop), open **Settings → Connectors → Add custom connector**, name it ImgVX AI and paste `https://imgvx.com/mcp`.

Claude Code:

```bash
claude mcp add --transport http imgvx-ai https://imgvx.com/mcp
```

### ChatGPT

With developer mode on (**Settings → Apps & Connectors → Advanced**), choose **Create**, name it ImgVX AI, paste `https://imgvx.com/mcp` and pick **No authentication**.

### Cursor

`~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "imgvx-ai": { "url": "https://imgvx.com/mcp" }
  }
}
```

### VS Code (GitHub Copilot)

`.vscode/mcp.json`:

```json
{
  "servers": {
    "imgvx-ai": { "type": "http", "url": "https://imgvx.com/mcp" }
  }
}
```

### Windsurf

`~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "imgvx-ai": { "serverUrl": "https://imgvx.com/mcp" }
  }
}
```

### Zapier, Make and n8n

- **Zapier:** add an **MCP Client** step, connect with the server URL, transport Streamable HTTP, no authentication.
- **Make:** add the **MCP Client** module, create a connection with the server URL and no authentication.
- **n8n:** give an **AI Agent** node the **MCP Client Tool**, set the endpoint to the server URL, transport HTTP Streamable, authentication None.

## Tools

| Tool | Input | Returns |
|---|---|---|
| `find_image_tool` | `task` (what to do to the image, in a few words), optional `language` (one of 40 language codes) | Up to five matching tools with what each does, its price and a link, in the user's language where a page exists |
| `list_image_tools` | optional `category` (`ai`, `compress-resize`, `adjust`, `effects`, `edit`, `convert`, `inspect`, `create`) | Every tool in that category with a short description and a link |
| `get_pricing` | none | What is free and what Pro and the credit packs cost |

## Example prompts

- "Remove the background from my product photo, which free tool should I use?"
- "I need to compress a passport photo to under 100 KB."
- "Make this old photo 4x bigger without it going blurry."
- "¿Cómo quito un objeto de una foto gratis?"

## Try it with curl

```bash
curl -s https://imgvx.com/mcp \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"find_image_tool","arguments":{"task":"remove background","language":"es"}}}'
```

## Privacy and support

The server receives only the tool inputs your app sends. It does not store them or link them to a person, and sets no cookies.
Images are never sent to it: every ImgVX AI tool runs in the user's browser. See the [privacy policy](https://imgvx.com/privacy/).

Questions or problems: support@imgvx.com or [imgvx.com/contact](https://imgvx.com/contact/).

## About this repository

This repository holds the public listing (`server.json` for the [MCP Registry](https://registry.modelcontextprotocol.io)) and setup docs
for the hosted ImgVX AI MCP server, under the MIT license. The server itself runs at imgvx.com.
