# opencode-tts-speak

An OpenCode TTS plugin that speaks assistant responses when a session goes idle.

This fork focuses on:

- Windows desktop compatibility
- natural Markdown cleanup before speech
- safe slash-command handling without server-error popups
- `edge-tts` playback through `ffplay`

## Install

Install as an OpenCode plugin:

```bash
opencode plugin opencode-tts-speak
```

Or point OpenCode at a local checkout:

```json
{
  "plugin": ["file:///absolute/path/to/opencode-tts-speak/dist/index.js"]
}
```

Then restart OpenCode.

## Commands

- `/tts-on`
- `/tts-off`
- `/tts-mode-summary`
- `/tts-mode-full`
- `/tts-speak <text>`
- `/tts-repeat`
- `/tts-uninstall`

If your OpenCode build does not show these commands, copy the files in `command/` to:

```text
~/.config/opencode/command/
```

## Configuration

Create or edit:

```text
~/.config/opencode/plugins/opencode-tts.jsonc
```

Example:

```jsonc
{
  "enabled": true,
  "mode": "full",
  "debug": false,
  "backend": "edge_tts",
  "voice": "zh-CN-XiaoxiaoNeural",
  "summaryLength": "2 sentences",
  "edge_tts": {
    "voice": "zh-CN-XiaoxiaoNeural",
    "rate": "+0%",
    "volume": "+0%",
    "player": "C:\\path\\to\\ffplay.exe"
  }
}
```

On Windows, install `ffplay` from FFmpeg and either put it on `PATH` or set `edge_tts.player`.

## Markdown Cleanup

Before speech, the plugin removes Markdown formatting such as headings, bold markers, links, lists, quotes, and code fences. It preserves comparison symbols such as `>` and `<`, so math like `9.7 > 9.11` is still spoken naturally by the TTS engine.

## Development

```bash
npm install
npm run build
npm run typecheck
```
