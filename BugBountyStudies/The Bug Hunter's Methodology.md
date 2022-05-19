# Getting Started
### Books
1. [The Web Application Hacker's Handbook](obsidian://open?vault=obsidian&file=Books%2FThe%20Web%20Application%20Hacker%E2%80%99s%20Handbook.pdf) : The bible of web hacking
2. [Real-World Bug Hunting](obsidian://open?vault=obsidian&file=Books%2FReal-World-Bug-Hunting.pdf) : Real world examples
3. OWASP testing guide
4. Bug bounty bootcamp
5. The Hacker Playbook 3
6. Breaking into information security
7. Hands on Hacking
8. Bug Bounty Playbook
9. Bug Bounty Playbook 2, Exploitation

### Resources
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

![[Pasted image 20220518234505.png]]

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

## Port Scan

# Content Discovery
# Application Analysis
