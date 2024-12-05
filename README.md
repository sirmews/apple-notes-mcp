# Apple Notes Model Context Protocol Server for Claude Desktop.

Read your local Apple Notes database and provide it to Claude Desktop.

Now Claude can search your most forgotten notes and know even more about you.

Noting could go wrong.

## Components

### Resources

The server implements the ability to read and write to your Apple Notes.

### Tools

The server provides multiple prompts:
- `get-all-notes`: Get all notes.
- `read-note`: Get full content of a specific note.
- `search-notes`: Search through notes.

### Missing Features:

- No handling of encrypted notes (ZISPASSWORDPROTECTED)
- No support for pinned notes filtering
- No handling of cloud sync status
- Missing attachment content retrieval
- No support for checklist status (ZHASCHECKLIST)
- No ability to create or edit notes

## Quickstart

### Install the server

Recommend using [uv](https://docs.astral.sh/uv/getting-started/installation/) to install the server locally for Claude.

```
uvx apple-notes-mcp
```
OR
```
uv pip install apple-notes-mcp
```

Add your config as described below.

#### Claude Desktop

On MacOS: `~/Library/Application\ Support/Claude/claude_desktop_config.json`
On Windows: `%APPDATA%/Claude/claude_desktop_config.json`

Note: You might need to use the direct path to `uv`. Use `which uv` to find the path.


__Development/Unpublished Servers Configuration__
  
```json
"mcpServers": {
  "apple-notes-mcp": {
    "command": "uv",
    "args": [
      "--directory",
      "{project_dir}",
      "run",
      "apple-notes-mcp"
    ]
  }
}
```


__Published Servers Configuration__
  
```json
"mcpServers": {
  "apple-notes-mcp": {
    "command": "uvx",
    "args": [
      "apple-notes-mcp"
    ]
  }
}
```


## Mac OS Disk Permissions

You'll need to grant Full Disk Access to the server. This is because the Apple Notes sqlite database is nested deep in the MacOS file system.

I may look at an AppleScript solution in the future if this annoys me further or if I want to start adding/appending to Apple Notes.

## Development

### Building and Publishing

To prepare the package for distribution:

1. Sync dependencies and update lockfile:
```bash
uv sync
```

2. Build package distributions:
```bash
uv build
```

This will create source and wheel distributions in the `dist/` directory.

3. Publish to PyPI:
```bash
uv publish
```

Note: You'll need to set PyPI credentials via environment variables or command flags:
- Token: `--token` or `UV_PUBLISH_TOKEN`
- Or username/password: `--username`/`UV_PUBLISH_USERNAME` and `--password`/`UV_PUBLISH_PASSWORD`

### Debugging

Since MCP servers run over stdio, debugging can be challenging. For the best debugging
experience, we strongly recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector).


You can launch the MCP Inspector via [`npm`](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) with this command:

```bash
npx @modelcontextprotocol/inspector uv --directory {project_dir} run apple-notes-mcp
```


Upon launching, the Inspector will display a URL that you can access in your browser to begin debugging.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Source Code

The source code is available on [GitHub](https://github.com/sirmews/apple-notes-mcp).

## Contributing

Send your ideas and feedback to me on [Bluesky](https://bsky.app/profile/perfectlycromulent.bsky.social) or by opening an issue.
