# Opening Files in Existing Neovim/Neovide Instances

https://neovim.io/doc/user/remote.html

NeoVim has a client-server communication functionality that allows one NeoVim server to accept remote commands such as opening files and sending commands from various Neovim clients to that server. 

## Terminal Neovim

### Starting a Server Instance

```bash
nvim --listen /tmp/nvim-server
```

### Opening Files in the Running Instance

```bash
nvim --server /tmp/nvim-server --remote file1.txt file2.txt
```

You can also open files in new tabs:

```bash
nvim --server /tmp/nvim-server --remote-tab file1.txt file2.txt
```

Or send commands to the server:

```bash
nvim --server /tmp/nvim-server --remote-send ':echo "Hello"<CR>'
```

## Neovide

We can use this client/server functionality for sending remote commands to start a NeoBeam server, connect to it from the Neovide GUI, and send files to that instance. 

With the NeoVim server running, we can connect to that server with the following. 

```bash
neovide --server=/tmp/nvim-server
```