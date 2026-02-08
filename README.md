# Pfsense-HomeLab-Configuration

Instructions on setting up Pfsense in my personal homelab. 


What is PFsense? 

pfSense is a free, open-source firewall and router software distribution based on FreeBSD that provides enterprise-grade network security and management. It is installed on physical computers or virtual machines and managed via a web interface.

Here is a link to the netgate documentation page:
[Pfsense Docs](https://docs.netgate.com/pfsense/en/latest/)

First I will begin with the basic steps for setting up pfsense 2.7.2 Community Edition, then the upgrade to 2.8.1. then I will break down the issues I ran into during my installation, and how I had to change my plans to fix them. 


PFSense Installation Steps:
- The first step depends on your current network configuration. I had a ISP provided all in one router/access point/modem. First I had to connect to the web UI. You need to find the IP address of the router and connect to the web UI, if you havent changed anything the log in credentials should be default. You can usually find the default credentials online or on the router. You will need to change it to bridge mode, it should have one port labeled differently than the rest, that will usually be the new WAN port you can connect your new pfsense router to. Once in bridge mode it should only act as a modem.
- I would suggest installing it on bare metal first, a device that has display, then switching to a ethernet connected device that can access the PFsense web UI. 
- The new installation of Pfsense version 2.8 and newer can be a pain because it requires an internet connection to connect to the netgate servers during install. The work around I had was to install the old 2.7.2 community edition, I already had the old ISO on a usb drive. You can download the ISO online and flash it to a drive using Balena Etcher.
- Once the drive has the ISO on it, you plug it into whichever device you are going to install PFsense on. I had a zimaboard that I planned on running PFsense on.
- During the process it should ask you to assign WAN and LAN ports for use. (If you are installing version 2.8 or newer fresh, you wont be able to proceed without an active internet connection)
- Once installed you should see the ip address of the PFsense router. Restart the web ui and then try to connect to it locally through the ip address in a browser. It will also have its defualt credentials, make sure you change them to new ones.
- Once inside the webgui, you need to make sure you are getting an IP address from your ISP for your router.
- Once you have an IP address, the easiest next steps to setting up your network is an ethernet connection from the LAN of PFsense to a switch, then you can add and conifgure an access point. 

