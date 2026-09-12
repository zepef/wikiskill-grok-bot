# Install (US)

[Français](INSTALL.fr.md)

Four pastes. No command line.

1. Paste [`prompts/create-bots.md`](prompts/create-bots.md) — creates Archivist, Coach, Referee.
2. Paste [`prompts/create-group.md`](prompts/create-group.md) — creates the Loop group chat.
3. Send [`prompts/init-workspace.md`](prompts/init-workspace.md) to Archivist — builds `/workspace/wikiskill`.
4. After one manual test run, paste [`prompts/create-routines.md`](prompts/create-routines.md) on each owning Bot.

Then: Settings → Plugins → Yours, and enable skills per [`TEAM.en.md`](TEAM.en.md).

Do not start nightly routines while `/workspace/wikiskill/bench/val` is empty. Referee must stop and say `no validation bench`.
