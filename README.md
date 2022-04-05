# Honeypot Assignment

**Time spent:** **5** hours spent in total

**Objective:** Create a honeynet using MHN-Admin. Present your findings as if you were requested to give a brief report of the current state of Internet security. Assume that your audience is a current employer who is questioning why the company should allocate anymore resources to the IT security team.

### MHN-Admin Deployment (Required)

**Summary:** How did you deploy it? Did you use GCP, AWS, Azure, Vagrant, VirtualBox, etc.?

*I used GCP to deploy the MHN admin machiine and the honeypot machine. It was simple to do by setting up the appropriate firewall and then creating an Ubuntu machine on which I installed the MHN application from GitHub. All of this was done using the commands provided in the assignment walkthrough.*

<img src="https://github.com/zipesb/codepath_2022/blob/unit11_honeypot/unit11_mhnadmin.gif">

### Dionaea Honeypot Deployment (Required)

**Summary:** Briefly in your own words, what does dionaea do?

*Dionaea, as a honeypot, is used to provide a seemingly vulnerable attack surface that is accessible to anyone on the internet. In doing so it captures traffic from malicious actors that have machines working automatically to explore public IP addresses and attempt to exploit them. Dionaea analyzes suspected malicious traffic inside a LibEmu VM, which can detect shellcode with the goal of extracting an actual malware sample that the malicious traffic was attempting to compromise the honeypot with. From here, extracted malware samples can be analyzed.*

<img src="https://github.com/zipesb/codepath_2022/blob/unit11_honeypot/unit11_honeypot.gif">

### Database Backup (Required) 

**Summary:** What is the RDBMS that MHN-Admin uses? What information does the exported JSON file record?

*MHN uses SQLite as its relational database system, and MongoDB as its large scale data management system. The exported JSON file generally stores 9 pieces of data for each instance of connection to one of the honeypots ports. The first is an id which is an artifact of the database system itself. The next, a protocol value, identifies what communication protocol the traffic used, for example Server Message Block (SMB). Next is an hpfeed id which is just an identifier for the original hp feed message sent to MHN from the honeypot (MHN uses the hpfeeds protocol for communicating data from the honeypots to the MHN tool). There is a timestamp value which is of course the date and time the traffic was captured. Then there are values for the source IP and source port of the traffic, and the targeted port of the honeypot. The last two fields are an alphanumeric id and name for the honeypot that captured the traffic since MHN supports multiple honeypots running at once. Sometimes a specific communication protocol will feature additional values stored in the database, such as file attachments with hash values.*

<img src="https://github.com/zipesb/codepath_2022/blob/unit11_honeypot/unit11_dataexport.gif">

*Be sure to upload session.json directly to this GitHub repo/branch in order to get full credit.*

`============= stretch challenges not completed ================`

### Deploying Additional Honeypot(s) (Optional)

#### X Honeypot

**Summary:** What does this honeypot simulate and do for a security researcher?

<img src="x-honeypot.gif">

### Malware Capture and Identification (Optional)

#### X Malware

**Summary:** How did you find it? Which honeypot captured it? What does each malware do?

MD5 Hash: *Run `md5sum` on the file and record the hash here.*

SHA1 Hash: *Run `sha1sum` on the file and record the hash here.*

<img src="x-malware.gif">

## Notes

Describe any challenges encountered while doing the assignment.
