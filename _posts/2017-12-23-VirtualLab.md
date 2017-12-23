# Virtual Lab
To prevent me destroying my own computer. It is a good idea to run experiments in a virtualized environment. I am using Windows because my laptop was shipped with it. I will eventually switch to a linux Host someday.

I chosed [Virtual Box] because it is practically free of charge and it can take snapshots. Whenever things go wrong, I can always revert back to an earlier snapshot.

# ISO ?
ISO are CDs that installs an Operating System. 
They are a bit more problematic than getting a preconfigured Virtual Machine image. Do not be worried because there are many online installations guide with screenshots. 

# Where can I get preconfigured VMs ?
Most preconfigured Linux VM images can be obtained from [OSBOXES].
Kali Linux Virtualbox image can be download from [Kali Website].

One disadvantage over using an ISO would probably be that the size of the disk has been configured and it would take up more than what you actually need.

# Virtualbox Networking
In Virtualbox, there are a few types of networking.
The following table from [Chapter 6 of VirtualBox Manual] is the most useful.

![Vbox Table]
![Vbox Diagram]

## NAT networking
This is the default configuration.
Think of it this way: 
- It treats your "host" like the router.
- The VM is hidden behind your host with *Network Address Translation* (KIV).
- Each VM is isolated from each other. Their only connection is to the "host". 
- VM will have Internet Access via the "host".

I mainly use this networking configuration. 
If I happen to need a connection back as a *reverse shell* (KIV),
I can employ port forwarding to allow a connection back to my Kali, similar to how routers can do a port forwarding.

## NAT Network networking
This is similar to NAT but instead of each VM being isolated, they are all in 1 single network.
- Each VMs can communicate with one another.
- They also have Internet Access via the "host".

## Host-only networking
This is similar to NAT Network but instead you have no internet access.
- Each VMs can also communicate with one another.
- They can communicate with the "host"

I would typically use this when I have a need to cut off the internet.

## Internal networking
This is complete isolation of the VMs from both Internet Access and to the Host. 
I supposed this is the optimal configurations when dealing with very malicious things like analysing viruses. I would like to look into Sandboxie one day and figure out their differences.

In this configuration, there is a need to set up our own VirtualBox dhcpserver which can be done as follows:
```cmd
vboxmanage dhcpserver add --netname TestingLab --ip 192.168.160.1 --netmask 255.255.255.0 --lowerip 192.168.160.2 --upperip 192.168.160.10 --enable
```

### What is a DHCP server?
In short, DHCP server is the server that assigns IP address dynamically to computers in a network. Benefit is that you don't have to deal with underlying ip address conflicts unlike static IPs.

[OSBOXES]:http://www.osboxes.org/
[Virtual Box]:https://www.virtualbox.org/wiki/Downloads
[kali Website]:https://www.offensive-security.com/kali-linux-vmware-virtualbox-image-download/
[Chapter 6 of VirtualBox Manual]:https://www.virtualbox.org/manual/ch06.html
[Vbox Table]:{{ '/assets/VboxTable.png' | absolute_url }}
[Vbox Diagram]:{{ '/assets/VboxDiagram.png' | absolute_url }}