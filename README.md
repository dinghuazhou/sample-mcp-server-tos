[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/dinghuazhou-sample-mcp-server-tos-badge.png)](https://mseep.ai/app/dinghuazhou-sample-mcp-server-tos)

# Sample TOS Model Context Protocol Server

An MCP server implementation for retrieving data from TOS.

## Features

### Tools

- **list_buckets**
    - Returns a list of all buckets owned by the authenticated sender of the request
- **list_objects**
    - Returns some or all (up to 1,000) of the objects in a bucket with each request
- **get_object**
    - Retrieves an object from volcengine TOS. In the GetObject request, specify the full key name for the object.
      General purpose buckets - Both the virtual-hosted-style requests and the path-style requests are supported

## Configuration

The server requires the following environment variables to be set:

- `VOLC_ACCESSKEY`: Required, The access key for the VolcEngine.
- `VOLC_SECRETKEY`: Required, The secret key for the VolcEngine.
- `REGION`: Required, The region for the TOS service.
- `TOS_ENDPOINT`: Required, The endpoint for the TOS service.
- `SECURITY_TOKEN`: Optional, The security token for the credential.
- `TOS_BUCKETS`: Optional, If you want to use a specific bucket, you need to set this.

You can set these environment variables in your shell.

### MCP Settings Configuration

To add this server to your MCP configuration, add the following to your MCP settings file:
```json
{
  "mcpServers": {
    "tos-mcp-server": {
      "command": "uv",
      "args": [
        "--directory",
        "/ABSOLUTE/PATH/TO/PARENT/FOLDER/src/mcp_server_tos",
        "run",
        "main.py"
      ]
    }
  }
}
```

or

```json
{
    "mcpServers": {
        "tls": {
            "command": "uvx",
            "args": [
                "--from",
                "git+https://github.com/volcengine/ai-app-lab#subdirectory=mcp/server/mcp_server_tos",
                "mcp-server-tos"
            ],
            "env": {
                "VOLC_ACCESSKEY": "your ak",
                "VOLC_SECRETKEY": "your sk",
                "REGION": "tos region",
                "TOS_ENDPOINT": "tos endpoint",
                "SECURITY_TOKEN": "your security token",
                "TOS_BUCKET": "your specific bucket"
            }
        }
    }
}
  ```

## Usage

### Running the Server

```bash
# Run the server with stdio transport (default)
tos-mcp-server
```

## License

This library is licensed under the MIT-0 License. See the LICENSE file.