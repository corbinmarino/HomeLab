# Cybersecurity Enterprise Homelab Environment

## Introduction 
In pursuit of a hands-on learning environment at home, I embarked on the creation of a cybersecurity enterprise homelab. My primary objective for this homelab was to construct a simulated ecosystem that mirrors real-world enterprise scenarios, providing a platform for practicing the configuration and utilization of essential security tools. 

## Tools/Technology Used
- Firewall (pfSense)
- Malware Analysis VMs (Windows FlareVM)
- Windows 10 Host
- Windows 2019 Server AD
- Linux Server (DVWA)
- Kali Linux
- DFIR (Tsurugi Linux)
- SIEM (Security Onion)
- Vmware Workstation Pro

## Hardware
I am currently using an old MSI laptop (GS65) with the specs below: 
CPU: Intel® Core i7-9750H processor
RAM: 16 GB DDR4
GPU: NVIDIA GeForce GTX 1660Ti
HDD: 512 GB SSD
OS: Windows 11 (upgraded from Windows 10)

I decided to use this laptop as I was not getting any other use out of it and for this environment it works amazingly. 
## Network Topology
**![](https://lh7-us.googleusercontent.com/dVesbeWt3TgIZADH2al7GdVNs7-GIxWo3EDyQLk5ro5nj8f7PNBOoMFTQnKIvX6u3q_84jWZBgSPBY-OuSYLKYD94uu84MejG-kJGqepwRdVo2t5y_IevlXtLnC_-qznK2ltMlM8aVcy2nj9cuYsfXQ)
After VLAN segmentation and device separation by VLANs/subnets

## Management Network (VLAN 5)
The Management Network is where I can access the pfSense firewall web GUI. pfSense is an open-source firewall solution where I configured it to have six network interface cards (NICs). Five of these NICs are allocated to the distinct networks in the lab environment. These networks are the Corp WAN, Corp LAN, Security, Isolated, and the Management. The sixth NIC acts as the gateway connecting the homelab to the LAN network of my physical laptop, which allows the Management Network to access the pfSense firewall's web GUI for monitoring and configuration. This also serves as the gateway for connecting certain VLANs to the real internet, enriching the simulation with real-world data flows. 
[pfSense Configuration](https://github.com/corbinmarino/HomeLab/blob/main/Homelab%20Screenshots/pfSense%20Config%20Screenshots.md)

## Corporate Wide Area Network (VLAN 10)
The Corporate Wide Area Network serves as a "fake" WAN where I have a Kali Linux instance to simulate a potential malicious entity attempting to breach the corporate defenses. This network has restricted access to the homelab network, only allowing it access to the Corporate VLAN 20. This creates a secure testing ground for offensive security tactics while giving me a safeguard against accidental dissemination of malicious software or scripts beyond the WAN. 
[Kali Linux Configuration](https://github.com/corbinmarino/HomeLab/blob/main/Homelab%20Screenshots/Kali%20Machine%20Configuration%20Screenshots.md)


## Corporate Local Area Network (VLAN 20)
The Corporate Local Area Network mimics the infrastructure that "employees" would be accessing. This includes a Windows 10 workstation, a Windows 2019 Server and an Ubuntu Server. The Windows 10 workstation acts as a user endpoint within the corporate network configured with file and printer sharing, seamlessly joined to the Active Directory domain hosted by the Windows 2019 Server. This Windows 10 workstation becomes a potential target for offensive security exercises. As mentioned previously, the Windows 2019 Server is hosting key features such as Active Directory Domain Service, DHCP Server, DNS Server, File and Storage Services, and Remote Access. This server establishes user management and network orchestration within the LAN. The last piece in this Corporate LAN is an Ubuntu Server hosting the Damn Vulnerable Web Application (DVWA). This is an intentional vulnerable web application which offers a spectrum of vulnerabilities to explore, exploit, and fortify against. This web application also hosts a MariaDB instance. These components together create a great ground for defensive and offensive security skills. 
[Windows 2019 Server Configuration](https://github.com/corbinmarino/HomeLab/blob/main/Homelab%20Screenshots/Windows%202019%20Server%20Configuration%20Screenshots.md)
[Windows 10 Workstation Configuration](https://github.com/corbinmarino/HomeLab/blob/main/Homelab%20Screenshots/Windows%2010%20Workstation.md)
[DVWA Configuration](https://github.com/corbinmarino/HomeLab/blob/main/Homelab%20Screenshots/DVWA%20Configuration%20Screenshots.md)

## Security Network (VLAN 30)
The Security Network contains a digital forensics and incident response (DFIR) virtual machine called Tsurugi Linux, that comes equipped with a suite of tools designed to dissect and analyze possible security incidents. For the security information and event management (SIEM) solution, I went with Security Onion as I wanted to expose myself to a different SIEM (I have previous work experience with Splunk). Security Onion allows for Elastic Agents to be deployed using the Elastic Fleet on my Corporate LAN network devices for aggregation of event logs for host visibility. Security Onion also supplies the Corporate LAN network with network visibility from Zeek, Suricata, and other tools. All of these logs can be analyzed using the Security Onion SOC dashboard. 
[DFIR Configuration](https://github.com/corbinmarino/HomeLab/blob/main/Homelab%20Screenshots/DFIR%20Workstation%20Configuration%20Screenshots.md)
[SIEM Configuration](https://github.com/corbinmarino/HomeLab/blob/main/Homelab%20Screenshots/Security%20Onion%20Standalone%20Configuration%20Screenshots.md)

## Isolated Network (VLAN 40)
The Isolated Network contains VMs, in this case the Windows FlareVM for malware analysis. This is for static and dynamic malware analysis without other machines getting infected. the Windows FlareVM comes pre configured with essential malware analysis tools, allowing for a quick reverse engineering environment. Some of these analysis tools include disassemblers, debuggers, and sandbox solutions. 
[Windows FlareVM Configuration](https://github.com/corbinmarino/HomeLab/blob/main/Homelab%20Screenshots/Windows%20FlareVM%20Configuration%20Screenshots.md)

## Resources
[pfsense](https://docs.netgate.com/pfsense/en/latest/)
[FlareVM](https://github.com/mandiant/flare-vm)
[Windows Active Directory Server](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview)
[Kali Linux](https://www.kali.org/docs/)
[Tsurugi Linux](https://tsurugi-linux.org/)
[Security Onion](https://docs.securityonion.net/en/2.4/)
[Vmware Workstation Pro](https://docs.vmware.com/en/VMware-Workstation-Pro/index.html)
[Elastic](https://www.elastic.co/guide/en/fleet/current/elastic-agent-installation.html)
