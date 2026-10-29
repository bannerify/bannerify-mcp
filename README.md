# Bannerify MCP server

Bannerify runs a remote [Model Context Protocol](https://modelcontextprotocol.io) server at `https://api.bannerify.co/mcp`. Connect it to Claude, Cursor, VS Code, Codex or another MCP client, and the assistant can generate images and PDFs from your [Bannerify](https://bannerify.co) templates.

This repository holds the setup steps and the registry metadata. The server is hosted: there is nothing to install or run.

- Transport: Streamable HTTP
- Auth: OAuth with dynamic client registration. You sign in to Bannerify and choose a workspace on a consent page. You create no API key.
- Registry name: `io.github.bannerify/bannerify`

## Tools

| Tool | What it does |
| --- | --- |
| `list_templates` | Lists the templates in the workspace, optionally with the layers you can change |
| `get_template` | Reads one template and its layers |
| `get_project` | Reads the workspace: id, name, plan and creation date |
| `create_image` | Renders a template as PNG, JPEG or WebP |
| `create_pdf` | Renders a template as a PDF and returns a link to it |
| `create_image_from_shapes` | Composes a one-off image from shapes, with no template |

## Connect

### Claude Code

```bash
claude mcp add --transport http bannerify https://api.bannerify.co/mcp
```

Then run `/mcp` in Claude Code and sign in.

### Claude

Open **Customize > Connectors**, click **+ Add**, then **Add custom connector**. Enter `Bannerify` and `https://api.bannerify.co/mcp`.

### Cursor

`.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "bannerify": {
      "url": "https://api.bannerify.co/mcp"
    }
  }
}
```

### VS Code

`.vscode/mcp.json`:

```json
{
  "servers": {
    "bannerify": {
      "type": "http",
      "url": "https://api.bannerify.co/mcp"
    }
  }
}
```

### Codex

```bash
codex mcp add bannerify --url https://api.bannerify.co/mcp
codex mcp login bannerify
```

### Other clients

Enter `https://api.bannerify.co/mcp`, with the HTTP transport and OAuth sign-in.

## Example requests

- "List my Bannerify templates, with the layers of each one."
- "Create a PNG from my Lifecycle email template. Set the headline to Welcome back."
- "Create a PDF from my invoice template for Acme Studio."
- "Design a 1200 by 630 banner with a dark background and the text Launch week."

## Limits

A generation from an MCP client counts toward the same plan limits as the REST API. The free plan has 100 images a month. See [pricing](https://bannerify.co/pricing).

## Docs

- [Connect an MCP client](https://bannerify.co/docs/mcp/overview)
- [Generate files with MCP tools](https://bannerify.co/docs/mcp/tools)

## Support

an@bannerify.co
