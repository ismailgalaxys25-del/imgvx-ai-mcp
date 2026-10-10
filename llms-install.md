# Installing the ImgVX AI MCP server

ImgVX AI is a hosted, remote MCP server. There is nothing to clone, build or install, and it needs no API key, account or environment variables.

- URL: `https://imgvx.com/mcp`
- Transport: Streamable HTTP
- Authentication: none

## Cline

Add this entry to `cline_mcp_settings.json` under `mcpServers`:

```json
{
  "mcpServers": {
    "imgvx-ai": {
      "type": "streamableHttp",
      "url": "https://imgvx.com/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

## Check that it works

The server exposes three read-only tools:

- `find_image_tool`: give it a task such as "remove the background from a product photo" (and optionally `language`, a code like `es`) and it returns the matching ImgVX AI tool pages.
- `list_image_tools`: lists every tool, optionally filtered by category.
- `get_pricing`: what is free and what Pro and credit packs cost.

Calling `find_image_tool` with `{"task": "upscale a small image"}` should return a link to https://imgvx.com/image-upscaler/.
