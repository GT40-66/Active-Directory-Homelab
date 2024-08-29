
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
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Windows Server 2022<br />
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Active Directory / DNS<br />
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Splunk Universal Forwarder<br />
Client<br />
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Windows 10 Pro<br />
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Splunk Universal Forwarder<br />
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Atomic Red Team<br />
Attacker<br />
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Kali Linux<br />
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Crowbar<br />
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Rockyou.txt<br />
Splunk Server<br />
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Ubuntu Server CLI<br />
   <br/>
<p align="center">
Network Diagram <br/>
<img src="https://imgur.com/bye8XhD.png" /> <br/>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The goal of this lab was not to practice brute forcing a vulnerable domain user, but to learn how to configure and use Splunk to see the reports generated when an event like that happens. I used Oracle Virtualbox as my VM platform with the VMs configured on a NAT network. Although I use Active DIrectory daily as a system administrator, it is always good practice to create new domains from scratch. I can use this base domain further and continue to learn group policies and inheritance. 
<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I installed Splunk Enterprise and configured it to start on boot under the user ‘splunk’ on my Ubuntu Server. Once that was configured, I let it sit in the background for the duration of the lab. 
<p align="center">
Ubuntu Server <br/>
<img src="https://imgur.com/uyuPQIq.png" /> <br />

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I then moved onto installing Splunk Universal Forwarder and Sysmon on both the client and domain controller. Using a configuration from github, I created the inputs.conf file that needed to be placed in the Local folder in Universal Forwarder to pull the needed events from Sysmon and set the index to ‘endpoint’. With that in place, I logged into the Splunk web GUI on the client machine and configured the endpoint index and listening port for Universal Forwarder. From here, reports began to generate. 
<p align="center">
Splunk Web GUI <br />
<img src="https://imgur.com/7GHb1YG.png" /> <br />
<img src="https://imgur.com/x8fbKvD.png" /> <br />

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In Active Directory, I created an ‘IT’ and ‘HR’ organizational unit (OU). One user account was created for each OU. With the client machine joined to the domain, I logged in as John Doe, a network engineer in the IT OU. Because John Doe needed to work remotely, remote connection was enabled. 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;On the Kali machine, I installed Crowbar, a brute force tool. Since the focus of the lab was not on brute force technique, I created a smaller password list pulled from rockyou.txt and included the password for the domain user. The attacker, knowing the IP and user name for John Doe’s machine, used Crowbar along with the password list to brute force into the account. It was a success. 
<p align="center">
Password List Created from Rockyou.txt <br />
<img src="https://imgur.com/w9xwOs6.png" /> <br />
Crowbar Brute Force <br />
<img src="https://imgur.com/620MGrb.png" /> <br />
One note for the Splunk dashboard: <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;It took quite a few hours to see the failed and successful logon attempts generated. This may be due to not being able to allocate enough resources to the machine to perform the data collection, since I am running this lab on an old desktop with 16GB of RAM. I went ahead and installed Atomic Red Hat. This was by far the coolest tool I used during this lab. Essentially what it does is enabled the user to generate a variety of simulated attacks or events using the IDs from MITRE ATT&CK. It is a great way to test if you truly are collecting event data on specific instances. Using a single Powershell line, I was able to simulate a new local user creation event and notice that it did not populate on my Splunk. 
Overall, it was a very enjoyable lab that can be further expanded to practice security hardening measures. 
<p align="center">
Atomic Red Team Events using MITRE ID <br />
<img src="https://imgur.com/ARAoghI.png" />
Brute Force Attempts on Splunk <br />
<img src="https://imgur.com/elUAROY.png" />


