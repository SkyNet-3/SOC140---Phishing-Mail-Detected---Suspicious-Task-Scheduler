<h1>SOC140 - Phishing Mail Detected - Suspicious Task Scheduler</h1>


<h2>Description</h2>
This lab reviews a phishing alert triggered by SOC rule SOC140 – Phishing Mail Detected – Suspicious Task Scheduler. The email used a “COVID-19 Vaccine” lure and was blocked before reaching the user. The activity suggests an attempt to create a malicious scheduled task, a common persistence technique attackers use to maintain access if malware is removed.
<br />


<h2> Utilities Used</h2>

- <b>LetsDefend SIEM</b> 
- <b>LetsDefend Email Security</b>
- <b>LetsDefend EDR</b>
- <b>AnyRun</b>
- <b>VirusTotal</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (22H2)

<h2>Alert walk-through:</h2>

<p align="center">
Go to investigation channel in Monitoring to get the context of the alert: <br/>
<img src="https://i.imgur.com/sOOHwJR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
After taking ownership of the case, parse the email for the needed information to perform analyses:  <br/>
<img src="https://i.imgur.com/X1aCxIX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
In order to see if the email had any URLs or attachments, check the Email Security: <br/>
<img src="https://i.imgur.com/vvan7G1.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Searching the email subject in Email Security allows us to locate the message and its attachment. Once confirmed, we proceed by answering “Yes” in the case management section:  <br/>
<img src="https://i.imgur.com/msdRZDr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next, determine whether the attachment is malicious by performing static and dynamic analysis using VirusTotal and ANY.RUN. Additionally, analyze the sender’s domain, SMTP IP, and any associated URLs:  <br/>
<img src="https://i.imgur.com/6nYUm9D.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
VirusTotal returned a 9/98 detection ratio, indicating multiple security vendors flagged the artifact as malicious or suspicious, consistent with phishing or malware activity:  <br/>
<img src="https://i.imgur.com/zeBXRyi.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
In the detail section it shows the detections point to phishing and spyware/malware, which are commonly used for credential theft and potential data exfiltration:  <br/>
<img src="https://i.imgur.com/dH3AO5X.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Although the SMTP IP is not currently flagged by antivirus vendors, negative community reputation, external reports of phishing activity, and geolocation inconsistencies indicate the infrastructure is likely being abused and should be treated as suspicious:  <br/>
<img src="https://i.imgur.com/aaN7zUs.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
The source address domain cmail.carleton.ca is a legitimate, long-established domain with no malicious reputation, the email did not originate from Carleton University’s authorized mail infrastructure. The trusted EDU domain was abused for credibility, and the SMTP source originating from Mexico—along with the urgent COVID-19 lure—confirms this as a phishing attempt via domain spoofing rather than a domain compromise:  <br/>
<img src="https://i.imgur.com/OeAUGFY.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
The attachment was a password-protected ZIP containing a PDF file. Upon extraction and opening, the document initiated multiple external HTTP and DNS requests, which is inconsistent with normal PDF activity and strongly indicates malicious or phishing-related functionality. Both MD5 and SHA-256 hashes resolved to the same ZIP in public submissions on ANY.RUN, which flagged the attachment as malicious, including indicators like phishing.img and suspicious PDF behavior. we proceed by answering “Malicious” in the case management section:  <br/>
<img src="https://i.imgur.com/NIsMwh3.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
In the investigation Channel is shows "Device Action: Blocked" so the malware was not delivered. Proceed with answering "Not Delivered":  <br/>
<img src="https://i.imgur.com/iTkAWMn.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Add the artifacts collected from your investgation in the case:  <br/>
<img src="https://i.imgur.com/aKkt6et.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
write your analyst notes from the case. click confirm and youre finished! Next closing the case..:  <br/>
<img src="https://i.imgur.com/6A6GFLn.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Lastly, close out your case by identifying this alert as a True  Positive because the security system correctly identified the malicious activities and IOCs. Write your notes, close it out, and youre done! :  <br/>
<img src="https://i.imgur.com/rNJ1O68.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
