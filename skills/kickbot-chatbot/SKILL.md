---
name: kickbot-chatbot
description: Set up the KickBot chat bot for a Kick channel. Use for custom chat commands such as !discord or !socials, command variables and cooldowns, timed messages, chat alerts for follows, subs, gifted subs, and KICKs, and chat moderation filters such as banned words, caps, and spam.
---

# KickBot chat bot

Read `get_account_overview` first. If the connection is missing, use the
host's KickBot Connect flow. Do not request credentials in chat. Read the
current items before you change them, and save only what the user asked for.

KickBot must be a moderator in the channel to post and delete messages. If the
bot does not reply, ask the streamer to type `/mod KickBot` in their Kick chat,
then call `check_moderator_status`. There is no tool to send a chat message, so
do not claim that the bot replied. Ask the user to test the command in chat.

## Commands

- Read `list_commands` before you add or change a command.
- Use `set_command_by_name` for a named command. It creates or updates one
  command and can run again without a duplicate. Read the existing command
  before you replace its response or permissions.
- Send the name without `!`. Names have at most 20 characters and no spaces.
  Responses have at most 500 characters. Cooldowns are 0 to 300 seconds, for
  each viewer (`user_cooldown`) or for everyone (`global_cooldown`).
- Responses can use variables in double curly braces, for example
  `{{sender.username}}`, `{{sender.followage}}`, `{{param}}` (the word after the
  command), `{{taggedUser.username}}`, `{{stream.title}}`,
  `{{stream.category}}`, `{{randomRange(1,100)}}`, and
  `{{randomItem("a","b")}}`. The tool schema has the full list.
- Set who can use it with the everyone, subscriber, VIP, and moderator fields.
- Built-in commands can be edited or disabled, but not renamed or deleted.
- A plan can limit the number of enabled commands. A new command can be saved
  disabled at the limit. Check the returned note and read it back with
  `get_command` before you say that it is enabled.

## Timed messages

- Read `list_timers` first. Timers have no name. Match a timer by its text and
  settings, and do not create a duplicate on a retry.
- Use `create_timer` for a new timer and `update_timer` for an existing one.
- `interval` is minutes between posts, from 5 to 180. `spacing` is the number
  of viewer messages between posts, from 1 to 30, so the bot does not post in
  an empty chat. Text has at most 500 characters.
- A plan can limit the number of enabled timers. Check the saved state.

## Chat alerts

Chat alerts are messages that KickBot posts in chat. Read
`get_chat_alert_settings`, then send only the requested fields to
`update_chat_alert_settings`.

- Follows, subs, gifted subs, and KICKs each have an on/off field and a text of
  15 to 300 characters.
- Keep the variables: `{{username}}` for all types, `{{months}}` for subs,
  `{{sub_count}}` for gifted subs, and `{{amount}}` for KICKs.
- Gifted subs and KICKs have a minimum amount. 0 posts every time.

For on-stream alerts with animation and sound, use the alerts and overlays
skill.

## Chat moderation

- Read `get_moderation_settings` before `update_moderation_settings`.
- The filters are the built-in bad word list, repeated text, excessive caps,
  zalgo text, and maximum message length (500 means no limit).
- `custom_banned_words` and `banned_regex` replace the full list. Keep entries
  that the user did not ask to remove. Invalid entries are dropped, so check
  the returned lists.
- `list_moderation_logs` shows the messages that the filters deleted.
- TTS and tip moderation have separate settings in their own skills.

Read back each changed item. Report what changed and its saved enabled state.
If a write has an uncertain result, read the item before you retry. Do not
repeat a write until you know its result.

Reference: https://docs.kickbot.com/dashboard/api/reference/commands
