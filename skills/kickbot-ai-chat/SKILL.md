---
name: kickbot-ai-chat
description: Set up KickBot AI features for a Kick channel. Use for the AI chatbot character that answers viewers in chat, custom personas and prompts, the AI model, web search, and the !imagine AI image command with its OBS widget.
---

# KickBot AI chat features

Read `get_account_overview` first. If the connection is missing, use the
host's KickBot Connect flow. Do not request credentials in chat.

## AI character

Read `get_ai_character_settings`, then send only the requested fields to
`update_ai_character_settings`. A verified account is required.

- Viewers talk to the character when they mention @KickBot in chat.
- Set who can use it with the everyone, subscriber, VIP, and moderator fields.
- Use a preset `character`, or set `character` to "Custom" with a
  `custom_prompt` of 15 to 1000 characters.
- Use the model IDs from `model_options`. Some models and web search need a
  different plan. If a tool returns `premium_required`, tell the user and do
  not retry.

When you write a custom prompt, keep it short and suitable for live chat.
Include rules against hate, harassment, sexual content, and impersonation of
real people. The streamer is responsible for the character in their channel.
Do not write a prompt that tries to avoid KickBot or Kick content rules.

## Imagine

Read `get_imagine_settings` before `update_imagine_settings`. Viewers use
`!imagine <prompt>` in chat. The settings include who can use it, the image
style, how long images stay on screen, and the slide direction.

The response has the Imagine widget URL. Tell the user to add it as an OBS
Browser Source and keep it private. `test_imagine` shows a sample image on the
live widget. Ask before you test while the streamer is live.
`get_imagine_queue` lists recent images.

Read the settings back after each change. Report what changed and the usage
against the plan limit if the tool returns it.

Reference: https://docs.kickbot.com/dashboard/api/reference/ai_character
