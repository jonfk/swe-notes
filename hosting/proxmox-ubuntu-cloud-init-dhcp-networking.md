At home I use DHCP to assign IP addresses. Today, when I created an Ubuntu VM using the Proxmox VE helper scripts, the VM came with a Cloud-Init config that needed editing.

Don’t forget to set up networking there (specifically, set the IPv4 config to **DHCP**)or the VM will boot with no network connectivity. 

So far I’ve only fixed it after the fact by manually creating a **netplan** config, applying it, and restarting things; I still need to test doing it correctly via Cloud-Init from the start.
