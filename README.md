# mcp-local-spec

Goals
##

The goal of this specification is to allow a standard way to list and configure MCP Servers on a local machine.

Specification for the local [MCP](https://docs.anthropic.com/en/docs/agents-and-tools/mcp) server discovery

There are many tools on a machine that can use MCP Servers to augment the AI. There is a non-standard approach to configuring the MCP Server per each tool. We mean the tools like
- IntelliJ IDEA
- Anthropic Claude
- OpenAI ChatGPT
- Cursor
- Windsurf
- <PR to add you>

# Supported in the following tools
- 

# Specification

Create a file per each MCP server in the `~/.mcp` folder (`%USER_HOME%` on Windows).
The file is a Markdown file that explains the LLM about your MCP server.
For example:

```
~/.mcp/my-mcp-server-tool-id.md
```

Create the following text inside:

```md
# MCP Server: Production

## Basic Information
- **Name**: Production Jonnyzzz MCP Server
- **ID**: prod-mcp-01
- **Version**: 3.2.1
- **URL**: https://mcp-prod.jonnyzzz.com:8443
- **API Version**: v2

## Authentication
- **Type**: oauth2
- **Client ID**: client_123
- **Token Endpoint**: https://auth.example.com/token

## Capabilities
- compute
- storage
- networking

## Regions
### us-east
- us-east-1a
- us-east-1b

### eu-west
- eu-west-1a
- eu-west-1b

## Health Check
- **Endpoint**: /health
- **Interval**: 60 seconds

## Metadata
- **Environment**: production
- **Owner**: platform-team
- **Priority**: high
```


# How to use the Spec?

An MCP client uses the LLM (Claude, o1) to extract the necessary information from each of the available MCP servers, which are discovered in the files under the `~/.mcp` folder. 
It is up to the LLM and the client to decide if to use a specific LLM, ask for credentials, and so on. 
