# fish-eza — Repository Guidelines

## Project Structure & Module Organization

fish shell plugin that replaces `ls`-style aliases with `eza` equivalents. Installed via [Fisher](https://github.com/jorgebucaran/fisher) 4.0+.

| Path | Purpose |
|------|---------|
| `conf.d/fish-eza.fish` | Main entry point — install/update/uninstall event handlers. Defines all aliases and their `EZA_*_OPTIONS` env vars. |
| `functions/eza_git.fish` | Auto-detects git repos and appends `--git` to `ll*` aliases. |

## Build, Test, and Development Commands

No build system or test suite. This is a pure fish shell plugin.

- **Install locally**: `fisher install ./fish-eza` (from parent dir) or clone and `fisher install <local-path>`
- **Uninstall**: `fisher uninstall plttn/fish-eza`
- **Validate syntax**: `fish --check conf.d/fish-eza.fish && fish --check functions/eza_git.fish`
- **Test in shell**: `fish` then run `ll`, `lla`, `ltaa`, etc.

## Coding Style & Naming Conventions

- Fish shell syntax: 4-space indentation, `set` for variables, `function` blocks for logic
- Env vars are uppercase with underscores: `EZA_STANDARD_OPTIONS`, `EZA_LL_OPTIONS`, `EZA_LI_OPTIONS`
- Internal vars prefixed with `__FISH_EZA_` to avoid collisions
- Alias names are lowercase short forms: `l`, `ll`, `lg`, `le`, `lt`, `lc`, `lo`
- Extended aliases append suffixes: `lla`, `llad`, `ltaa`, etc.
- `ll*` aliases route through `eza_git` function (auto `--git` in git repos); all others call `eza` directly

## Key Conventions

- Extended options are **prepended** to base alias options in the alias expansion
- `ltaa` and `ltaac` are skipped (`--tree` is useless with `--all --all`)
- Config uses `set -Ux` for universal exports; users should avoid quotes — set vars as lists
- No nested AGENTS.md or project skills needed for this small repo
