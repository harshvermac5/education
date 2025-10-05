# SECTION 1
## Cyber Defence Frameworks
Junior Security Analyst Intro
Pyramid Of Pain
Pyramid Of Pain
Cyber Kill Chain
Cyber Kill Chain
Unified Kill Chain
Diamond Model
MITRE
Summit
Eviction

# SECTION 2
## Cyber Threat Intelligence
Intro to Cyber Threat Intel
Threat Intelligence Tools
Yara
OpenCTI
MISP
Friday Overtime
Trooper

# SECTION 3
## Network Security and Traffic Analysis
Traffic Analysis Essentials
Snort
Snort Challenge - The Basics
Snort Challenge - Live Attacks
NetworkMiner
Zeek
Zeek Exercises
Brim
Wireshark: The Basics
Wireshark: Packet Operations
Wireshark: Traffic Analysis
TShark: The Basics
TShark: CLI Wireshark Features
TShark Challenge I: Teamwork
TShark Challenge II: Directory

# SECTION 4
## Endpoint Security Monitoring
Intro to Endpoint Security
Core Windows Processes
Sysinternals
Windows Event Logs
Sysmon
Osquery: The Basics
Wazuh
Monday Monitor
Retracted

# SECTION 5
## Security Information and Event Management
Introduction to SIEM
Investigating with ELK 101
ItsyBitsy
Splunk: Basics
Incident handling with Splunk
Investigating with Splunk
Benign
Introduction to Phishing

# SECTION 6
## Digital Forensics and Incident Response

DFIR: An Introduction

### Windows Forensics 1

#### Common windows hives:

- HKEY_CURRENT_USER: configuration of logged in user
- HKEY_USERS: active loaded user profiles
- HKEY_LOCAL_MACHINE: configuration of the machine
- HKEY_CLASSES_ROOT: merges information from `HKEY_LOCAL_MACHINE\Software\Classes` and `HKEY_CURRENT_USER\Software\Classes`. former one mentions default config while latter one provides the overrides.
- HKEY_CURRENT_CONFIG: hardware profile information, used at system startup
- NTUSER.DAT: mounted at `HKEY_CURRENT_USER` when a user logs in, can be found in `C:\Users\<username>` 
- USRCLASS.DAT: mounted at `HKEY_CURRENT_USER\Software\CLASSES`, can be found in `C:\Users\<username>\AppData\Local\Microsoft\Windows`
- Amcache Hive: contains info about programs that were recently run on system, can be found in `C:\Windows\AppCompat\Programs\Amcache.hve`

#### File Extensions Used in Hives
- .log – Transaction logs for changes
- .sav – Backup copies
- .alt – Alternate backups for critical hives
- No extension – Full hive data

#### Some important hives
- OS Version: `SOFTWARE\Microsoft\Windows NT\CurrentVersion`
- Current control set: configuration that controls system startup, there are two of them `ControlSet001` and `ControlSet002`. we can be assured that it stores the `last known good` configuration. all these info can be found at `SYSTEM\ControlSet001`, `SYSTEM\ControlSet002`, `SYSTEM\Select\LastKnownGood`
- Computer Name: `SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`
- Time Zone Information: `SYSTEM\CurrentControlSet\Control\TimeZoneInformation`
- Network Interfaces and Past Networks: `SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`, `SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Unmanaged` and `SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Managed`
- Autostart Programs: `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`, `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce`, `SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce`, `SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\Run`, `SOFTWARE\Microsoft\Windows\CurrentVersion\Run` and for services `SYSTEM\CurrentControlSet\Services`. Keep in mind that in services if `start`
 key is set to `0x02` means service will start at boot.
 - SAM hive and user information: `SAM\Domains\Account\Users`




Windows Forensics 2
Linux Forensics
Autopsy
Redline
KAPEKAPE
Volatility
Velociraptor
TheHive Project
Intro to Malware Analysis
Unattended
Disgruntled
Critical
Secret Recipe
SECTION 7
Phishing
Phishing Analysis Fundamentals
Phishing Emails in Action
Phishing Emails in Action
Phishing Analysis Tools
Phishing Prevention
The Greenholt Phish
Snapped Phish-ing Line
Phishing Unfolding
SECTION 8
SOC Level 1 Capstone Challenges
TempestTempest
Boogeyman 1
Boogeyman 2
Boogeyman 3
Upload and Conquer
Hidden HooksHidden Hooks
Scenario Hidden Hooks
BlackCat
