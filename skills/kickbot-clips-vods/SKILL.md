---
name: kickbot-clips-vods
description: Work with Kick clips and VODs through KickBot. Use for the !clip chat command, clips made by viewers, downloading Kick clips or past broadcasts as MP4, and cutting a clip from a Kick VOD.
---

# KickBot clips and VODs

Read `get_account_overview` first. If the connection is missing, use the
host's KickBot Connect flow. Do not request credentials in chat.

## !clip command

Read `get_clip_command_settings` before `update_clip_command_settings`. Viewers
type `!clip` (or `!clip 90` for a length in seconds) to make a clip of the live
stream. Set who can use it with the everyone, subscriber, VIP, and moderator
fields. `premium_settings_editable` shows if the reply text and clip lengths
can change. The reply supports `{user}` and `{clip_url}`.

`list_command_clips` lists clips that viewers made. `delete_command_clip`
deletes the video and its public page, and cannot be undone. Delete only the
clip that the user names.

## Kick clip downloads

Use `get_kick_clip` to check a clip URL or ID, then `start_clip_download`.
Downloads usually take under a minute. Use `list_clip_downloads` to get the
status and `download_url`. Any public Kick clip works.

## VOD downloads

Use `get_kick_vod` with the VOD URL to get the title, length, and available
resolutions. Then call `start_vod_download` once. Do not start the same VOD
again while it is queued. Use `list_vod_downloads` for progress, the
`download_url`, and when the file expires. Download limits depend on the plan.
`delete_vod_download` removes a finished file and cannot be undone.

## VOD clip editor

`create_vod_editor_clip` cuts a part of a VOD. Convert times such as 1:02:30
to seconds. `end_seconds` must be after `start_seconds`. Check the VOD length
with `get_kick_vod` first. Use `list_vod_editor_clips` for status and the
download link.

Only download or edit content the user has the right to use. Report the job
status as the tool returns it. Do not claim a file is ready until its status is
complete.

Reference: https://docs.kickbot.com/dashboard/api/reference/clips and
https://docs.kickbot.com/dashboard/api/reference/vods
