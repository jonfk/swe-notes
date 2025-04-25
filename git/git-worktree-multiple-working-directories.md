# Using Git Worktree for Multiple Working Directories

Git worktree allows you to have multiple working copies of the same repository simultaneously, each at different commits or branches. This is extremely useful when you need to:

- Work on multiple features in parallel
- Make a hotfix while in the middle of feature development
- Compare implementations across different branches

## Basic Commands

### Adding a new worktree

```bash
git worktree add ../path-to-new-directory branch-name
```

This creates a new working directory at the specified path, checked out to the named branch.

### Listing worktrees

```bash
git worktree list
```

### Removing a worktree

```bash
git worktree remove path-to-worktree
```

## Practical Workflow Example

1. **Start with your main repository**:
   ```bash
   cd ~/projects/my-repo  # Your original repository
   ```

2. **Add a worktree for a feature branch**:
   ```bash
   git worktree add ../my-repo-feature feature-branch
   ```

3. **Add a worktree for a specific commit or tag**:
   ```bash
   git worktree add ../my-repo-v1.0 v1.0
   ```

4. **Create and check out a new branch in a worktree**:
   ```bash
   git worktree add -b hotfix/bug-123 ../my-repo-hotfix main
   ```

You now have multiple directories, each containing a different version of your code, all sharing the same Git history and objects.

## Best Practices

- Keep worktree directories outside but adjacent to your main repository
- Use descriptive directory names matching branch purposes
- Remove worktrees when you're done with them
- Remember all worktrees share the same config and hooks from the main repository
