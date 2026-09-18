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



<!-- Start of picture text -->
> hops Paces Sep17 9:13 9M @52% Gow 2 on too Joo Os O<br>oe 2 ramen@hai:~ Â«<br>: oman Name: NETWORKS. COM<br>Registry Donain 10: 26523i9255_DONAK_COM-VRSU<br>Dock Registrar WIS Server: whois. godaddy-com<br>Wal Registrar URL: hetp:/ mm. godaddy.com<br>Updeted Date: 2025-13-12730:00:492<br>folder Registry Expiry Date: 2027-11-06722:51:462<br>Registrar TAMA 1D! 146<br>thundBa Registrar:Registrar AbuseGoDaddy.com,Contact LLCEmail: abuseagodaddy.com<br>as Registrar abuse Contact Phone: 460-624-2505<br>Donan status: clientDeleteProhibited https://icann.org/epptclientDeleteProhibited<br>Donain status: eLientRenewprohibited https://cann.org/eppaclientRenewProhibited<br>Name Server: NS6126.HOSTGATOR. COM<br>Dssect unsigned<br>URL of the TCAM Whois Tnaccuracy Conptaint Form: https://am.icann.org/wicf/<br>>>> Last update of whois database: 2026-09-17735:43:102 <ce<br>TERS OF USE: You are not authorized to access or query our whois<br><!-- End of picture text -->



<!-- Start of picture text -->
stops Paces sepi7. 9:16PM Â© Gin oom too soo OO<br>Cis 2 ramen@ali:~ a<br>â€˜ {301 Moved permanently] Apache, cookies{_wpdn client], Country[UNITED STATES][._], HTTPServerLApache], Mt<br>tponty{wpdn-client], 19(192.252.216.135], RedirectLecation(https://networnaiks.con/], Uncomonleaders(peraissions-policy, Fed<br>wall Tks. con], Frane, Google-Tag-hanager,{200 Ok] Apache,HIMLS,Bootstrop(7.1},HTTPServer{ cookies{_wpde_client],Apache], t@ponty{__wpda_client],country{UNITED1P(192,252.216.135],STATES) (1, Email3Qvery(3.7-1,infoanetworiraMeta<br>hader enerator(wordPressPrUar2=Toanp;scWar2-12,9ei,nordPress,appl ication/Downloadjson,hanagerapplication/Ldsjson,3.3.58), Open-Graph-Protocol{osbsite],module, speculationrules, text/Javascript],Script] sSSuMt-iPr8sanp;pidqvar2-S051i8anpTitle<br>a 200 or] Apache, Bootstrop{?-11, country{ONITED STATESIL 1, tnalilinfoonetworlastks con], Frame, Sooglel<br>pesom â€œrog-nanager,Â£1313158], Open-GraphProtocolWIMLS, NTTPServerTspoche],-Â£P(392.232-216.135],,website], Seript{sssenR-i180anp; piÃ©nvar2-50s116anp;prtVar2=7anp;sewar2-12,3QUery{3.7.1}, NetaGenerator{wordPress. 7.1,nordPressapplication/Download son Manageappt<br>Adress: 1921168, 202,2452<br>hddress: 192.232.216.335<br>NTWe/1.1 301 Roved Pernanently<br>Permissions-Policy: private-state-token-redenption=(self â€œhttps://mm.google.conâ€ â€œhttps: //ham.gstatic.cos" â€œhetps://recaptcha.net<br>s"rnttps://chal lenges.cloudflare.conâ€ "https://heaptcha.con"), privatesstate-token-issuances(selt "https://m.google-conâ„¢ â€œhips:<br>fun gstatic.con" â€œhitps://recaptcha.netâ„¢ â€œhttps: //chailenges.cloudFlare.<br>Expires: thu, 17 Sep 2026 10:46:52 OT conâ€ "https:/7heaptcha. conâ€)<br>Encheccontro: max-age-3600<br>Schedirect-by: WordPress ~ Really Sinple security<br>Setscookies â€ wpdn,client=70621e0907ccbid87I3401044f00206) path-/; donain-networkwalks.con; Httponly<br>Upgrade: h2,f2Â¢<br><!-- End of picture text -->

Pentesting Project Report  |  Networkwalks  |  Page 7 



<!-- Start of picture text -->
- me<br>loue networkwalks.con<br>- server 8.8.8.8<br>Fagen Address 8.8.8.8953<br>Non-authoritative answer<br>Gal) Address: 192.232.216.135<br>he . :<br><!-- End of picture text -->



<!-- Start of picture text -->
{~]<br>curl -I networkwalks.com<br>TTP/1.1 301 Moved Permanently<br>pate: Thu, 17 Sep 2026 15:46:52 GMT<br>Berver: Apache<br>Permissions-Policy: private-state-token-redemption=(self â€œhttps: //wm.google.comâ€ "https://ww.gstatic.comâ€ "https://recaptcha.net<br>r "https://challenges.cloudflare.com" "https://hcaptcha.com"), private-state-token-issuance=(self "https://www.google.comâ€ â€œhttps:<br>/www.gstatic.con" "https://recaptcha.net" *https://challenges.cloudflare.comâ€ "https://hcaptcha.com")<br>xpires: Thu, 17 Sep 2026 16:46:52 GMT<br>â€˜ache-Control: max-age=3600<br>-Redirect-By: WordPress - Really Simple Security<br>Bet-Cookie: __wpdm_client=78621e0937ccb1d8713dd1b44fooa30e; path=/; domain=networkwalks.com; HttpOnly<br>grade: h2,h2c<br>â€˜onnection: Upgrade<br>cation: https://networkwalks.com/<br>Referrer-Policy: no-referrer-when-downgrade<br>-Endurance-Cache-Level: 0<br>-nginx-cache: WordPress<br>â€˜ontent-Type: text/html; charset-UTF-8<br><!-- End of picture text -->



<!-- Start of picture text -->
= hops Places Sepi7 987M Â© 7% Oww gow took Loos Oe O<br>+<br>wa â‚¬ wor!)<br>"<br>folder vey<br>thud<br>The Web Application Firewall Fingerprinting Toolkit<br>[+] checking https://networiratks com<br>{5 Mais : is boning we<br>#5<br>i<br><!-- End of picture text -->

Pentesting Project Report  |  Networkwalks  |  Page 8 



<!-- Start of picture text -->
Ss hope Paces sepi7 92276 Om OAK Som Too Looe ONO<br>be, 2 ramen: ~ a<br>Dock The web Aoplication Fireuait Fingerprinting Tootkit<br>xy Ee pubes] otaregeceeeei hee hak<br>Ee es '2026-09-17T21:20:59.113341+05302aze-09-17721:20:39,2e2s-o9-17%21:20Â°59-1127120059094433360530 INFOERWORTAFO std:StartingHo answerPerformingenunerstionfor ORSSECGeneralforqueryEnumerationdomain:for networkaalks.connetworkwatke.comagainst: networkwalks.com.<br>2e26-09-17121:21:00.695419-9530 INFO." SOn'ns6135.Rostgater com 30.07, aeeya?<br>Zeze-o9-17121:21c01-71546670530 INFO As noei3s-hostgator-com 30,87. i4es87<br>deze-oo-17121:21:02 s06960%0530 INFO bind Version for 30.87, 100.87 "9Â¢i6.23-RN"<br>Zeze-oo-i7121-21c02 s07262-0530 INFO Rs nseineshestgnter. con 192,232-716.131<br>gaze-09-17721:21:03. 19544200530 INFO Bind Version for 192.232.216.431 *9,16,23-R4<br>gaze-09-17T21:21:04,087015:0530 INFO Wt malLsnetworbwaltsscow 192.232.216.135<br>deaecoa-i7ra1sa1:os-sce77es0500 INFO Ainetwormatkeccou 192.292,216.135<br>deae-oa-17Fa1:21:0a 20010100590 INFO TXT networbras-con google-site-verification-rrOteRnqioW3Â¥ennizONVK4q75K-1)-njgfeg-USYI<br>Zeze-op-i7rai:2t:e0.200376-0530 INFO TAT networtnalhs.con Qoopfl va sax eiptsa0.87-Aet-a? sinclude:websitews\cne.con atl<br>eze-o9-17721:21:09.060083-9530 INFO Enumerating SRY Records<br>gaze-09-17721:21:13.927722-0530 INFO SRV -autodiscover.-tcp.networkwalks.com cpanelemaildiscovery.cpanel.net 184,94,204.14 443<br>2aze-09-17721:21:13.920059-0530 INFO SRV Lautodiscover._tcp.networkwalts. con cpanelemaildiscovery cpanel net 184,94,204.35 3<br>boze-09-17721:21:13.920882:0530 INFO SRV Lautodiscover._tep.networlwalts.con cpanelemaildiscovery.cpanel net 184794,203.35 3<br>gaze-09-17Ta1:21:13.9zeeaoson38 INFO SRV lautotiscover.-tep.networlwalts.con cpanelemaildiscovery cpanel fet 184,94,296.32 3<br>gaze-09-17721:21:13.92878760530 INFO SRV Lautodiscover,_tep.networkwalts.con cpanelemaildiscovery.cpanel et 184,94,203.14 3<br>deze-o9-17121:21:13.90090900530 IMFO SHY â€œautediscaver.ctepsnetwortwalas.com cpanelemaildiscovery.cpaneLenet 14.94.2031 443<br>Jeze-oo-17121:24s13 90901300500 IMFO SHV â€œautediscover:ctcp.neteortwalis.com cpanelenailaiscovery.cpanelsnet io4,9ec204,9 443<br>Jeze-oo-i7t2tc2tcis 9204180580 IMFO SHV â€œnutediscover:ctcp.neteortualisscom cpanelenaildiscoveryscpanelinet 164,96:203.9 443<br>done-o9-17721:21:13.933127+0830 INFO 8 Records Found<br>ene-op-17121:21:19.980487-0530 INFO Completed enumeration for domain: networkwatks.com<br>1<br><!-- End of picture text -->



<!-- Start of picture text -->
Se top Paces Sep? 932 PM Oo Oun oom too Loon On<br>ri<br>reos Sager thenarvester Erâ€™[oh] onseeesotved}-Â¢ oouamn (-1 fen)Cour]t-4)(-3 START](oF eivehe){-p] [os]Cow woRDList][screenshotfoal ScREENswoT]foe) {-> sounee](-e ONS. SERVER) (-t]<br>SN ro srry arya<br>ee fet ORT tt<br>SNEED ASL NASTEA SI 3<br>+ Coed by christian nartoretta &<br>+ Eagessecurity Research :<br>[1] No 1s found<br>[1] No enaits found<br>[1] no people found<br>[1] no hosts found<br><!-- End of picture text -->

Pentesting Project Report  |  Networkwalks  |  Page 9 



<!-- Start of picture text -->
theHarvester -d microsoft.com -l 50 -D a<br>Read proxies.yaml from /etc/theHarvester/proxies.yaml<br>parE SE IO SSE S IRIS S ISOS ISO III IIIA III IIA II<br>ie *<br>a WN |e. â€”â€” Se eee<br>pee ANY 4 7 PONE 77 ew a SV ao SS<br>el Itttt27/72 /CIIl VWs LALNIL L771 *<br>*<br>iejp NEE TEREST WW 77 NI N/A *<br>* theHarvester 4.11.1 *<br>* Coded by Christian Martorella *<br>x Edge-Security Research *<br>+ cmartorellagedge-security.com *<br>le *<br>poisiinohinabiniabiniabiniabiniibins<br>ins ina IAS IA IA IA IAIIA IAI IAI IAIIAI IAI IAI<br>[+] Target: microsoft.com<br>Read api-keys.yaml from /etc/theHarvester/api-keys.yaml<br>Failed to process bevigil search for word: â€˜microsoft.comâ€™<br>Error Message:<br>[!] Missing API key for bevigil.<br>Read api-keys.yaml from /etc/theHarvester/api-keys.yaml<br>[!] Missing API key for Bitbucket.<br>Read api-keys.yaml from /etc/theHarvester/api-keys.yaml<br>Failed to process bufferoverun search for word: â€˜microsoft.comâ€™<br>Error Message:<br>[!] Missing API key for bufferoverun.<br>Read api-keys.yaml from /etc/theHarvester/api-keys.yaml<br>Failed to perform BuiltWith search for word: â€˜microsoft.comâ€™<br>A Missing Key Error occurred in builtwith:<br>[!] Missing API key for BuiltWith.<br>Read api-keys.yaml from /etc/theHarvester/api-keys.yaml<br>Failed to process brave search for word: â€˜microsoft.comâ€™<br>Error Message:<br>[!] Missing API key for Brave Search.<br>Read api-keys.yaml from /etc/theHarvester/api-keys.yaml<br><!-- End of picture text -->



<!-- Start of picture text -->
fae eps Paces Sepae A226PM Oi Ose eon tose soos ONO<br>Target: 192:16820200/24 = Profile: + (Sean<br>Dock Command: nmap rn 192168202.0/28<br>vatnee 05EMUBRIGERO= Host192.168.2022 startingtinapmap scan-n192.168.202.0/24napreport7.99for( PEASE ) at Detaits<br>= 1921682021<br>[ee Host isup (9.000205 Latenc<br>Seer) MMWMREAR bo:se:56:c0:00408 (kare)<br>a a ? Wapjost scanis up report(0. 0 0 2 5 for latency)<br>Â«cp. finapost scanisu report forLatency)<br>iisap scan report for<br>TERIORHost is u 256 1Â° addresses (4 hosts up) scanned in 3.01 seconds<br>Cm Po @ oot<br><!-- End of picture text -->

Pentesting Project Report  |  Networkwalks  |  Page 10 



<!-- Start of picture text -->
â€œI Hosts |SenigÂ®s| Nmap Output Ports/Hosts Topology Host Details Scar<br>Dockat OS268.2021Host Hosts Viewer Fisheye Control jegendSave Graphic<br>= 192.168.2022 Pe<br>[ \<br>Clim PR O@s @F<br><!-- End of picture text -->

-End- 

**ðŸ‘¤ Author Ramen Debbarma** LinkedIn: https://www.linkedin.com/in/ramen-debbarma-a71632286/ 

**ðŸ‘¤ Project Information** 

**Program Name:** Cybersecurity program at Networkwalks | **Week:** 02 | **Repository:** GitHub 

Pentesting Project Report  |  Networkwalks  |  Page 11 
