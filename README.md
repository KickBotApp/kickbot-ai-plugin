# KickBot plugin

Manage your Kick stream and KickBot account from chat. KickBot is a toolkit for
streamers on Kick, the live streaming platform. With this plugin, your AI
assistant can set up your chat bot (commands, timed messages, chat alerts, chat
filters), OBS alerts and overlays, custom widgets, text-to-speech, the AI chat
character, tipping, clips, and VODs.

## What is in this plugin

- `skills/`: eight Markdown skills that tell the assistant how to do common
  KickBot tasks well, such as channel setup and the chat bot.
- `.mcp.json` and `mcp.json`: the address of the KickBot MCP server,
  `https://kickbot.com/api/v1/mcp`.
- Manifests for Claude (`.claude-plugin/`) and Cursor (`.cursor-plugin/`).

The plugin has no code, scripts, or hooks. Nothing runs on your computer. The
assistant sends tool calls only to the KickBot MCP server at kickbot.com.

## Connect

1. Install the plugin in your AI app.
2. Select Connect or Authorize. Sign in to KickBot.
3. Pick a channel and choose read-only or read and write access.

Your channel permissions apply. Changes go live on your channel right away. Keep
OBS browser source URLs private. You can disconnect at any time on the API & MCP
page of the KickBot dashboard.

## Data

The KickBot MCP server reads and changes your KickBot settings for the channel
you pick. The plugin does not collect anything itself. See the
[Privacy Policy](https://kickbot.com/privacy-policy) and [Terms](https://kickbot.com/terms-of-service).

[Connection guide](https://docs.kickbot.com/dashboard/api/connect-ai-apps) · Support: support@kickbot.com

Version 0.1.5. MIT license, see LICENSE and NOTICE.
