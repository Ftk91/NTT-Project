# NTT-Project

In this lab I simulated working for a small MSP that was hired to build a small business enviroment

Tools used in this lab
----
GSN3
Wireshark
Greenbone

The client in this scenario requested

* a secure network
* an internal Windows Domain
* an internal Microsoft IIS webserver
* an internal Windows 10 workstation
* a public webserver
* a public FTP server
* a LAN network on 10.128.0.0/24
* a DMZ network on 10.128.10.0/24
* a GUEST network on 10.128.99.0/24

# Stage 0 - Beginning topogoly 

![Stage-0](https://github.com/Ftk91/NTT-Project/assets/170447276/f7166442-d400-4640-8875-65a016036231)


----

# Stage 1 - Network Setup

In Stage 1 I added and configured Fortigate firewall, LAN Switch, DMZ Switch, and Windows 10 workstation resulting in the topology below

![Stage-1](https://github.com/Ftk91/NTT-Project/assets/170447276/71d92734-67db-4a8b-b600-c7e124e5c6f7)

## Fortigate Firewall Configuration
----

Per the client request they requested LAN to configured to 10.128.0.0/24

![Fortigate 1](https://github.com/Ftk91/NTT-Project/assets/170447276/f7affebe-c446-4daa-95dc-89a16834de4f)

I verified the configuration applied correctly

![Fortigate 2](https://github.com/Ftk91/NTT-Project/assets/170447276/bf1a5329-c88f-43bb-8f1e-3c76dab5b229)





