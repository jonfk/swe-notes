You can set up a separate Neovim configuration and create a different command to access it. The easiest approach is to use the `NVIM_APPNAME` environment variable, which tells Neovim to use a different configuration directory.

Here's how to set it up:

1. Create a new directory for your experimental config:
   ```bash
   mkdir -p ~/.config/nvim-test
   ```

2. Copy your existing config to start with or start one fram scratch:
   ```bash
   cp -r ~/.config/nvim/* ~/.config/nvim-test/
   ```

3. Edit the experimental config files in `~/.config/nvim-test/`

4. Create an alias or function in your shell configuration file (`.bashrc`, `.zshrc`, etc.):
   ```bash
   # For a simple alias
   alias nvim-test='NVIM_APPNAME=nvim-test nvim'
   
   # Or for a more flexible function
   nvim-test() {
     NVIM_APPNAME=nvim-test nvim "$@"
   }
   ```

5. Source your updated shell config or start a new terminal session:
   ```bash
   source ~/.bashrc  # or source ~/.zshrc
   ```

Now you can use `nvim-test` to launch Neovim with your experimental configuration while `nvim` will continue to use your original setup.

The `NVIM_APPNAME` approach is preferred over using `-u` because it properly handles all configuration directories including plugins, which makes it ideal for testing plugin changes.
