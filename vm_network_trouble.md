Multiple things went wrong while setting all of this up. I will try and exlpain it in this.

1. When deleting libvirt's default network I added the new bridge network that I made first, effectivly creating a new NIC interface. This caused the VM's to not request DHCP names as the new NIC was
not set up for that. The old NIC interface was still the default. Easy fix of changing the /etc/network/interface/* if I could just console in.

2. When setting up the VMs originally they were all setup headless. The VM's serial ports were not outputting to libvirt's ptyS0 serial port, meaning I could not console into them, and with the 
network problems I could not SSH into them either. I had to mount the VM's virtual harddrives ".qcow2" to the host OS and update their GRUB to send serial signals over libvirt's ptyS0 port.

3. After fixing both problems I was having problems with my NAT rules. Learning to flush nftables before updating their rules was very valuable :)
