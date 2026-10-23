---
name: kickbot-widget-builder
description: Create or edit private KickBot HTML, CSS, and JavaScript widgets for OBS. Use for stream overlays, follower or subscriber goals, alerts, and channel data displays.
---

# KickBot widget builder

Read `get_account_overview` and `list_widgets`. Use `get_widget` for an existing
widget or `list_widget_templates` for a requested template. Build for the
connected channel and check widget permissions and plan limits.

## Build and save

- `create_widget` accepts a name, HTML body content, CSS, JavaScript, dimensions,
  and variables. Do not put `<html>` or `<head>` wrappers in the HTML field.
- `create_widget` also installs a copy for this channel. Read `get_widget`, then
  pass an ID from `installed_widget_ids` to `get_installed_widget` to get the
  OBS browser source URL. Do not install a second copy just to get a URL.
- Use `update_widget` for a requested change. Patch only the needed fields.
  The `variables` field replaces the full set, so read and preserve other
  variables. Changes to an owned widget appear when OBS reloads the overlay.
- For an installed library widget, use `get_installed_widget` and
  `update_installed_widget` to change its supported settings. These saves cause
  the live overlay to reload.
- Check for the named widget after an uncertain write before creating another.

## Runtime

Read widget settings from `userVariables.<key>.value`. Channel data is in
`globalValues`, including `followerCount`, `subCount`, `viewerCount`,
`lastFollower`, `lastSub`, `streamerInfo.kick`, and `currentStream`.
Handle unavailable data at startup without showing a false count.

Listen for live changes through the widget event bus:

```javascript
document.addEventListener('widgetEvent', (event) => {
  const { event_name, data } = event.detail;
  // Update the relevant UI from the documented event payload.
});
```

Events include `followEvent`, `followerCountUpdatedEvent`, `subEvent`,
`subCountUpdatedEvent`, `viewerCountUpdatedEvent`, and `chatMessageEvent`.
Read the current runtime reference for the event payload you need:
https://docs.kickbot.com/dashboard/widgets/widget-builder-docs

Use `window.kickbotWidget.createTextNode(text)`, DOM `textContent`, or the
documented `createChatMessageFragment(content, font_size)` helper for viewer
text. Do not put chat messages or viewer names into `innerHTML`. Do not add
external scripts, trackers, or data uploads that the requested widget does
not need. Keep credentials and private browser source URLs out of its code.

## Preview and delivery

Check the code and layout before saving. Verify the saved code, dimensions,
variables, and installed copy after saving. Return the OBS URL privately and
state which parts need an OBS or live-event check. Do not claim that a live
event test passed when only the code was checked.

A private widget does not need public library submission. `publish_widget`
starts that separate process. Call it only when the user explicitly asks to
submit the widget to the public library and supplies the required material.
