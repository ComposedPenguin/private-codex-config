# Shared Codex instructions

These instructions are portable across Oscar's computers. Treat each machine as a real working system with valuable state, not as a disposable development container.

## Safety and privacy

- Do not inspect, copy, summarize, or store passwords, API keys, authentication or session tokens, browser cookies, SSH private keys, private keys, credential stores, or secrets files.
- Preserve existing custom functionality. Prefer small, reversible changes and make a backup before broad or risky configuration changes.
- Never run destructive commands such as `git reset --hard`, `git clean`, recursive deletion, or broad overwrites without explicit authorization and a clearly verified target.
- Do not expose private information discovered on the machine unless it is directly relevant to the task.

## Working style

- Gather evidence first. Inspect the relevant files, references, services, and current state before proposing or making changes.
- Search files with `rg` or `rg --files` when available.
- Preserve the existing formatting, naming, file organization, and project conventions.
- Keep solutions reasonably simple and maintainable. Do not rewrite unrelated parts of a file.
- After a change, run the narrowest meaningful validation and inspect the diff.
- Give complete, pasteable commands. Prefer the user's active shell and verify quoting, expansion, chaining, and redirection.

## Configuration and development

- Inspect existing configuration, includes, services, modules, helper scripts, and generated files before inventing new infrastructure.
- Before installing packages, check whether the command or an equivalent is already available. Use the operating system's established package manager and keep package changes narrowly scoped.
- Match the project's existing language, toolchain, formatter, test runner, and dependency workflow rather than imposing a new one.
- For desktop or graphical issues, account for the active session, sockets, user services, and generated state. Do not infer that a feature is absent from one conventional config file.

## Machine-specific details

Hardware, operating-system, display, shell, package-manager, and personal-path details belong in a per-machine profile. Verify those details live on the current computer instead of assuming that another computer has the same setup.
