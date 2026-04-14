# VS Code MCP Configuration 

This directory contains the Model Context Protocol (MCP) server configuration for integrating GitHub Copilot with enterprise tools.

## Overview

The `mcp.json` file configures four MCP servers that enable AI-assisted interactions with:

| Server | Purpose | Docker Image |
|--------|---------|--------------|
| **GitHub Enterprise** | Repository management, PRs, issues | `ghcr.io/github/github-mcp-server` |
| **Jenkins** | Build status, job management, logs | `@mister-good-deal/host-mcp-jenkins` |
| **Confluence** | Documentation search and retrieval | `ghcr.io/sooperset/mcp-atlassian` |
| **Jira** | Issue tracking, sprint management | `ghcr.io/sooperset/mcp-atlassian` |

## Prerequisites

- **Docker** must be installed and running
- **VS Code** with GitHub Copilot Chat extension
- Personal access tokens for each service (see [Token Setup](#token-setup))

## Token Setup

You'll be prompted for tokens when the MCP servers are first used. Generate tokens from:

### GitHub Enterprise Token
1. Go to https://URL_GITHUB_URL/settings/tokens
2. Create a new token with scopes: `repo`, `read:org`, `read:user`

### Jenkins API Token
1. Go to https://YOUR_JENKINS_URL/user/YOUR_USER/configure
2. Under "API Token", click "Add new Token"

### Confluence Token
1. Go to https://YOUR_CONFLUENCE_URL/plugins/personalaccesstokens/usertokens.action
2. Create a new personal access token

### Jira Token
1. Go to https://YOUR_JIRA_URL/plugins/personalaccesstokens/usertokens.action
2. Create a new personal access token

## Service Endpoints

| Service | URL |
|---------|-----|
| GitHub Enterprise | YOUR_GITHUB_URL |
| Jenkins | URL_JENKINS_URL |
| Confluence | YOUR_CONFLUENCE_URL |
| Jira | YOUR_JIRA_URL |

## Usage

Once configured, you can ask GitHub Copilot to:

- **GitHub**: "Show recent PRs", "Create a branch", "Search code in repo"
- **Jenkins**: "What's the status of the develop build?", "Show build logs"
- **Confluence**: "Find documentation about [topic]", "Search YOUR space"
- **Jira**: "Show my open issues", "Get sprint details"

## Troubleshooting

### Docker not running
Ensure Docker Desktop is started before using MCP servers.

### Token expired
Re-enter tokens when prompted, or restart VS Code to trigger re-authentication.

### Server not responding
Check Docker logs:
```bash
docker logs $(docker ps -q --filter ancestor=ghcr.io/github/github-mcp-server)
```

## Security Notes

- Tokens are entered securely via VS Code's `promptString` with `password: true`
- Tokens are not stored in the configuration file
- Each session requires re-entering tokens (by design for security)

## Related Resources

- [MCP Specification](https://modelcontextprotocol.io/)
- [GitHub MCP Server](https://github.com/github/github-mcp-server)
- [Atlassian MCP Server](https://github.com/sooperset/mcp-atlassian)
