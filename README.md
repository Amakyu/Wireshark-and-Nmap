# Wireshark and Nmap

## Objective
Perform network scans using Nmap and Zenmap on the 10.168.27.0/24 network block to identify active hosts, open ports, and vulnerabilities. Access the Kali Machine, run the scans, and analyze the results.

Monitor network traffic by analyzing packet capture (PCAP) files using Wireshark. Choose a PCAP file from the "Pcap Files" folder on the Kali Machine and examine it to detect anomalies such as ARP spoofing, HTTP, and TCP traffic patterns.

## Network Topology:
The network topology is a hybrid topology. This topology draws characteristics of the star, mesh and ring topologies and are best suited for a particular network. In this diagram, direct links with additional links to a unique node imply a blend of the star and mesh network making it a blend of the said network. I also used `nmap -sn 10.168.27.0/24` and found that there were 6 hosts on the network.
![nmapandwireshark1](https://github.com/user-attachments/assets/12ad440a-3f99-448a-a34f-eeb3ce3dfbe2)
*Ref 1: Network Topology*
![nmapandwireshark2](https://github.com/user-attachments/assets/9465fc5c-57b7-494f-b10d-ecfc4b1098b1)
*Ref 2: Network Scan*

## Nmap Vulnerabilities:
An advanced scan was done that scanned for the possible open ports, possible services running, and the operating systems on the network with the help of the command `nmap -sV -O 10. 168. 27. 0/24`. To some extent, this scan is also useful for identifying services that can either have outdated software or be misconfigured, which can attract security risks. 
 Regarding listening ports to various hosts, some hosts opened the following; Host: 192. 168. 183. 1 opened port 22/SSH, 80/HTTP, 135/MSRPC, Host: 192. 168. 183. 38 opened port 139/NetBIOS, Host: 192. 168. 183. 39 opened ports, 445/Microsoft-ds. The mentioned open ports can be abused if the services that are bound with these ports are not secure. During the scan the identification of some hosts with outdated software versions, for example OpenSSH 5. 5p1 Towards and Microsoft Windows Server 2008 R2. These are the previous versions that have vulnerability details which include features that hackers can exploit. The scan also showed several hosts with old operating systems such as the Windows Server 2008 R2 and possibly windows 7 or vista. These systems are at increased risk since they will not likely receive new security updates. Some of the detected services are Windows FTP service and Microsoft FTP service as well as FileZilla FTP. In case these services are not updated or the settings of these services are not correct, then such services can also be exploited. From these observations, recommendations of some security issues of concern that need to be examined in detail to evaluate specific threats and apply correct measures to mitigate them arise. 
![nmapandwireshark3](https://github.com/user-attachments/assets/43cba2db-cde5-43d7-be82-ca748772032d)
![nmapandwireshark4](https://github.com/user-attachments/assets/ee3de214-0ca3-4993-8918-f115fe82e26e)
*Ref 3 & 4: Advanced Network Scan*

### Wireshark Anomalies:
ARP Traffic Analysis
ARP analysis exposes several issues such as the frequent sending of requests from Microsoft_01:80:10 to different IPs which may be described as ARP flooding or from a wrongly configured device. This may suggest ARP spoofing whereby the attacker seeks to change his MAC address to correlate to the IP of another device by forwarding authentic ARP messages. 
![nmapandwireshark5](https://github.com/user-attachments/assets/c1f14385-4eee-47e9-bb20-e386e96f3928)
*Ref 5: ARP Traffic Analysis*
### HTTP Traffic Analysis
Captured HTTP data consists of GETs, POSTs, OPTIONSs and most connections are made with internal IPs (10. 168. 27. 10 & 10. 16. 80. 243) although some external connections are present. Despite no particular risk being apparent at first glance, the use of HTTP in the URLs as opposed to HTTPS could lead to all sorts of data being exposed easily. All major error codes are absent and all responses are either 200 OK, 304 Not Modified or 404 Not Found. Even then, 4xx and 5xx response codes may require further study and could possibly give out more problems. Those data- requests that deserve a closer look are the requests for the files connected to certificates (for instance, ‘disallowedcertsl1. cab’), the ‘robots. txt,’ the requests associated with the WebDAV such as PROPFIND.
![nmapandwireshark6](https://github.com/user-attachments/assets/113647d3-8260-452f-a1ff-95990409d364)
*Ref 6: HTTP Traffic Analysis*
#### TCP Traffic Analysis
TCP traffic with a large number of SYN packets may represent a SYN flood attack, in which an individual attempts to bring a server to its knees through the creation of half-open connections. Thus, many occurrences in the field may indicate scanning or attempts to modify existing links and connections.
![nmapandwireshark7](https://github.com/user-attachments/assets/7a8d301a-a4bc-4ac5-b8b9-0186c66feb16)
*Ref 7: TCP Traffic Analysis*

## Summary
The results of the Nmap scan show that there are large safety issues because of open ports, undisputed programs, and susceptible services. Any protocols that directly interface with the external world such as Ports 22(SSH), 80/443 (HTTP/HTTPS), and Windows networking ports(135, 139, 445) are especially vulnerable to brute force or malware or unauthorized access. It is equally ludicrous having old software such as OpenSSH 5. 5p1 & unpatched OS including Windows Server 2008 R2 are highly dangerous as their vulnerabilities are well-documented & they no longer receive updates. Further, prone facilities such as Microsoft FTP and FileZilla were also able to be penetrated to achieve unauthorized access. To avoid these risks, the organization needs to upgrade or acquire new systems, enforce user control, reduce unneeded services, demarcate the network and carry out security audits. Responding to such issues will strengthen the overall security position of your business. If a single host, for instance Microsoft_01:80:10, is sending abnormal ARP requests that could be higher than the standard requisite, it may lead to ARP spoofing or flooding thus disrupting the functioning of the network. HTTP traffic anomaly could indicate security threats such as malware, reconnaissance, or data leakage that may result in data breach, unauthorized control of a system, or compromised systems and data; performance anomalies such as DoS and other resource depletion. About operating issues there are false positives that lead to alert fatigue and the missing of threats. This is evident from the fact that TCP flows samples exhibit situations where re-transmissions are apparent due to high congestion in the network and SYN flood indicators or bizarre ports which may present unauthorized services or DoS attacks.

## Recommended Solutions
To mitigate the risks of the presentation of older Windows Server editions, it is suggested to update the server to the current version such as Windows Server 2019 or 2022 to avail continued security patches and updates. Or, the migration to Microsoft Azure can extend up to three more years of important security updates for free to plan a definite long-term upgrade approach. New software with new hardware as well as the installation of a new OS with migrating data can increase security, dependability, and speed. For, urgent requirement, the users can opt for Extended Security Updates as they can avail a few critical updates on an emergency basis before finalizing a complete redesign plan. 
One of the critical steps is identification, as well as categorization of migration priorities, data backup and the use of tools and technologies like Microsoft Assessment and Planning (MAP) toolkit. Using cloud services and, therefore, introducing suitable cloud services in cooperation with Microsoft or other service providers can also help to consolidate further. Support for older operating systems comes to an end and rapid action is required to address security and compliance issues The upgrade process requires its planning with great attention paid to specifics of your organization environment.
To improve the network security, the first thing one does is: Check the updates for all the operating systems and application softwares, shut down the unnecessary ports and install firewalls and IDS to monitor traffic for any anomaly. These are the features that need constant system audits and patches to remove all the exposed shortcomings. 
For ARP traffic, it is recommended to enable Dynamic ARP Inspection (DAI) that would filter ARP packets against a trusted database to prevent ARP spoofing, and to configure static ARP for critical device(s). ARP attack effects can also be minimized by dividing the network based on VLANs that offer network segmentation. 
For acquiring HTTP traffic, increase the capture duration, target POST requests, and analyze the possibilities of reconnaissance in OPTIONS requests. Give special attention to both ingress and egress traffic, use DPI for a more detailed detection of the content of the stream and block traffic for specific URIs. Abnormal user-agent strings should also be examined and analyzing traffic against server log allows one to have a look at overall activity. 
For TCP traffic turn on syn flood protection, apply filter on TCP traffic, and identify through IDS anomalous traffic such as repeated retransmission or scan. These steps reduce various attacks that are linked to TCP based connections. 
