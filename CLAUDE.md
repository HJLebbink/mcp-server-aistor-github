# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the documentation and configuration repository for the AIStor MCP (Model Context Protocol) server. The actual server implementation is containerized and distributed as a Docker/Podman image at `quay.io/minio/aistor/mcp-server-aistor:latest`.

Note: The server implementations exist in separate closed-source repositories (`mcp-server-aistor-py` and `mcp-server-aistor-go`). This repository serves as the public-facing documentation and configuration guide.

## Repository Structure

- `README.md` - Main documentation for configuring and using the MCP server
- `glama.json` - MCP server registration file for Glama.ai

## Development Commands

Since this is primarily a documentation repository, there are no build or test commands. Common tasks include:

```bash
# Update documentation
git add README.md
git commit -m "Update documentation"
git push origin main

# Check container image (requires Docker/Podman)
podman pull quay.io/minio/aistor/mcp-server-aistor:latest
podman images | grep mcp-server-aistor
```

## Working with the MCP Server

The MCP server supports two transport modes:

1. **STDIO** - For Claude Desktop and similar clients
2. **StreamableHTTP** - For web-based clients (use `--http` flag)

### Configuration Flags

- `--allow-write` - Enable write operations (create buckets, upload objects)
- `--allow-delete` - Enable delete operations (remove objects and buckets)
- `--allow-admin` - Enable admin functions (cluster info, health status)
- `--allowed-directories` - Specify local directories accessible to the server
- `--max-keys` - Limit number of objects listed (default: 1000)
- `--http` - Enable StreamableHTTP transport
- `--http-port` - Specify HTTP port for StreamableHTTP

### Environment Variables

Required for connecting to MinIO/AIStor:
- `MINIO_ENDPOINT` - Server endpoint URL
- `MINIO_ACCESS_KEY` - Access key credentials
- `MINIO_SECRET_KEY` - Secret key credentials
- `MINIO_USE_SSL` - Enable/disable SSL (true/false)

## Documentation Updates

When updating the README:
1. Test configurations with actual MinIO/AIStor instances when possible
2. Keep examples concrete and working (use MinIO Playground for public examples)
3. Update the "Updates" section with dated entries for significant changes
4. Maintain the tool descriptions list to match the actual server capabilities

## MCP Protocol Version

The server currently supports MCP version 2025-03-26. Updates to the protocol version should be documented in the README's "Updates" section.