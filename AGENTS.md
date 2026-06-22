# Repository Guidelines

## Project Structure & Module Organization

This repository is a Rime Ice configuration tree. Root `*.schema.yaml` files define input schemes such as `rime_ice`, `double_pinyin_*`, `melt_eng`, and `t9`; `default.yaml`, `squirrel.yaml`, and `weasel.yaml` hold frontend-wide settings. Chinese dictionaries live in `cn_dicts/`, English dictionaries in `en_dicts/`, conversion data in `opencc/`, Lua translators and filters in `lua/`, and personal high-priority entries in `custom_phrase.txt`. The `others/` directory contains recipes, platform examples, assets, and the Go maintenance tool under `others/script/`. Treat `build/` and `*.userdb/` as generated or local runtime state unless a change is intentional.

## Build, Test, and Development Commands

- `'/Library/Input Methods/Squirrel.app/Contents/MacOS/Squirrel' --reload`: redeploy the macOS Squirrel configuration after editing Rime files.
- `'/Library/Input Methods/Squirrel.app/Contents/MacOS/Squirrel' --build`: build schemas from the current configuration directory.
- `go test ./others/script/...`: compile and test the Go maintenance module; use this instead of `go test ./...` from the repository root.
- `go run ./others/script s`: sort and deduplicate supported dictionaries. Run only when intentionally regenerating dictionary order, then review the diff carefully.

## Coding Style & Naming Conventions

Use two-space indentation in YAML and preserve existing explanatory comments. Dictionary and custom phrase entries are tab-separated, usually `word<Tab>code<Tab>weight`; do not replace required tabs with spaces. Keep schema names, dictionary names, and translator keys aligned with existing Rime identifiers. Format Go code with `gofmt`. Lua files use local variables and small translator/filter modules; follow nearby style. Use `python3` for any one-off Python helper.

## Testing Guidelines

There is no separate automated test suite for schemas or dictionaries. Validate config changes by redeploying with Squirrel and testing the affected input code manually. For script changes, run `go test ./others/script/...`. For dictionary edits, check tab formatting, duplicate entries, and generated diffs before committing.

## Commit & Pull Request Guidelines

The history uses concise imperative summaries and occasional Conventional Commit prefixes such as `chore:` or `fix(lua):`. Start commits with a high-level summary, then include a detailed body explaining changed files, decisions, and assumptions. Pull requests should describe affected schemes or dictionaries, list validation performed, link relevant issues, and include screenshots only for visible frontend or documentation changes.

## Agent-Specific Instructions

Before editing, check for user changes with `git status --short`. Do not overwrite local customizations such as `custom_phrase.txt`, `*.custom.yaml`, or user database files unless explicitly requested.
