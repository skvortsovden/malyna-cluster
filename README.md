# malyna-cluster-logbook

This is a logbook of my home lab cluster setup.

## hardware

- 3x Raspberry Pi 4B (2x 4GB RAM, 1x 8GB RAM)
- 3x 32GB microSD card
- 1x usb hub anker with 6 usb ports

## software
- Raspberry Pi OS Lite (64-bit) a port of Debian Trixie with the Raspberry Pi with no desktop environment

## configuration

- node1:
  - hostname: malyna
  - role: master
- node2:
  - hostname: kalyna
  - role: worker
- node3:
  - hostname: lohyna
  - role: worker

## logbook records

### 2026-03-08

- ssh key-based authentication configured on all nodes
- ssh password authentication disabled on all nodes
- catch-22: do not hardcode dynamic IP addresses in the SSH configuration
  - details: locked myself out of all nodes by hardcoding dynamic IP addresses in the ListenAddress in SSH configuration, when restarted the nodes got different IP addresses assigned by the router DHCP, which caused me to lose SSH access to all nodes. I got back in by re-installing the OS on SD cards and re-configuring SSH access