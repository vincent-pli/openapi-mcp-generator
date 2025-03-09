# OpenAPI to MCP

A command-line tool that generates Model Context Protocol (MCP) server code from OpenAPI specifications. This tool helps you quickly create an MCP server that acts as a bridge between LLMs (Large Language Models) and your API.

## Features

- **Automatic Tool Generation**: Converts each API endpoint in your OpenAPI spec into an MCP tool
- **Multiple Transport Options**: Supports stdio, WebSocket, and HTTP transport methods
- **Complete Project Setup**: Generates all necessary files to run an MCP server
- **TypeScript Support**: Includes TypeScript definitions and configuration
- **Easy Configuration**: Simple environment-based configuration for the generated server

## Installation

```bash
# Clone this repository
git clone https://github.com/yourusername/openapi-to-mcp.git

# Navigate to the project directory
cd openapi-to-mcp

# Install dependencies
npm install

# Make the script executable
chmod +x index.js

# Optionally, install globally
npm install -g .
```

## Usage

Generate an MCP server from an OpenAPI specification:

```bash
./index.js --openapi path/to/openapi.json --output ./my-mcp-server
```

Or if installed globally:

```bash
openapi-to-mcp --openapi path/to/openapi.json --output ./my-mcp-server
```

### Command Line Options

| Option | Alias | Description | Default |
|--------|-------|-------------|---------|
| `--openapi` | `-o` | Path or URL to OpenAPI specification | (required) |
| `--output` | `-d` | Output directory for generated files | `./mcp-server` |
| `--name` | `-n` | Name for the MCP server | `openapi-mcp-server` |
| `--version` | `-v` | Version for the MCP server | `1.0.0` |
| `--transport` | `-t` | Transport mechanism (stdio, websocket, http) | `stdio` |
| `--port` | `-p` | Port for websocket or HTTP server | `3000` |
| `--help` | `-h` | Show help information | |

### Examples

Generate from a local OpenAPI file:

```bash
./index.js --openapi ./specs/petstore.json --output ./petstore-mcp
```

Generate from a remote OpenAPI URL:

```bash
./index.js --openapi https://petstore3.swagger.io/api/v3/openapi.json --output ./petstore-mcp
```

Specify a WebSocket transport:

```bash
./index.js --openapi ./specs/petstore.json --transport websocket --port 8080
```

## Generated Files

The tool generates the following files in the output directory:

- `server.js` - The main MCP server implementation
- `package.json` - Dependencies and scripts
- `README.md` - Documentation for the generated server
- `.env.example` - Template for environment variables
- `types.d.ts` - TypeScript type definitions for the API
- `tsconfig.json` - TypeScript configuration

## Using the Generated Server

After generating your MCP server:

1. Navigate to the generated directory:
   ```bash
   cd my-mcp-server
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create an environment file:
   ```bash
   cp .env.example .env
   ```

4. Edit `.env` to set your API base URL and any required headers:
   ```
   API_BASE_URL=https://api.example.com
   API_HEADERS=Authorization:Bearer your-token-here
   ```

5. Start the server:
   ```bash
   npm start
   ```

## Requirements

- Node.js 16.x or higher
- npm 7.x or higher

## License

MIT