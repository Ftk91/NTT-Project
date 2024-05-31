# NTT-Project

In this lab I simulated working for a small MSP that was hired to build a small business enviroment

Tools used in this lab
----
* GSN3
* Wireshark
* Greenbone

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

I then verified the configuration applied correctly

![Fortigate 2](https://github.com/Ftk91/NTT-Project/assets/170447276/bf1a5329-c88f-43bb-8f1e-3c76dab5b229)

Next I configured the DHCP server for the LAN interface

![Fortigate 3](https://github.com/Ftk91/NTT-Project/assets/170447276/a8075e8c-6520-4b3f-990f-e67f82ceec80)

I again verified the configuration and verified the workstation has leased a DHCP address

![Fortigate 4](https://github.com/Ftk91/NTT-Project/assets/170447276/d67ec68a-fc80-4d92-80d1-8ef56af4b687)

![Fortigate 4](https://github.com/Ftk91/NTT-Project/assets/170447276/dc70ecc9-a78f-4347-aa4c-96a10afb425c)

Next I connected to the Fortigate GUI and setup a hostname, Timezone, enabled NTP allowing LAN and DMZ devices to sync time with the firewall, updated the idle timeout time just so I didn't have to constantly login, and enabled auto file system check to prevent warning messages due to unclean shutdowns. Once settings were applied I made sure to created a backup and rebooted the firewall.

![Fortigate 5](https://github.com/Ftk91/NTT-Project/assets/170447276/53e83cf3-2db9-4d13-80c9-2d51ad3635ad)

Next I configured the network interfaces per the clients request and configured DNS

* 10.128.0.0/24 as the LAN network
* 10.128.99.0/24 as the GUEST network
* 10.128.10.0/24 as the DMZ network

![Fortigate 6](https://github.com/Ftk91/NTT-Project/assets/170447276/67e11d00-6b14-49db-8e00-9afcb6a3eed5)
  
![Fortigate 7](https://github.com/Ftk91/NTT-Project/assets/170447276/78cb69b5-cde8-4c46-b5c6-d0ca9a5e09cc)

![Fortigate 8](https://github.com/Ftk91/NTT-Project/assets/170447276/72ad5362-728e-459e-9dc8-35755666b06f)

I then created 2 different service groups LAN service group and DMZ service group

| LAN members   | DMZ members   |
|:-------------:|:-------------:|
| ALL_ICMP      | ALL_ICMP      | 
| NTP           | FTP           | 
| RDP           | RDP           | 
| SSH           | SSH           |
| Web Access    | Web Access    |
| Windows AD    |               |

![Fortigate 9](https://github.com/Ftk91/NTT-Project/assets/170447276/767f01f1-6dce-4369-8fc4-d900c8032ebd)

Lastly I configured firewall rules and backed up changes

![Fortigate 10](https://github.com/Ftk91/NTT-Project/assets/170447276/7cc86517-ad09-4bf6-8f4a-3454ba0a6c48)

# Stage 2 - Domain Setup

Preparing Win2012r2 server for Active Directory Domain Services role I logged in to the server and setup a static IP Address, sync the time on the LAN interface with the firewall, and change hostname to dc

![Stage 2 11](https://github.com/Ftk91/NTT-Project/assets/170447276/36226bc0-b166-461c-8220-124d18efb993)

![Stage 2 1](https://github.com/Ftk91/NTT-Project/assets/170447276/18da0755-16fe-4778-958f-3e4da3882624)

![Stage 2 2](https://github.com/Ftk91/NTT-Project/assets/170447276/15062ee6-8cfe-469d-bfd2-686d437d750e)

![Stage 2 3](https://github.com/Ftk91/NTT-Project/assets/170447276/7803df49-5b40-417a-acdc-9f1eb49d4274)

Then I installed Active Directory services following Microsofts guide and named the domain widgets.localdomain per clients request

[Building Your First Domain Controller on 2012 R2](https://learn.microsoft.com/en-us/archive/technet-wiki/22622.building-your-first-domain-controller-on-2012-r2) 


Once installed I created domain user accounts and domain admins account to manage the enviroment. I added the admin account to the domain admin group

![Stage 2 7](https://github.com/Ftk91/NTT-Project/assets/170447276/f81c06f3-b0a3-46d6-bc8d-80851c2e11e9)

![Stage 2 8](https://github.com/Ftk91/NTT-Project/assets/170447276/f3d01924-62e8-4ed0-8019-896325746246)


I then prepared the Windows 10 workstation to join the domain by changing the hostname, changing the primary DNS server to the IP of the domain controller, and setting the NTP by syncing with dc.widgets.localdoamain.

![Stage 2 4](https://github.com/Ftk91/NTT-Project/assets/170447276/be1fe23f-d413-498a-b402-dd8b0873ae57)

![Stage 2 5](https://github.com/Ftk91/NTT-Project/assets/170447276/5fabf2f1-0072-47e4-9db1-8a784bd34f79)

![Stage 2 6](https://github.com/Ftk91/NTT-Project/assets/170447276/56d41788-8618-4773-9b13-51c68bd4252d)

Finally I joined the Windows 10 workstation to the domain

![Stage 2 9](https://github.com/Ftk91/NTT-Project/assets/170447276/2017b243-65b8-4146-85b4-aaf94b150aba)

To differentiate user accounts and admin accounts I deployed desktop background wallpaper using group policy

![Stage 2 10](https://github.com/Ftk91/NTT-Project/assets/170447276/2055ff04-4470-40ec-a519-6371bdd04d69)

# Stage 3 - IIS Setup




