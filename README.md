# push

A standalone, no-dependency GitHub pusher. Python stdlib only — no install, no pip. You can upload your code directly from vscode terminal.

## Install

```bash
cp push ~/.local/bin/push
chmod +x ~/.local/bin/push
```

Requires `gh` (or a `GITHUB_TOKEN`) to create repos.

## Commands

```text
push                                              numbered picker over changed files + repo picker
push main.c utils.py -r proj                      these files only, no file picker
push -y -m "wip"                                  commit everything, zero prompts
push --dry-run                                    git status only; change nothing
```

| Flag | Meaning |
|------|---------|
| `-r repo` | target GitHub repo (`myproj` or `owner/myproj`) |
| `-b branch` | branch to push (remembered per project; default `main`) |
| `-m message` | commit message (else prompted; `e` opens `$EDITOR`) |
| `--ssh` / `--https` | transport (default, and remembered per project) |
| `--public` | create the GitHub repo public (default: private) |
| `-y` | never prompt; take every default |
| `--reset` | forget this project's remembered settings (`.pushconfig.json`) |
| `--selftest` | run internal parser checks |

## Full usage

```
usage: push [-h] [-m MESSAGE] [-y] [-r REPO] [-b BRANCH] [--ssh] [--https]
            [--public] [--dry-run] [--reset]
            [files ...]

Push your work to GitHub. Stdlib only, no installation.
```

## How it works

Every run (unless `-r` or `-y`) asks **which repo** via a numbered picker of
your GitHub repos — the remembered repo from `.pushconfig.json` is the
Enter-default. Then it stages changed/untracked files (numbered picker),
optionally shows the cached diff, commits, creates the repo if missing, and
pushes. Repo/branch/transport are cached per project in `.pushconfig.json`.
