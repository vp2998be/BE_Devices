# Device Setup - SPS Demo


## Overview

| Device | Address | Status |
| --- | --- | --- |
| RevPi Core S (custom case) | 192.168.178.119 | Reachable, default credentials |
| RevPi Core S (case with info) | 192.168.178.23 / SSH at 192.168.176.63 | Reachable, MAC not recorded |
| Raspberry Pi + display | 192.168.176.82 (static) | Static IP done, kiosk pending |
| Siemens S7-1200 G2 (CPU 1212C) | 0.0.0.0 (none) | Found, no IP yet |
| Siemens ET200SP | 192.168.1.3 | Found, different subnet |
| Coligo Syna (Toradex) | 192.168.176.81 (static) | Done |
| TQ MBox (tq-mbox-3) | 192.168.178.73 (static) | Done |
| B&R controller | 192.168.178.214 | Found only |

## Network

- Gateway and DNS: 192.168.178.1
- Subnet mask /22 (255.255.252.0), so 192.168.176.x through 192.168.179.x are all on the same LAN — the 176.x and 178.x addresses can reach each other directly.
- Your laptop (Wi-Fi): 192.168.178.47

## Revolution Pi Core S — custom case

**Access**

- Shell user: `pi` · Web user: `admin`
- Default password (shell and web): `nv0s54`
- IP: 192.168.178.119
- MAC: C8:3E:A7:10:9F:A6

**Completed**

- [x] Found on network, IP and MAC recorded

**Open**

- Nothing Open

## Revolution Pi Core S — case with info

**Access**

- Shell user: `pi` · Web user: `admin`
- Default password (shell and web): `zsfb5y`
- IP (from notes): 192.168.178.23
- SSH listed under this device: `ssh admin@192.168.176.63`, password `Coligo123!`

**Completed**

- [x] Found on network, default credentials recorded
- [x] SSH login at 192.168.176.63 recorded
- [x] Set a static IP (192.168.176.63)

**Open**

- [ ] Record the MAC address (field left empty)

## Raspberry Pi + display

**Access**

- IP: 192.168.176.82 (static)
- `ssh admin@192.168.176.82`
- Configured via `sudo raspi-config`

**Completed**

- [x] Static IP set (192.168.176.82)

**Open**

- [ ] Stop the screen blanking ("blank screen watchdog" note)
- [ ] Open the target website automatically on every boot (kiosk mode)

**Commands**

- Shut down: `ssh -t raspberrypi "sudo shutdown -h now"`
- Reboot: `ssh -t raspberrypi "sudo reboot"`

## Siemens S7-1200 G2

**Hardware**

- CPU 1212C DC/DC/DC, order no. 6ES7212-1AG50-0XB0, firmware state FS 02, built 2026
- Supply 24 V DC, up to 700 mA
- 8 digital inputs (24 V), 6 digital outputs (24 V, 0.5 A each)
- MAC: 10:D6:57:DF:42:D7

**Discovered stations**

| MAC | Station name | IP | Subnet | Gateway | Type |
| --- | --- | --- | --- | --- | --- |
| 10:d6:57:df:42:d7 | (none) | 0.0.0.0 | 0.0.0.0 | 0.0.0.0 | S7-1200 G2 (CPU 1212C) |
| 4c:e7:05:33:ff:d4 | et200sp | 192.168.1.3 | 255.255.255.0 | 0.0.0.0 | ET200SP |

**Completed**

- [x] Hardware details and MAC recorded
- [x] CPU and ET200SP discovered on the network

**Open**
- Nothing open

**Command**

- Find the CPU in the ARP table (Windows): `arp -a | findstr /i "10-d6-57-df-42-d7"`

## Coligo Syna (Toradex)

**Access**

- Original IP: 192.168.178.115 (MAC 00:14:2D:EF:E7:06, vendor Toradex AG)
- New static IP: 192.168.176.81

**Completed**

- [x] SSH (port 22) reachable at 192.168.178.115
- [x] Static IP set (192.168.176.81)
- [x] SSH (port 22) verified at 192.168.176.81

**Open**

- Nothing open

**Command**

- Check SSH port (PowerShell): `Test-NetConnection 192.168.176.81 -Port 22`

## TQ MBox (tq-mbox-3)

**Access**

- root / root · user / user
- Original IP: 192.168.178.28
- `ssh user@192.168.178.73`

**Static IP config**

- Method: manual
- Address: 192.168.178.73/22
- Gateway: 192.168.178.1
- DNS: 192.168.178.1

**Completed**

- [x] Static IP set (192.168.178.73/22)
- [x] Auto sleep disabled

**Open**

- Nothing open

**To undo the sleep change**

- `sudo systemctl unmask sleep.target suspend.target hibernate.target hybrid-sleep.target`
- `sudo rm /etc/systemd/logind.conf.d/no-sleep.conf`

## B&R

**Access**

- IP: 192.168.178.214
- MAC: 00:60:65:83:20:FE (vendor B&R Industrial Automation GmbH)

**Completed**

- [x] Found on network, IP and MAC recorded
- [x] Identify the model and login credentials
- [x] Set a static IP (192.168.176.64)

 | Setting | Value |
|---|---|
| IP address | 192.168.176.64 (static, DHCP off) |
| Netmask | 255.255.252.0 |
| Gateway | empty |
| Hostname | brdemoroom |
| OPC UA | opc.tcp://192.168.176.64:4840 |
| Hardware address | 00-60-65-83-20-fe |
**Open**

- Nothing open