# Multiple Git Profiles

When working on different github accounts, the accounts cannot share the same ssh key. You may also want to have 
different name and email set to the different accounts. 

The way I solve this is by having the git config included based on the repository with the `includeIf` construct 
and the directory under which the alternate config should be turned on.

## Example

The following setup would be how I would set it up on a work computer. The default config would therefore be taken
from the `.gitconfig.work`, but in any path under `~/jonfk_code` or `~/another_jonfk_code`, the `.gitconfig.jonfk`
would be in effect.

This setup assumes that there is a default `~/.ssh/id_ed25519` ssh key and one at `~/.ssh/id_ed25519_jonfk`.

```
# .gitconfig

[include]
    path = ~/.gitconfig.common

# Default to work settings on work computer
[include]
    path = ~/.gitconfig.work

# Use personal settings for specific directories
[includeIf "gitdir:~/jonfk_code/"]
    path = ~/.gitconfig.jonfk

[includeIf "gitdir:~/another_jonfk_code/"]
    path = ~/.gitconfig.jonfk
```

```
# .gitconfig.work
[user]
	name = Jonathan Fok kan
	email = jfokkan@examplework.com

[github]
    user = jfokkan-examplework
```

```
# .gitconfig.jonfk
[user]
	name = Jonathan Fok kan
	email = jonathan@fokkan.ca

[core]
    sshCommand = ssh -i ~/.ssh/id_ed25519_jonfk

[github]
    user = jonfk
```

## Alternative

I previously tried to use ssh config to do something somewhat similar in the past but replaced it with this setup in 
the end. Both ways could possibly be used complementarily. 
See [specify-ssh-key-by-host](./specify-ssh-key-by-host.md)
