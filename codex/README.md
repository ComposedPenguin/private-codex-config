# Shared Codex configuration

The tracked file `AGENTS.md` contains portable behavior shared between computers. Each computer should also preserve its existing global instructions as `machines/<profile>.md`.

After pulling changes, rebuild the active global file with:

```fish
fish ~/dotfiles/codex/assemble-agents.fish desktop
```

Replace `desktop` with the local profile name. The assembler preserves an existing non-generated `~/.codex/AGENTS.md` as a timestamped backup before composing the shared and machine-specific instructions.

Do not commit `~/.codex/auth.json`, history, logs, SQLite databases, session state, model caches, locks, or generated plugin caches.
