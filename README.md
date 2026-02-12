# Pfsense-HomeLab-Configuration 

PfSense Home Lab Firewall Deployment

A self-hosted pfSense firewall/router deployment for my personal homelab, built to provide:

-Network segmentation
-Centralized routing
-DHCP/DNS services
-Ad blocking (pfBlockerNG)
-A foundation for future IDS/IPS and VPN services

-This project documents the full installation process, upgrade path, and real-world issues encountered during my deployment.

I started this project to improve the security of my home network, strengthen my networking skills, and prepare for future self-hosted services. I am currently setting up a home server to host applications such as Bitwarden and Nextcloud, and I will be documenting those projects soon.

Here is a link to the netgate documentation page:
[Pfsense Docs](https://docs.netgate.com/pfsense/en/latest/)

## Hardware Used:
| Component | Details      |
| --------- | ------------ |
| Device    | ZimaBoard    |
| CPU       | Intel-based  |
| RAM       | 4GB          |
| Storage   | 32 GB eMCC   |
| Intel NIC | 1 Gigabit    |


Network Typology:
ISP Modem (Bridge Mode)
        ↓
   pfSense (WAN)
   pfSense (LAN)
        ↓
      Switch
        ↓
  Access Point + Clients

### Step 1: Flash ISO
- Flash PFsense to a usb drive
- install the ISO from netgate, or find the 2.7.2 community edition online. (Netgate has the 2.8.1 version on the website. This version requires internet for installation)
- Flash it to a drive with balena etcher or Rufus. 


### Step 2: Bridge Mode
- convert ISP router to bridge mode.
- connect to the web ui via ethernet and turn on bridge mode. (You may need to find the default credentials on the router or online.)

### Step 3: Install PFSense
- Installed 2.7.2 Community Edition, you will need to go into the Bios of the device on boot and change the order to boot from the USB if that is what you are using. 
- Upgraded after first boot
 Installer created:
  WAN interface
  LAN interface
  Default LAN IP: 192.168.1.1

### Step 4: Web UI access
- Initial Access, connect to the web ui over PFsenses ip address.
  something like this. https://192.168.1.1
- next you should:

  Change default credentials

  Verify WAN IP from ISP

  Confirm internet connectivity

### Step 5: DHCP config
- configure the IP address range and subnet
   it should look something like 192.168.1.2 through 192.168.1.100
- I would also suggest setting static ip's for certain devices that would need it. 
- You will need to map a devices MAC address to a specific IP.

### Step 6: Upgrade PFSense if Necessary
- After this step check if there is an upgrade needed for PFSense, it should be on the front page of the Web UI.
- Make the upgrade first if needed, I upgraded my version from 2.7.2 to 2.8.1.

## Step 7: Install Packages
- In the Web UI you can navigate to packages and download packages avaialable online.
- I downloaded PFblockerNG. 


# Issues I ran into on install

Realtek NIC compatibility
The ZimaBoard includes Realtek NICs, which can have driver and stability issues with pfSense (FreeBSD-based).
This can cause unreliable networking during installation or runtime.

 Solution: Used the included Intel NIC instead, which is better supported and more stable.

Recommendation: Prefer Intel NICs for any pfSense deployment.

pfSense 2.8 installer requires internet
Fresh installs of 2.8+ require an active internet connection to reach Netgate servers.
This blocked installation in an offline environment.

Solution: Installed pfSense 2.7.2 first, then upgraded to 2.8.1 from within the web UI.

Attempted software switching/bridging instead of a physical switch

Initially tried to use multiple pfSense NICs as a pseudo-switch using bridge mode.

Resulted in:
-complicated configuration
-packet drops
-TTL/time-to-live issues
-unreliable performance

Solution: Switched to a simple unmanaged physical switch.

This:
-simplified the topology
-improved stability
-reduced troubleshooting time
-Originally planned to segment IoT devices using VLANs, but the access point’s built-in network isolation features made this unnecessary for my use case.

Key takeaway:
When possible, keep the physical network simple:
Use Intel NICs,
Use a real switch,
avoid unnecessary network Bridges.
In the future, I will configure Vlans on a managed switch or on PFsense. It wasn't needed for my current homelab setup. 




