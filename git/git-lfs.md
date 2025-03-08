# Git LFS

Git LFS (Large File Storage) uses Git's content filtering system to handle large files efficiently.
It works through three main mechanisms:

1. Clean Filter: Converts large files to LFS pointers when adding to the index.
    The pointer contains a unique SHA-256 hash that references the actual file content stored on the LFS server.
2. Smudge Filter: Replaces LFS pointers with actual file content when checking out.
    If the file isn't cached locally, it's downloaded from the LFS server. 
    - These filters are registered in .gitattributes for specific file patterns.
3. Pre-commit Hook: 
    - Automatically runs before each commit to ensure LFS objects are properly tracked.
    - Identifies new or modified LFS-tracked files and prepares them for storage.
    - Uploads the LFS objects to the remote LFS server during git push.

## Notes on implementation

Can be implemented with libgit2 for custom Git implementations, but would require integration with the Git LFS binary 
in Go.
The Git LFS extension handles authentication, transfer protocols, and server communication.

## Personal feelings

I am pretty over git LFS for a few reasons:
- Git hosts/forges need to have support for git LFS which not all hosts do (e.g. sourcehut doesn't)
- Git hosts naturally have to enforce certain limits for git LFS objects, but I find that those limits are often enough
and less than the normal size limits of git repos. It feels like this is done to get users locked into git that forge's
LFS
- Once you start using git lfs on a repository, you need to continue always using it for the the files that are in there.
I can see git repos that get good value out of their git lfs objects making good use of it but for my usage as a personal
user, I haven't found it to be useful.

So my personal feelings are to simply check-in my binary files into the repositories and use them as normal git objects.
If these would tend to change often, I prefer to version them outside of git rather than using git lfs. It keeps my 
repositories simple and I never have to question whether I initialized a git repository correctly or have git lfs manage
my binary files.
