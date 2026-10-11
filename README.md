# MagicWP plugin for Claude Code

> **Preview.** Signing in with your MagicWP account (OAuth) is being rolled out. Until it is live on `mcp.magicwp.io`, the plugin can't connect yet. This note goes away when it is.

Manage your [MagicWP](https://magicwp.io) WordPress sites from [Claude Code](https://code.claude.com): create sites, run updates, take and restore backups, check what's up and what needs attention, in plain words.

This repository holds **only the Claude Code plugin**: a marketplace file, the connection to MagicWP's hosted MCP server and a few skills. It does not contain the MCP server or any other MagicWP code.

## Install

```bash
claude plugin marketplace add magicwpio/mcp
claude plugin install magicwp@magicwp
```

Start Claude Code and run `/mcp`. Pick **magicwp** and choose **Authenticate**. Your browser opens MagicWP: sign in, pick the workspace, choose **Full access** or **Read-only**, and approve. That's it: no API token to copy, and nothing secret is stored in this plugin.

Your MagicWP plan needs MCP access, and connecting an app needs two-factor authentication on your account.

## What you get

- **The MagicWP MCP server** at `https://mcp.magicwp.io/mcp`: about 60 tools for sites, backups, updates, staging, domains, caching, PHP, Cloudflare, email and more. A read-only connection only sees the tools that look.
- **Skills** Claude uses when they fit:
  - `create-site`: creates a site and waits for its build to finish before calling it ready.
  - `destructive-actions`: what to check and say before deleting, restoring, resetting or overwriting anything.
  - `health-report`: a read-only report across all your sites: up or down, updates, backups, versions, disk.

Ask things like:

- "Create a site called Bakery in Frankfurt and tell me when it's ready."
- "Which of my sites need updates or haven't been backed up this week?"
- "Restore shop.example.com to yesterday's backup."

## Safety

- Destructive actions need you to type the site's domain. Claude can't fill it in for you.
- Claude can do no more than your role in the workspace allows.
- Everything it does shows in your MagicWP Activity log, marked "via MCP".
- Disconnect any time in the MagicWP dashboard under **MCP → Connected apps**. A connection that isn't used for 90 days ends by itself.

## Docs

- MCP documentation: https://docs.magicwp.io/mcp
- Using Claude or ChatGPT on the web instead: add `https://mcp.magicwp.io/mcp` as a custom connector. The docs show how.

## License

[MIT](LICENSE)
