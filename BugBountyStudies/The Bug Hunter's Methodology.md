# Getting Started
### Books
1. The Web Application Hacker's Handbook : The bible of web hacking
2. Real-World Bug Hunting : Real world examples
3. OWASP testing guide
4. Bug bounty bootcamp
5. The Hacker Playbook 3
6. Breaking into information security
7. Hands on Hacking
8. Bug Bounty Playbook
9. Bug Bounty Playbook 2, Exploitation

### Resources and Hands on Training
1. [PentesterLab](https://pentesterlab.com/) : Paid solution for laboratories
2. [WebSecurityAcademy](https://portswigger.net/web-security)  Guides with real laboratories (free)
3. HackTheBox
4. VulnHub
5. OVWAD

# Mental Hurdles
1. The client is to big and too smart => the more complexity a project has, the more bugs it has.
2. Don't worry about other people that has alredy found some bugs, there is always more bugs.
3. size can be overwhelming. but size = complexity and complexity = bugs. Don't let size gets you down
4. Open Source. it is absolutely false that everyone looks at the code just for the fact that it is open. Don't overlook the source code of an open source project.
5. Don't just stay in the surface of the app, the most in depth you go, the most likely it is to find some bugs.

![[Drawing 2022-05-19 14.17.27.excalidraw.png]]

# Pre-Manual Testing and Automation
Usually this section can be done with tools for automation. It is good to view an application for its layers and these can be tested individually.

**Testing Layers:**
	 1. *Open Ports and Services*: Look for default creds on services, or service level exploit. (ssh,ftp,rdp) at this level it is rare to find service level exploit, most usually you will find default creds.
	 2. *Web Hosting Software*: Look for default creds, Web server misconfigurations, web exploits (apache, nginx, ...etc)
	 3. *Application Framework*: maybe has some admin pages with default creds.
	 4. *Application*: Here is where the custom code or COTS (custom of the shell software) lives. here is where the majority of bugs lives, like sql injections, xss, idor's, ...etc.
	 5. *Application Libraries (usually javascript)*: bake in libraries or dependencies can have their own vulnerabilites and allow you to use them against the app.
	 6. *Integrations*: your site can talk with others sites, and in those instances you can look for vulnerabilites

## Tech Profiling
When you fist approach a site/app you need to know what tech it is running. two browser extensions that can be used are [whatruns](https://www.whatruns.com/) and [wappalyzer](https://chrome.google.com/webstore/detail/wappalyzer-technology-pro/gppongmhjkpfnbhagpmjfkannfbllamg). There is also some command line tools to integrate into your automation like [webanalyze](https://github.com/rverton/webanalyze).

## Finding CVE's and Misconfigs
having completed recon on an assessment or bounty we want to analyze if targets have:
* known vulnerabilities
* Framework login pages
* Default creds
* and more

everything here it is related to *non-custom code*. These are usually platform, application server, framework, CMS, library, and misconfiguration related.

**Tools for automation of Finding CVE's and Misconfigs**:
1. [Nuclei](https://github.com/projectdiscovery/nuclei)
	* It is a community powered vulnerability Scanner highly extensible and allows you to make custom template for custom vulnerabilities or new CVE's that are not yet included.
	* it has checks for over 1000 CVE's.
	* it has checks for over 100 informational detections.
	* 500+ admin panel detectors
	* 1500+ other checks
		* creds/keys
		* 67 subdomain takeover
		* http form brute force
		* 3428 total templates
2. [Jaeles](https://github.com/jaeles-project/jaeles)
	* Another very popular for automatic web app testing.
3. Gofingerprint (by Tanner Barnes)
4. Sn1per (by @xer0dayz)
5. Intrigue Core (by jcran)
6. Vulners (Burp Extension)
7. Retire.js (Vulns related to javascript libs and frameworks)

Avoid hitting with automation large and very known targets because probably they have alredy done that thousands of times. It is best to use these tools on fresh targets or hidden domains.


## Port Scan
On top of finding CVE's at the layer of the web server, you also wanna do some port scanning. The most fast and extensible port scanner right now it is [Naabu](https://github.com/projectdiscovery/naabu), basically you give it a host, a domain it will resolve it and it will do port scanning for you, then you can pipe it to [nmap](https://nmap.org/) for service scanning or other automation tools of your like.
So for one shot port scann, Naabu is the way to go.

# Content Discovery
It is one of the most important parts of your web hacking journey. and they are seven main focus on content discovery discussed on their own section.
Some tools to automate content discovery:
1. [FEROXBUSTER](https://github.com/epi052/feroxbuster): A Rust Written tool for automating content discovery. It has the hability to pause content discovery scan and edit it while it is paused. An example of the usefulness it is that sometimes you hit a 200 response but it is actually a custom not found page, so the tool says it is here even when it is not, here with this tool you can pause it, add a filter really quick and then resume it. Actual Go To Tool.
2. Dirsearch (writteng in python, yuck)
3. WFuzz: The web fuzzer. preffered by people who really want to control the filters
4. Ffuf: really fast and was the go to content discovery tool for a long time.
5. GoBuster
6. TurboIntruder: Fastest of all of them because it incorporates http pipe lining allowing to send multiple requests per time. limited by being a part of burp paid suite

Content Discovery tools are nothing without the lists that drives them. basically we are sending request trying to find paths and files that exists on the web server, so we need some really good lists.
Some really amazing lists can be found on [wordlists.assetnote.io](https://wordlists.assetnote.io/).


## Based on tech
Recommendations on picking a List to do content discovery based on tech:
* **Tech**: 
	* *IIS/MSF (microsoft tech)*
		* from assetnote.io:
			* httparchive_aspx_asp_cfm_svc_ashx_asmx_...
		* IIS Shortname Scanner 
	* *PHP+CGI*
		* from assetnote.io:
			* httparchive_cgi_pl_...
			* httparchive_php...
	* *General API*
		* from assetnote.io:
			* httparchive_apiroutes_...
			* swagger-wordlist.txt
		* [api-endpoints.txt](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/api/api-endpoints.txt)
	* *JAVA*
		* from assetnote.io:
			* httparchive_jsp_jspa_do_action_...
	* *Generic*
		* from assetnote.io:
			* httparchive_directories_1m_...
		* [RAFT](https://github.com/danielmiessler/SecLists/tree/master/Discovery/Web-Content)
		* Robots Dissalowed
		* https://github.com/six2dez/OneListForAll
		* jhaddix/content_discovery_all.txt
	* *Others*
		* in assetnote.io search for anything in the "technology <=> host mappings" section. Like:
			* AEM
			* Apache
			* Cherrypy
			* Coldfusion
			* Django
			* Express
			* Flask
			* Laravel
			* Nginx
			* Rails
			* Spring
			* Symfony
			* Tomcat
			* Yii
			* Zend

>[!tip]
>pay special attention to configuration files for the technologies you are against
>specifically the web server or the application framework, for example you can find configuration that have a database connection with hard-coded credentials.
>It is also useful to take note of where the admin login and routes/endpoints are.

## COTS / PAID / OSS

**Open Source:**
if you go againts an application that is open source you can use the tool [Source2URL](https://github.com/danielmiessler/Source2URL) from Daniel Miessler that will index and retrieve the complete map of the app.

**PAID:**


## Custom
## Historical
## Recursive
## Mobile APIs
## Change Detection

# Application Analysis
