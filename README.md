# libvirt-gpu-passthrough
Scripts and configs for my vfio setup

Current host-hardware configuration
* core i7 6500
* intel igp for the host
* 32gb ddr4
* ssd with lvm for storage
* nvidia gtx970 for passthrough
* archlinux
* synergy for shared mouse/keyboard


Setup at the moment
* two monitors used for host when vm is not running, both connected to IGP
* one of the two monitors is also connected to the gtx970
* when the guest starts, the left monitor on the host is disabled, switching to the gtx970
* the host desktop is moved to the right screen
* cpugovernor is set to performance
* synergy starts in client mode on the host, if the host is the server most games that capture the mouse wont work properly
* on shutdown the original host setup is restored
* the cpugovernor gets reset to powersave
* synergy is shutdown

The VM uses virtio for the network card, and virtio-scsi for storage

Memory for the guest is allocated with hugepages

Pitfalls
* Sound was not working due to a permission issue. Setting the user in ```/etc/libvirt/qemu.conf``` to my user fixed that
* Creating a bridge with networkmanager was harder to figure out than plain netctl/bridgeutils/etc 
* Error 43 on nvidia driver install, easy fix  with hv_vendorid and kvm hiddin domain xml
