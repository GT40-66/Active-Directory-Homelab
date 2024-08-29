
<h1>Active Directory and Splunk Home Lab</h1>

<h2>Description</h2>
In this lab, I created a domain controller with a user on a vulnerable client machine. Using Splunk on an Ubuntu server, I was able to see failed and successful logon attempts from a Kali Linux machine.
<br />

<h2>Tools and Systems Used</h2>
Windows 10 Pro, Windows Server 2022, Ubuntu Server, Kali Linux, Active Directory, Splunk Enterprise, Sysmon, Atomic Red Team, Splunk Universal Forwarder
<br />

<h2>Skills Learned</h2>
- Run Sysmon to log and aggregate data<br />
- Use Splunk Universal Forwarder to send data to Splunk Enterprise web GUI that is searchable through the index name<br />
- Create Active Directory Forest, Organizational Units within the domain, and domain user accounts<br />
- Utilize Crowbar on Kali Linux to brute force remote connection on a domain user account<br />
- Show failed and successful logon attempts in the Splunk GUI</b><br />
- Download and use Atomic Red Team on Windows 10 client to find vulnerabilities and events that Splunk was not configured to detect<br />



<h2>In this home lab, we created the following network</h2>
Domain Controller<br />
    Windows Server 2022<br />
    Active Directory / DNS<br />
    Splunk Universal Forwarder<br />
Client<br />
    Windows 10 Pro<br />
    Splunk Universal Forwarder<br />
    Atomic Red Team<br />
Attacker<br />
    Kali Linux<br />
    Crowbar<br />
    Rockyou.txt<br />
Splunk Server<br />
    Ubuntu Server CLI<br />
