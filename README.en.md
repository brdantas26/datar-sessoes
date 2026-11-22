# datar-sessoes

🇧🇷 [Versão em português](README.md) · 🇺🇸 English

A skill for the **Claude desktop app** (Code tab) that adds the last-activity date and time to each session title: `[22/11 15:14] My session` (day/month hour:minute, in your local time zone). Run it again to refresh the timestamps.

## Install from GitHub (untested)
```
/plugin marketplace add brdantas26/datar-sessoes
/plugin install datar-sessoes@datar-sessoes
```

## Install manually
Download the ZIP (**Code → Download ZIP**) and copy `skills/datar-sessoes` into `~/.claude/skills/` (Windows: `C:\Users\YOU\.claude\skills\`). Then run `/datar-sessoes` in the app.

## How it works
1. Lists your sessions and reads each `lastActivityAt` (UTC), converting it to your local time zone.
2. Shows a table `current title → new title` and asks for confirmation.
3. Renames each session with `[dd/mm HH:mm] Title`, replacing any old prefix.

## Limits
- Only works where the desktop app's session tools exist (not terminal-only).
- Not automatic: create a scheduled task that calls `/datar-sessoes` if you want it to run on its own.
- Sessions without a title are skipped. Titles ending in `…` are dated normally (the app already stores them truncated).
- Only titles are changed. Nothing is deleted or archived. To undo, remove the `[dd/mm HH:mm] ` prefix.

## License
MIT
