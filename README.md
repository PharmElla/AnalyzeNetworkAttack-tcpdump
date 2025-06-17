# Apply OS hardening techniques

Yummyrecipesforme.com is a website that sells recipes and cookbooks. Consider a scenario where multiple customers emailed yummyrecipesforme’s helpdesk complaining that the company’s website had prompted them to download a file to access free recipes. The customers claimed that after running the file, the address of the website changed and their personal computers began running more slowly. 

In response to this incident, the website owner tries to log in to the admin panel but is unable to, so they reach out to the website hosting provider. As a cybersecurity analyst, I and my team are tasked with investigating this security event. The goal is to document the incident in detail, including identifying the network protocols used to establish the connection between the user and the website, and then recommend a security action to take to prevent attacks in the future.

## What was provided

- Tcpdump traffic log

## Activity

### Scenario

In this activity, I work as a Cybersecurity Analyst for yummyrecipesforme.com. A former employee has decided to lure users to a fake website with malware. The former employee/ hacker executed a brute force attack to gain access to the web host. They repeatedly entered several known default passwords for the administrative account until they correctly guessed the right one. After they obtained the login credentials, they were able to access the admin panel and change the website’s source code. They embedded a javascript function in the source code that prompted visitors to download and run a file upon visiting the website. After embedding the malware, the hacker changed the password to the administrative account. When customers download the file, they are redirected to a fake version of the website that contains the malware. Several hours after the attack, multiple customers emailed yummyrecipesforme’s helpdesk. They complained that the company’s website had prompted them to download a file to access free recipes. The customers claimed that, after running the file, the address of the website changed and their personal computers began running more slowly. 

### Incident Response

To address the incident, I create a sandbox environment to observe the suspicious website behavior. I run the network protocol analyzer tcpdump, then type in the URL for the website, yummyrecipesforme.com. As soon as the website loads, I am prompted to download an executable file to update my browser. I accept the download and allow the file to run. I then observe that my browser redirects me to a different URL, greatrecipesforme.com, which contains the malware.  

**The logs show the following process:**

1. The browser initiates a DNS request: It requests the IP address of the yummyrecipesforme.com URL from the DNS server.
2. The DNS replies with the correct IP address. 
3. The browser initiates an HTTP request: It requests the yummyrecipesforme.com webpage using the IP address sent by the DNS server.
4. The browser initiates the download of the malware.
5. The browser initiates a DNS request for greatrecipesforme.com.
6. The DNS server responds with the IP address for greatrecipesforme.com.
7. The browser initiates an HTTP request to the IP address for greatrecipesforme.com.

A senior analyst confirms that the website was compromised, checks the source code for the website and notices that javascript code had been added to prompt website visitors to download an executable file. Analysis of the downloaded file found a script that redirects the visitors’ browsers from yummyrecipesforme.com to greatrecipesforme.com. 

My team reports that the web server was impacted by a brute force attack. The disgruntled hacker was able to guess the password easily because the admin password was still set to the default password. Additionally, there were no controls in place to prevent a brute force attack. 
