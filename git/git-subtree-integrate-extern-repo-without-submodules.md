# Git Subtree Quick Reference

Git subtree lets you embed external repositories directly within your own repo, preserving their files and history while allowing you to treat them as part of your codebase.

## When to use

- When you want to include external code that you may modify
- When you want the external code to be immediately available (no extra steps for others)
- When you want to maintain the ability to pull upstream changes

## Key commands

```bash
# Add external repo as remote
git remote add <name> <repository-url>

# Add the subtree
git subtree add --prefix=<local-path> <remote-name> <branch> --squash

# Pull updates later
git subtree pull --prefix=<local-path> <remote-name> <branch> --squash
```

## Tracking subtree sources

Since remotes are only stored locally, document subtree sources by:

- Creating a `SUBTREES.md` file listing all sources
- Using descriptive commit messages with source URLs
```bash
git subtree add --prefix=libs/algorithm https://github.com/org/algorithm.git main --squash -m "Add algorithm library from https://github.com/org/algorithm.git (main branch)"
```
- Adding a `SOURCE.md` in each subtree directory
	- e.g.
```
This code was imported from https://github.com/org/algorithm.git (main branch)
Last synchronized: 2025-05-09
```

## Why use subtrees over submodules

- Files are physically in your repo (not just pointers)
- Your repo has full ownership of the code
- No special commands needed for team members to get the code
- You can modify the included code freely
- Still maintain connection to upstream for future updates