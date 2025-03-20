# Sequential Thinking MCP Server
[![smithery badge](https://smithery.ai/badge/@smithery-ai/server-sequential-thinking)](https://smithery.ai/server/@smithery-ai/server-sequential-thinking)

An MCP server implementation that provides a tool for dynamic and reflective problem-solving through a structured thinking process.

## Features

- Break down complex problems into manageable steps
- Revise and refine thoughts as understanding deepens
- Branch into alternative paths of reasoning
- Adjust the total number of thoughts dynamically
- Generate and verify solution hypotheses
- HTTP server support for easy deployment

## Tool

### sequential_thinking

Facilitates a detailed, step-by-step thinking process for problem-solving and analysis.

**Inputs:**
- `thought` (string): The current thinking step
- `nextThoughtNeeded` (boolean): Whether another thought step is needed
- `thoughtNumber` (integer): Current thought number
- `totalThoughts` (integer): Estimated total thoughts needed
- `isRevision` (boolean, optional): Whether this revises previous thinking
- `revisesThought` (integer, optional): Which thought is being reconsidered
- `branchFromThought` (integer, optional): Branching point thought number
- `branchId` (string, optional): Branch identifier
- `needsMoreThoughts` (boolean, optional): If more thoughts are needed

## Usage

The Sequential Thinking tool is designed for:
- Breaking down complex problems into steps
- Planning and design with room for revision
- Analysis that might need course correction
- Problems where the full scope might not be clear initially
- Tasks that need to maintain context over multiple steps
- Situations where irrelevant information needs to be filtered out

## Configuration

### Command Line Options

The server supports the following command line options:

- `--transport, -t`: Transport type (stdio or http, default: http)
- `--port, -p`: HTTP port to listen on (default: 3000)
- `--host, -h`: Host to bind to (default: 0.0.0.0)
- `--help, -?`: Show help

### Using with HTTP

You can test the HTTP server with the following curl commands:

```bash
# Health check
curl http://localhost:3000/health

# List available tools
curl -X POST http://localhost:3000/mcp/v1/tools

# Call the sequential_thinking tool
curl -X POST http://localhost:3000/mcp/v1/tools/sequentialthinking \
  -H "Content-Type: application/json" \
  -d '{
    "thought": "Initial problem analysis",
    "nextThoughtNeeded": true,
    "thoughtNumber": 1,
    "totalThoughts": 5
  }'
```

### Usage with Claude Desktop

Add this to your `claude_desktop_config.json`:

#### npx

```json
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-sequential-thinking"
      ]
    }
  }
}
```

#### docker

```json
{
  "mcpServers": {
    "sequentialthinking": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "mcp/sequentialthinking"
      ]
    }
  }
}
```

## Building

Docker:

```bash
docker build -t mcp/sequentialthinking -f src/sequentialthinking/Dockerfile .
```

## Running as HTTP Server

This fork has been modified to run as an HTTP server by default, making it easier to deploy to cloud environments.

```bash
# Run via npm
npm start

# Run with custom port
npm start -- --port 8080

# Run with stdio transport (original behavior)
npm start -- --transport stdio
```

## Deploying to Coolify

To deploy this server to Coolify:

1. Fork this repository
2. In Coolify, create a new service using this repository
3. Set the Dockerfile path to `src/sequentialthinking/Dockerfile`
4. Set the build context to `/` (root directory)
5. Deploy the application

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.
