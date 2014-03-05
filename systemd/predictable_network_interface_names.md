/*
Title:  Predictable Network Interface Names
Author: Philipp Schmitt
Date: 2014/03/05
Tags: systemd,network,linux
*/

### How not to get screwed

This isn't really new but since systemd 197, network devices are named following a new scheme. Byebye eth0 and wlan0.
The [ArchWiki](https://wiki.archlinux.org/index.php/Network#Device_names) warns about possible network profile breakage but doesn't provide any hint on how to PREDICT what the new name of the interface will be. I successfully figured mine out using:

    # Replace eth0 with the name of your current network device
    NET_DEVICE=eth0
    udevadm test-builtin net_id /sys/class/net/$NET_DEVICE 2>/dev/null | sed -n 's/^ID_NET_NAME_PATH=\(.*\)/\1/p'

**Read more:**

- [systemd source @freedesktop](http://cgit.freedesktop.org/systemd/systemd/tree/src/udev/udev-builtin-net_id.c#n20)
