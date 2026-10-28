# Playable games from a phone

This repository is a starter for making Playable games in Claude Code or Codex cloud sessions, often by
someone on a phone who does not code. Keep replies short and plain, skip technical detail unless asked, and
do the technical steps yourself.

- Make each game in its own folder (`thothan_start_game` picks one from the title). Its code and art are
  kept in Thổ Thần and show up in the Playable app, so the game is safe even if nothing is committed here.
- "Continue my game": list the creator's games, ask which one if there are several, and open it.
- Finish each piece of work by pushing to Thổ Thần (`thothan_push`) and telling the creator how to play it
  in the Playable app.

<!-- thothan:start -->
## Playable game (Thổ Thần)

This repository builds a Playable game with the Thổ Thần plugin, vendored in `.thothan/`. Follow the
playable-game skill (`.agents/skills/playable-game/SKILL.md`).

- When the `thothan` MCP tools are available, use them as the skill says.
- Without them (some cloud environments start no MCP servers), run the same steps with the CLI. Service tool
  `game_genesis_<api>` is `game call taka-game-genesis <api>`; likewise `image_forge_` → `taka-image-forge`,
  `sound_sage_` → `taka-sound-sage`, `gtd_` → `appota-gtd`.
  - `node .thothan/thothan.mjs game status --json`
  - `node .thothan/thothan.mjs game new "<title>" --prompt "<request>"` or `game open --game <gameId>`
  - `node .thothan/thothan.mjs game reference taka-game-genesis fetch_game_creation_procedure` (reads that need no game)
  - `node .thothan/thothan.mjs game call taka-game-genesis <api> '<json>'`
  - `node .thothan/thothan.mjs game push -m "<note>"`, `game pull`, `game note "<message>"`
- Not signed in? Call `thothan_login` and give the creator the link and code; they approve it on any device.
  With the CLI, run `node .thothan/thothan.mjs login --no-wait`, give the creator the link and code it prints, then run
  `node .thothan/thothan.mjs login --wait` in the foreground (not in the background: some sandboxes stop background
  processes) until it says "Login successful". If it stops before that, run `login --wait` again; the code
  lasts 10 minutes. Never ask for, print, store or commit a key.
- The game itself is kept in Thổ Thần. To continue one in a fresh session, find it with
  `game_genesis_list_studio_projects` and open it with `thothan_open_game` (or `game open --game <gameId>`).
- Asked to update Thổ Thần: run `d=$(mktemp -d) && git clone -q --depth 1 https://github.com/appota-ai/thothan "$d" && node
  "$d/bin/thothan.mjs" game install repo --dir .`, commit the changed files, and tell the creator the new
  version loads in their next session.
<!-- thothan:end -->
