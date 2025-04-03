# Discorevy local MCP Servers. Specification.

Version: 1.0.1

# Goals

This specification aims to allow _the standard way_ to list and configure [MCP](https://docs.anthropic.com/en/docs/agents-and-tools/mcp) Servers on a local machine.

Many tools already use MCP Servers to augment the LLMs. Currently, there is no standard approach to quickly registering an MCP Server. 

Here are the most popular MCP Clients:
- IntelliJ IDEA
- Anthropic Claude
- OpenAI ChatGPT
- Cursor
- Windsurf
- Warp
- **PR to add you**

# Supported in the following tools
- **PR if you support the spec**

# Specification

Create a file per each MCP server in the `~/.mcp` folder (`%USER_HOME%` on Windows).

The file is a Markdown file that explains an LLM (such as Claude or CharGPT) about your MCP Server details. The client uses LLM to transform your explanation into an actionable MCP Server.

The client is required to regularly refresh the information from the disc to discover new MCP Servers. 

This protocol does not resolve any security implications for MCP servers. That is still the responsibility of MCP Clients.


For example:

```
~/.mcp/my-mcp-server-tool-id.md
```

Create the following text inside:

```md
---
version: 1.0.1
---

# MCP Server: Production

Here, I describe what my MCP Server is doing and why the LLM would decide to include my server in a specific request, which is queried.

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

An MCP client uses the LLM (e.g., Claude, ChatGPT) to extract the necessary information from each of the available MCP server's markdown files, which are discovered in the files under the `~/.mcp` folder. 
It is up to the LLM and the client to decide if to use a specific LLM, ask for credentials, and so on. 
The client should refresh the files from the disk regularly.
