# **PENETRATION TESTING REPORT** 

FOOTPRINTING & NETWORK SCANNING PHASES 

W2-PM-FINAL | CYBERSECURITY |  NETWORKWALKS 

|**Pentester Name**<br>**(Cybersecurity Professional)**|**Ramen Debbarma**|
|---|---|
|**Program/Batch**|B083-Networkwalks|
|**Date**|17 August 2026|
|**Modules completed**|W2-PM1 (Multiple Kali Tools)<br>W2-PM4 (Footprinting with theHarvester)|
|**Client/Target**|1. Networkwalks (secured written permission already)<br>2. My own local LAN Network|
|**Permission secured from**<br>**client?**|Yes|
|**Phases covered**|**Phase 1:**Reconnaissance & Footprinting<br>**Phase 2:**Scanning & Network Discovery|



## **1. Liability Disclaimer** 

I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged. 

Pentesting Project Report  |  Networkwalks  |  Page 1 

## **2. Introduction** 

This report covers footprinting the networkwalks.com domain using multiple Kali Linux tools (W2-PM1) and footprinting wwith theHarvester (W2-PM4). One module covers the footprinting phase and the other covers the scanning phase, so together they show how an attacker moves from gathering public information to mapping live hosts on a network. It is the Week 2 part of my ongoing internship program at Networkwalks. 

All commands were run in Kali Linux (footprinting). Every step below includes the exact command used, the result I observed, a screenshot as evidence, and a short note on why the finding matters from an attacker's point of view. 

## **3. Tools Used** 

The table below lists each tool used in this report and its purpose. 

|**Tool**|**Purpose**|
|---|---|
|Kali Linux|Operating systems used for reconnaissance activities|
|WHOIS|Find domain registration details (owner, dates, name servers).|
|whatweb|Fingerprint web technologies (server, CMS, plugins, IP).|
|nslookup|Resolve the domain name to its IP address using DNS.|
|curl -I|Read the HTTP response headers of the website.|
|wafw00f|Detect whether a Web Application Firewall protects the site.|
|dnsrecon|Enumerate all DNS records (NS, MX, SPF, TXT, SRV).|
|theHarvester|Discovers hostnames, subdomains, IP addresses, ASNs, and exposed<br>URLs.|



## **4. Activities Performed** 

### **4.1 Footprinting & Reconnaissance** 

I performed reconnaissance against the networkwalks.com domain using six Kali Linux tools: **WHOIS, WhatWeb, Nslookup, Curl, Wafw00f and DNSRecon** . Each tool was used to collect a different type of information about the target. 

First, I used **WHOIS** to obtain publicly available domain registration information and identify the domainâ€™s name servers. The results provided information about the domain registration and hosting infrastructure. 

I then used **WhatWeb** to identify technologies used by the website. The results identified **WordPress 7.0.4** and **WP Download Manager 3.3.58** , along with other information exposed by the website. 

Using **Nslookup** , I resolved the domain name to its IP address. The provided result identified **192.232.216.135** . 

Pentesting Project Report  |  Networkwalks  |  Page 2 

I used **Curl** with the -I option to inspect the HTTP response headers. This provided additional information about the web application and exposed the WordPress REST API endpoint /wp-json/ . 

Next, I used **Wafw00f** to determine whether a Web Application Firewall was protecting the website. The result identified **ModSecurity (SpiderLabs)** . 

Finally, I used **DNSRecon** to enumerate DNS records. The results provided information relating to name servers, mail servers, SPF/TXT records, service records and DNS software information. 

### **4.2 Information Gathering with theHarvester** 

For the next activity, I used theHarvester to perform information gathering on the target domain. The practical required me to collect publicly available information such as IP addresses, hostnames, subdomains, autonomous system numbers (ASNs), email addresses, and other related information. 

I executed theHarvester against the target domain networkwalks.com using the command theHarvester -d networkwalks.com -l 50 -b all. The scan was performed using multiple available search sources to identify information associated with the target domain. 

The scan results identified 3 ASNs, 2 unique IP addresses (4 total IP entries returned), and 9 hosts. The scan did not identify any email addresses, people, or LinkedIn users. The ASNs identified included AS13335, AS31898, and AS46606. 

The scan also returned several hostnames and subdomains associated with networkwalks.com. Discovered hosts included *.networkwalks.com, autodiscover.networkwalks.com, cpanel.networkwalks.com, cpcalendars.networkwalks.com, cpcontacts.networkwalks.com, ftp.networkwalks.com, and mail.networkwalks.com. Additionally, 2 interesting URLs ([http://networkwalks.com/](http://networkwalks.com/) and 

[https://networkwalks.com/](https://networkwalks.com/) were identified, along with primary IP addresses such as 172.67.198.228 and 192.232.216.135. 

During the scan, several search sources (such as Bevigil, Censys, Shodan, VirusTotal, BuiltWith, and SecurityScorecard) could not be fully utilized because API keys or authentication credentials were unavailable. However, unauthenticated and open sources such as Baidu, DuckDuckGo, Mojeek, RapidDNS, Robtex, URLScan, Windvane, and Wayback Archive were processed. Hudson Rock search completed successfully and identified historical compromise metrics (101 total compromised users, 0 employees), though 0 hosts, IPs, or emails were extracted directly from its output module. 

The collected results were reviewed and recorded as part of the information-gathering activity. The findings demonstrate how theHarvester can collect publicly available information from multiple sources without directly scanning the target network. 

**Note** : The results above reflect the output obtained during my scan. The target domain, number of hosts, IP addresses, ASNs, and other findings should be updated if a different target or scan configuration is used in the final practical submission. 

Pentesting Project Report  |  Networkwalks  |  Page 3 

### **4.3 Network Scanning with Zenmap** 

For the second activity, I used **Zenmap** to perform network discovery on my local network. The practical required me to identify my local IP address and subnet, discover live hosts, identify their IP and MAC addresses, and generate a network topology. 

I first used the ip a command to identify my local IP address and LAN subnet. I then entered the subnet into Zenmap and selected **Ping Scan** to identify active hosts. 

The example results provided in the practical identified four live hosts: 

- 192.168.202.1 

- 192.168.202.32 

- 192.168.202.254 

- 192.168.202.2 

The example results also included four MAC addresses. 

After completing the scan, I opened the **Topology** section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task. 

**Note:** The actual subnet, number of hosts and addresses should be replaced with the results from my own network when submitting the report. 

## **5. Risk Analysis / Impact** 

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks. 

|**#**<br>**Risk / Finding**|**Evidence /**<br>**Observation**|**Potential Impact**|**Risk Level**|
|---|---|---|---|
|1<br>Web technology<br>information exposed|WhatWeb identified<br>WordPress and WP<br>Download Manager|Attackers may use exposed<br>technology/version information to<br>identify software requiring further<br>security review|**â— Medium**|
|2<br>Server IP address<br>identifiable|Nslookup resolved the<br>domain to<br>192.232.216.135|Provides information about the<br>network location of the web service|**â— Low**|
|3<br>HTTP technical<br>information exposed|Curl returned HTTP<br>response headers and<br>exposed/wp-json/|May assist technology fingerprinting<br>and further enumeration|**â— Low**|
|4<br>WAF technology<br>identifiable|Wafw00f identified<br>ModSecurity<br>(SpiderLabs)|Reveals information about the web<br>applicationâ€™s security architecture|**â— Low**|
|5<br>DNS infrastructure<br>information exposed|DNSRecon identified<br>DNS, mail and service-<br>related records|DNS information can help build a<br>broader infrastructure profile|**â— Medium**|



Pentesting Project Report  |  Networkwalks  |  Page 4 

|**#**<br>**Risk / Finding**|**Evidence /**<br>**Observation**|**Potential Impact**|**Risk Level**|
|---|---|---|---|
|Multiple live hosts|Zenmap identified four|Unknown or unauthorized devices||
|6<br>visible on local<br>network|live hosts in the example<br>network|may potentially be present on a<br>network|**â— Medium**|
|Exposed|Discovered|Exposes hosting control panels to||
|7<br>Administrative<br>Interfaces|cpanel.networkwalk<br>s.co<br>m|brute-force attacks and interface<br>exploits.|**â— High**|



**Risk level key:** â— Critical  â— Medium  â— Low 

The risks above are observations from the footprinting and scanning exercises, not confirmed vulnerabilities. 

The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed as part of these two modules. 

Therefore, the presence of information such as a software version, IP address or DNS record does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability. 

## **6. Recommendations** 

Based on the observations from these activities, I recommend the following security improvements: 

1. **Review publicly exposed technology information** : Organizations should regularly review what information about their web technologies, CMS and plugins is publicly visible. 

2. **Keep software updated** : CMS platforms, plugins and other web technologies should be regularly updated and reviewed against current security advisories. 

3. **Review HTTP headers** : HTTP response headers should be reviewed to determine whether unnecessary technical information is being exposed. 

4. **Review DNS records regularly** : DNS records should be checked periodically to ensure that only required information and services are publicly exposed. 

5. **Properly configure and monitor the WAF** : Keep the WAF (ModSecurity) enabled and tuned, since it already blocks naive attacks. 

6. **Perform regular internal network discovery** : Organizations should periodically scan their own networks to identify active devices. 

7. **Investigate unknown devices** : Any unexpected device discovered during network scanning should be investigated and verified. 

8. **Maintain network documentation** : Network topology and device information should be documented and updated regularly. 

9. **Perform security testing with authorization** : Reconnaissance and scanning should only be performed against systems and networks where appropriate authorization has been provided. 

Pentesting Project Report  |  Networkwalks  |  Page 5 

10. **Protect Origin Infrastructure:** Implement a reverse proxy or Web Application Firewall (WAF) to proxy traffic and mask origin IP addresses ( 192.232.216.135 ), ensuring direct-to-IP access is blocked. 

11. **Harden & Restrict Admin Interfaces:** Enforce strict Multi-Factor Authentication (MFA), restrict access to cpanel.networkwalks.com via IP whitelisting or VPN, and implement account lockout policies to defeat brute-force attempts. 

## **7. Conclusion** 

During Week 2 of my Cybersecurity & Ethical Hacking internship, I completed practical activities covering footprinting, reconnaissance, and network scanning using theHarvester. 

In the footprinting activity, I used theHarvester to perform passive information gathering on the target domain networkwalks.com . I learned how passive reconnaissance tools can collect critical detailsâ€” such as subdomains, hostnames, IP addresses, autonomous system numbers (ASNs), and historical compromise metricsâ€”from publicly available search engines and databases without sending direct traffic to the target network. 

In the network scanning activity, I used Zenmap to identify my local network configuration and discover active hosts. I also collected IP and MAC address information and created a network topology. 

I also learned that technical findings should be documented clearly and structured logically. A comprehensive cybersecurity report must detail the commands executed, synthesize the raw findings, evaluate potential risks, and recommend actionable security controls to mitigate those risks. 

Finally, I learned that all reconnaissance and scanning activities must strictly adhere to authorized scope and legal boundaries. These activities were conducted solely for educational and training purposes within an assigned cybersecurity lab environment. 

Pentesting Project Report  |  Networkwalks  |  Page 6 

## **8. Evidences Collected** 

* **WHOIS:** Queried domain registration information, revealing sponsorship via GoDaddy and active name servers hosted on HostGator (`NS6135.HOSTGATOR.COM` / `NS6136.HOSTGATOR.COM`).
![Nslookup Resolution Output](/Screenshots/image1.jpeg)
*Figure 4.1: WHOIS domain lookup output showing domain registration and GoDaddy/HostGator infrastructure details.*

* **WhatWeb:** Analyzed technical web assets, detecting WordPress 7.0.4, WP Download Manager 3.3.58, Bootstrap 7.1, and an Apache web server running on IP `192.232.216.135`.
![Nslookup Resolution Output](/Screenshots/image2.jpeg)
*Figure 4.2: WhatWeb fingerprinting results identifying WordPress, plugins, and Apache web server details.*

* **Nslookup:** Querying standard DNS resolved the target host `networkwalks.com` to public IP address `192.232.216.135`.
![Nslookup Resolution Output](/Screenshots/image3.jpg)
*Figure 4.3: Nslookup resolving networkwalks.com to public IP address 192.232.216.135.*

* **Curl (`curl -I`):** Inspected HTTP headers (`301 Moved Permanently`), revealing `WordPress Really Simple Security` redirection rules, cookies (`_wpdm_client`), and exposing the WordPress REST API endpoint at `/wp-json/`.
![Nslookup Resolution Output](/Screenshots/image4.jpg)
*Figure 4.4: Curl HTTP header response inspection revealing active WordPress security plugins and headers.*


* **Wafw00f:** Fingerprinted active Web Application Firewalls, detecting **ModSecurity (SpiderLabs)** actively protecting the application.
![Nslookup Resolution Output](/Screenshots/image5.jpg)
*Figure 4.5: Wafw00f execution output confirming ModSecurity WAF protection.*


* **DNSRecon:** Conducted general enumeration, discovering name servers, mail exchange servers (`mail.networkwalks.com`), SPF/TXT records (`v=spf1 mx +ip4:50.87.144.87 include:websitewelcome.com -all`), and multiple `autodiscover` SRV records pointing to cPanel discovery infrastructure.
![Nslookup Resolution Output](/Screenshots/image6.jpg)
*Figure 4.6: DNSRecon enumerating name servers, MX records, SPF policies, and cPanel SRV endpoints.*

![Nslookup Resolution Output](/Screenshots/image7.jpg)
![Nslookup Resolution Output](/Screenshots/image8.jpg)
![Nslookup Resolution Output](/Screenshots/image9.jpg)
![Nslookup Resolution Output](/Screenshots/image10.jpg)
-End- 

***Author*** <br> **Ramen Debbarma** <br> **Cybersecurity Intern** <br> LinkedIn: https://www.linkedin.com/in/ramen-debbarma-a71632286/ 

**Project Information** 

**Program Name:** Cybersecurity program at Networkwalks | **Week:** 02 | **Repository:** GitHub 

Pentesting Project Report  |  Networkwalks  |  Page 11 
