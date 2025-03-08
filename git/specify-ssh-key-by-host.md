# Specify ssh key by host

To be able to used different ssh keys for different projects/repositories, you can configure an ssh key per host.

## Example

By using the following ssh config, you could used different ssh keys by cloning the repositories by specifying the
host as follows: 

- `git clone git@jonfkgithub:jonfk/dotfiles.git` would clone the dotfiles repository using the `~/.ssh/id_ed25519_jonfk`
ssh key.
- `git clone git@workgithub:workorg/workrepo.git` would clone the workrepo repository using the `~/.ssh/id_ed25519` key.

```
# ~/.ssh/config

Host jonfkgithub
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_ed25519_jonfk

Host workgithub
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_ed25519
```
