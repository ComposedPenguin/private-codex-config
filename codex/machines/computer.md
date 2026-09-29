# Global Codex instructions for Oscar's machine

These instructions apply to work on this personal computer. Treat the home directory, desktop configuration, and projects as a real working system with valuable state, not as a disposable development container.

## 1. Machine / OS

- This is a personal x86_64 Arch Linux system using the standard Arch `linux` kernel family. Arch is rolling release, so verify current versions when a task depends on them rather than relying on versions recorded in documentation.
- The GPU is an NVIDIA GeForce RTX 2060 using the NVIDIA kernel driver and graphics stack.
- Do not recommend reinstalling the OS as a first-line fix. Do not blindly reinstall large parts of the desktop environment to solve an isolated problem.
- Do not expose private information discovered on this machine unless it is directly relevant to the task. Never inspect, copy, summarize, or store passwords, API keys, authentication or session tokens, browser cookies, SSH private keys, private keys, credential stores, or secrets files.

## 2. Desktop environment

- The graphical session is Hyprland on Wayland. The desktop is based on `illogical-impulse/end-4` dots-hyprland and is already highly customized.
- The configured display layout has two 1920x1080 displays side by side: `DP-1` on the left at `0x0`, explicitly set to 144 Hz, and `HDMI-A-1` on the right at `1920x0`, using its preferred 60 Hz mode. Both use scale 1. The user requested 144 Hz on DP-1; preserve that choice. Confirm live state with `hyprctl monitors` when the exact current state matters.
- Audio uses PipeWire with the PipeWire PulseAudio compatibility layer and WirePlumber as session manager. Prefer `wpctl`, `pactl`, and relevant user-service logs for diagnosis.
- Kitty is the terminal. Its configuration explicitly launches fish.
- Do not assume functionality is missing because it is absent from one conventional config file. This setup is modular: search the existing configuration, sourced files, services, modules, and helper scripts before proposing a replacement.

## 3. Shell and terminal conventions

- Fish is the preferred interactive shell, and commands given for the user to paste should be fish-compatible unless there is a strong reason to use another shell. The account login shell may still report zsh; Kitty is configured to run fish, and the user's stated preference takes precedence for instructions.
- Give complete, pasteable commands. Verify that quoting, variable expansion, command substitution, chaining, and redirection are valid in fish.
- Avoid bash-only heredocs when a straightforward fish-compatible alternative exists. If bash is genuinely needed, invoke it explicitly and explain why.
- Nano is the preferred editor for quick terminal edits unless the existing project or workflow clearly uses another editor.
- Existing interactive fish conventions include Starship, generated Quickshell terminal colors, `eza` for interactive `ls`, and Kitty's SSH integration. Inspect `~/.config/fish` before changing shell behavior.

## 4. Package management

- Prefer `pacman` for official Arch repository packages and `yay` for AUR packages when appropriate.
- Before installing anything, check whether the needed package, command, library, or equivalent functionality is already present.
- Keep package changes narrowly scoped. Avoid broad desktop reinstall or replacement as a troubleshooting shortcut.
- When a requested action needs administrator authentication, use a graphical password prompt such as `pkexec` when available. Never ask the user to paste a password or to run the command themselves; if graphical authentication is unavailable, report that specific blocker and ask for an alternative.
- Python tooling available on this machine includes `pip`, `pipx`, and `uv`; select the tool that matches the existing project rather than imposing a new package workflow.

## 5. Important config locations

- Hyprland: `~/.config/hypr`
  - Main Lua entry point: `~/.config/hypr/hyprland.lua`
  - Shipped/base modules: `~/.config/hypr/hyprland/`
  - Update-safe user overrides: `~/.config/hypr/custom/`
  - Displays and workspace placement: `~/.config/hypr/monitors.lua` and `~/.config/hypr/workspaces.lua`
  - Inspect the Lua loader, variables, services, helper scripts, and custom layer before editing. Prefer the established `custom/` override mechanism where it fits.
- Quickshell: `~/.config/quickshell/ii`
  - The tree already contains `modules/`, `services/`, `scripts/`, `panelFamilies/`, `assets/`, and shared components. Inspect QML imports, `qmldir` files, singletons, services, and helpers before adding infrastructure.
  - Generated user state and terminal theming may live under `~/.local/state/quickshell/user`; distinguish generated state from source configuration before editing.
- Standalone Pibble picker: `~/pibble`, controlled with `~/pibble/pibble`. Local wallpaper-only integration is enabled by `Settings.wallpaperOnly` in `~/pibble/config/Settings.qml`. Its persistent settings are managed by Quickshell under `~/.local/state/quickshell/by-shell/`; use the existing settings adapter rather than overwriting these files while Pibble is running.
- Wallpaper bridge: `~/.local/bin/pibble-wallpaper` delegates to ii's `~/.config/quickshell/ii/scripts/colors/switchwall.sh`. ii's wallpaper configuration is in `~/.config/illogical-impulse/config.json`; inspect only the fields relevant to the task rather than dumping configuration indiscriminately.
- Fish: `~/.config/fish`
- Kitty: `~/.config/kitty/kitty.conf`, with supporting Kitty scripts in the same directory
- User commands and helpers: `~/.local/bin`
- User services and timers: `~/.config/systemd/user`
- Before making a substantial dotfile change, inspect the relevant existing implementation and every directly connected include, service, module, or helper.

## 6. Development preferences

- Common work includes Python, Java, JavaScript, p5.js, QML/Quickshell, Godot/GDScript, Unity/C#, and shell scripts. A tool need not be globally installed merely because it is part of the normal workload; inspect the current project and its environment.
- LibreOffice Fresh is installed, including Calc. Use Calc as the native spreadsheet application on this Linux system. Its Excel Analysis ToolPak equivalents are built in under `Data > Statistics` (including regression, ANOVA, sampling, correlation, and common statistical tests), so do not look for a separate Microsoft Analysis ToolPak extension. Calc can read and write `.xlsx`; preserve an original copy when exact Microsoft Excel compatibility matters.
- Major system tooling currently includes Git, GCC, Clang, Make, CMake, Ninja, Python, Rust/Cargo, Go, Qt/qmake, VSCodium, Nano, Vim, `jq`, and ripgrep. Verify availability and version when a task depends on either.
- When editing QML/Quickshell or Hyprland configuration, inspect imports, existing services, modules, helper scripts, generated files, and local conventions before inventing new infrastructure. Reuse an existing helper, service, or module when it already performs part of the task.
- Preserve the formatting, naming, file organization, and style already present in a project. Keep solutions reasonably simple and maintainable.
- Do not silently change unrelated parts of a file. If Git is present, use status and diffs where useful, while preserving unrelated working-tree changes.

## 7. Change management / safety rules

- Preserve working custom functionality wherever possible. Prefer extending or modifying the existing system over replacing it with an unrelated alternative, and do not overwrite customizations merely because upstream or default examples differ.
- Prefer small, reversible changes. For risky or broad configuration changes, make or suggest a timestamped backup first and verify the exact target.
- Explain commands that could delete data, overwrite configuration, alter boot configuration, change partitions, or affect system startup.
- Do not run destructive commands unless they are explicitly necessary and authorized for the task. Never run `git reset --hard`, `git clean`, or similarly destructive Git commands without explicit permission.
- Treat boot, display-manager, compositor startup, systemd, storage, and package-removal changes as high-impact. Gather the current state and identify a recovery path before changing them.
- Do not discard unrelated work or rewrite whole files when a focused edit will do.

## 8. Debugging approach

- Gather evidence first. When an error message, log, source file, generated file, config, or live status command can answer a question, inspect it before suggesting speculative fixes.
- Reproduce or characterize the failure when practical, then check the smallest relevant scope: configuration loading order, imports, service state, user journal, helper scripts, permissions, and package versions.
- Search the whole relevant configuration tree before concluding that a feature is absent. Follow references between Hyprland Lua files, Quickshell modules and services, user scripts, and systemd units.
- Prefer focused diagnostics such as `hyprctl`, `qs`, `wpctl`, `pactl`, `systemctl --user`, `journalctl --user`, `rg`, and project-specific checks. Account for the possibility that a command run outside the active graphical session cannot reach its Wayland, Hyprland, D-Bus, or PipeWire socket.
- After a change, use the narrowest meaningful validation first, inspect the diff, and avoid unrelated cleanup.

## 9. Known customizations

- Hyprland uses a Lua loader that combines base modules with files under `~/.config/hypr/custom`; the custom layer is designed to survive dots-hyprland updates.
- Workspaces are split across both displays. The current configuration also includes a special Discord workspace and places Spotify on workspace 10. Preserve these behaviors unless the task specifically changes them.
- Quickshell is a large, established shell rather than a minimal sample config. Existing custom work includes deadline/calendar UI, media controls and MPRIS queue helpers, EasyEffects/audio integration, wallpaper selection/carousel behavior, and video-wallpaper support.
- The user wants **standalone Pibble's wallpaper picker**, including its current appearance, animations, carousel, settings, and live previews. ii supplies the rest of the desktop. Pibble's app/clock/clipboard pages, custom-page scanning, app-icon warming, notification server, volume OSD, notification/launch-history stores, and power/reboot actions are disabled in wallpaper-only mode. Keep those roles in ii; do not re-enable the full Pibble shell as a default fix. Inactive source files remain available for rollback.
- Pibble selections and ii's wallpaper actions share `switchwall.sh` for rendering, theme generation, saved selection, thumbnails, and login restoration. The script serializes requests with a lock whose descriptor is not inherited by renderer processes. Pibble reads ii's generated `colors.json` instead of running a second matugen pass; ii updates Pibble's selection through `launcher syncWallpaper` IPC. Preserve this shared state when changing either picker or theme code.
- ii's background window is intentionally disabled in `modules/ii/background/Background.qml`. `awww` renders still wallpapers; `mpvpaper` renders videos/GIFs. These are complementary renderers, not duplicate shells to remove. The generated `~/.config/hypr/custom/scripts/__restore_video_wallpaper.sh` restores either type at login despite its historical name; edit its generator in `switchwall.sh`, not the generated file. `~/Pictures/wallpapers` is a symlink to `~/Pictures/Wallpapers`.
- `Super+T` opens standalone Pibble. ii's `wallpaperSelector toggle` IPC/global shortcut also opens Pibble; ii's old embedded Pibble-inspired UI remains on disk but is not the normal entry point. The random-wallpaper action still uses ii's wallpaper service. `Ctrl+Super+R` restarts only ii with config-scoped Quickshell commands; never replace it with a blanket kill of `qs`, `quickshell`, or `ydotool`.
- For integration checks, `qs -p ~/pibble ipc call launcher status` reports wallpaper-only mode, active pages, flyout flags, app count, and accent without dumping private state. Use `qs -c ii` versus `qs -p ~/pibble` to target the correct shell. Existing Pibble compatibility edits disabling unsupported `BackgroundEffect.blurRegion` must be preserved.
- GTK, KDE, and Hyprland portal backends are intentionally configured together: `~/.config/xdg-desktop-portal/hyprland-portals.conf` selects KDE for file dialogs and Hyprland/GTK for other interfaces. Multiple portal processes alone are not evidence of duplication. Likewise, installed Waybar/Dunst packages do not establish that another bar or notification daemon is running.
- Backups for the Pibble/ii integration are under `~/.local/state/codex-backups/pibble-ii-*/`, preserving original paths. Inspect the relevant backup/diff before reverting; do not discard the user's pre-existing Pibble changes or reset its Git checkout.
- Quickshell-generated theme data is consumed by both fish and Kitty. Changes to theme generation can therefore affect multiple parts of the desktop.
- Existing user-level automation includes PipeWire/WirePlumber integration, `ydotool`, a periodic MyLearningSpace calendar sync, and a Bluetooth headset auto-connect service. Inspect the relevant unit and helper before modifying or duplicating any of them.
- `~/.local/bin` contains personal helper commands for calendar/deadline workflows, wallpaper handling, camera control, and download-manager integration. Search there before creating a new helper with overlapping behavior.
