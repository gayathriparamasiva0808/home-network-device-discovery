# home-network-device-discovery
Performed network discovery and device identification using Nmap and ARP scanning in a virtualized Linux lab environment.
#  Home Network Device Discovery Lab

# Note: IP details have been modified for privacy and security purposes.

## Objective
To identify and analyze devices connected to a local home network using Linux-based networking tools in a virtual lab environment.


## Tools Used
- Nmap
- arp-scan
- net-tools
- Linux (VirtualBox environment)

---

## Lab Setup
- Host Machine: Windows
- Virtualization: VirtualBox
- Guest OS: Linux
- Network Mode: Bridged Adapter (to access real home network)

---

## Steps Performed

1. Identify Network Interface and IP Range
```bash
ip a

OUTPUT:

    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether XX:XX:XX:XX:XX:XX brd XX:XX:XX:XX:XX:XX
    

2. Install Required Tools

sudo apt update
sudo apt install nmap net-tools arp-scan

3. Discover Active Devices in Network

sudo arp-scan --localnet

-> Identified all active devices with IP and MAC addresses
-> Observed some devices with unknown vendors

OUTPUT:

192.168.0.1	XX:XX:XX:XX:XX:XX	(Unknown)
192.168.0.4	XX:XX:XX:XX:XX:XX	(Unknown)
192.168.0.6	XX:XX:XX:XX:XX:XX	(Unknown)
192.168.0.3	XX:XX:XX:XX:XX:XX	(Unknown: locally administered)
192.168.0.9	XX:XX:XX:XX:XX:XX	(Unknown: locally administered)

4. Perform Detailed Scan on Target Device
sudo nmap -A 192.X.X.X

Identified:
Open ports
Running services
OS detection
Example findings:
Port 80 (HTTP) open

5. Check Open Ports on Local Machine
 netstat -tulnp

OUTPUT:
tcp        0      0 XXX.XXX.XXX.XXX:53           XXX.XXX.XXX.XXX:*               LISTEN      -                   
tcp        0      0 XXX.XXX.XXX.XXX:631           XXX.XXX.XXX.XXX:*               LISTEN      -                   
tcp        0      0 XXX.XXX.XXX.XXX:53           XXX.XXX.XXX.XXX:*               LISTEN      -                   
tcp6       0      0 ::1:631                 :::*                    LISTEN      -                   

Listed active listening ports and associated services

Observations:
-> Multiple devices were identified in the network
-> Some devices appeared as "Unknown" due to MAC randomization or missing vendor database

Key Learnings
-> Understood how ARP scanning works in local networks
-> Learned to identify devices using IP and MAC addresses
-> Gained experience in using Nmap for service and OS detection
-> Understood limitations of vendor identification
