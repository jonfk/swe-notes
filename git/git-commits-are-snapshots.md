# Git commits are snapshots not diffs

source: https://github.blog/open-source/git/commits-are-snapshots-not-diffs/

Git commits are snapshots of your entire codebase at a specific moment, not just the changes you made. This is a key 
insight many people miss about Git. When you make a commit, Git isn't storing the differences between versions 
- it's taking a complete picture of all your files. Commands like cherry-pick and rebase don't actually move commits 
around; they create brand new commits that look similar to the originals. Understanding this snapshot model helps 
explain why Git behaves the way it does and makes it easier to use Git effectively, especially when working with 
complex repository histories.

## Some Implications for Git Commands

- git cherry-pick doesn't "move" a commit; it creates a new commit with a similar diff
- git rebase recreates a series of commits as new objects with new hashes
- Rename detection happens dynamically during diff calculation, not in the stored data

## Some Implications for Complex Git Histories

- Branch Management: When you merge branches, Git doesn't simply apply a series of changes - it creates a new snapshot that combines two different states of your codebase. This explains why merges sometimes create unexpected conflicts that weren't visible in the individual changes.
- Rebasing Long-Lived Branches: When rebasing a branch with many commits, Git is creating an entirely new set of commits with new identities (new hashes). Anyone else working on the original branch will have a completely different history, making collaboration difficult if you rebase shared branches.
- Cherry-Picking: When cherry-picking commits across branches, you aren't "moving" changes - you're creating new snapshots with similar content. This can lead to duplicate changes if you later merge the original branch, as Git sees these as different commits despite having similar effects.
- Repository Performance: For large projects with long histories, Git remains efficient because it only stores unique objects once. Two commits that share mostly unchanged files will reference many of the same objects, keeping repository size manageable.
- Bisecting and Debugging: When using git bisect to find bugs, you're moving between complete snapshots of your codebase. This makes it reliable for tracking down when issues were introduced, as each commit is a fully testable state.
