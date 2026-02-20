![Topology Diagram](https://github.com/furkangurses/LAN-Setup-Router-and-Switch-Interface-Configuration-CCNA-/blob/main/45.PNG?raw=true)

🎯 Lab Objective

Configure and verify interfaces on one router (R1) and two switches (SW1, SW2) within a single LAN.

Network: 172.16.0.0/16

Gateway: 172.16.255.254 (R1 G0/0)

The lab focuses on hostname configuration, IP addressing, speed and duplex settings, interface documentation, disabling unused ports, and saving configurations.

                172.16.0.0/16

                 R1
              G0/0 | 172.16.255.254
                    |
                  SW1
         -----------|------------
        |                        |
      SW2                     PC1, PC2
                                |
                             PC3, PC4

Devices

R1 – Default gateway for the LAN

SW1 – Distribution switch

SW2 – Access switch

PC1–PC4 – End devices

⚙️ Configuration Steps
1) Configure Hostnames

Router → R1

Switches → SW1, SW2

2) Configure IP Addressing
R1 – G0/0

IP: 172.16.255.254

Subnet: 255.255.0.0

Interface enabled with no shutdown

| PC  | IP Address | Subnet Mask | Default Gateway |

| --- | ---------- | ----------- | --------------- |

| PC1 | 172.16.0.1 | 255.255.0.0 | 172.16.255.254  |

| PC2 | 172.16.0.2 | 255.255.0.0 | 172.16.255.254  |

| PC3 | 172.16.0.3 | 255.255.0.0 | 172.16.255.254  |

| PC4 | 172.16.0.4 | 255.255.0.0 | 172.16.255.254  |

3) Configure Speed and Duplex

Manually configured on Gigabit interfaces:

speed 1000

duplex full

4) Add Interface Descriptions

Descriptions were added to document:

Inter-device links

Access ports

Unused ports

5) Disable Unused Interfaces

All unused FastEthernet interfaces were administratively shut down for security and best practice.

6) Save Configurations

Different save methods were used:

copy running-config startup-config

write memory

write

💻 Commands Used
🖥Router (R1)

enable

configure terminal

hostname R1

interface g0/0

ip address 172.16.255.254 255.255.0.0

speed 1000

duplex full

description ## to SW1 ##

no shutdown

interface range g0/1 - 2

description ## not in use ##

do show ip interface brief

show running-config

copy running-config startup-config

show startup-config

🖥Switch SW1

enable

configure terminal

hostname SW1

interface g0/1

speed 1000

duplex full

description ## to R1 ##

interface g0/2

speed 1000

duplex full

description ## to SW2 ##

interface range f0/1 - 2

description ## host ports ##

interface range f0/3 - 24

description ## not in use ##

shutdown

show interface status

write memory

show startup-config

🖥Switch SW2

enable

configure terminal

hostname SW2

interface g0/1

speed 1000

duplex full

description ## to SW1 ##

interface range f0/1 - 2

description ## host ports ##

interface range g0/2, f0/3 - 24

description ## not in use ##

shutdown

show interface status

write

show startup-config

🧠 Technical Explanation

This lab reinforces fundamental enterprise networking concepts.

Router interfaces are administratively down by default and must be enabled. Switch interfaces are enabled by default but should be managed for security. Proper Layer 3 addressing enables communication within the LAN. Speed and duplex must match on both ends to avoid performance issues. Configurations must be saved to persist after reboot.

🌍 Real-World Use Case

This configuration reflects a small office LAN deployment scenario.

It applies to new branch setups, lab environments, entry-level network engineering roles, and IT support infrastructure tasks involving router and switch initialization.

🛠️ Skills Gained

Cisco IOS CLI navigation

Interface configuration and verification

IP addressing implementation

Manual speed and duplex configuration

Interface documentation best practices

Bulk configuration using interface range

Configuration persistence management

🔮 Possible Improvements

Implement VLAN segmentation

Configure inter-VLAN routing

Enable SSH for secure remote management

Apply port security on access ports

Implement basic ACLs

Configure NTP and logging

🧩 Troubleshooting Notes

Use show ip interface brief to verify router interface status

Use show interface status on switches

Ensure speed and duplex match on both ends

Confirm no shutdown on router interfaces

Save configuration to avoid loss after reload

Packet Tracer may display auto-negotiation indicators inaccurately
