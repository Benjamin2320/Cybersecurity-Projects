# 🛡️ Lumma Stealer Phishing Investigation – EventID: 316

---
![Screenshot 2025-06-19 211835](https://github.com/user-attachments/assets/c30059ea-b685-454c-9600-c9d87e9729f7)
In the main alert feed we can see the top alert being a Critical Severity alert that came in on March 13, 2025 at 9:44AM. The rule that triggered the alert was "Lumma Stealer - DLL Side-Loading via Click Fix Phishing". We can also see that the type is classified as "data leakage". From this alert, my thinking process is that we are going to be looking for a phishing link that was clicked that caused some type of malware to be downloaded for data exfiltration.

---

![Screenshot 2025-06-19 211922](https://github.com/user-attachments/assets/88d84ab2-9c39-4f1a-9624-d5ce77c6d355)
Additional details for the alert show that teh SMTP (Simple Mail Transfer Protocol) address is 132.232.40.201, the source domain is update@windows-update.site, the destination email address (dylan@letsdefend,io), the subject line, that the action was performed and the reason that an alert was triggered. 

![Screenshot 2025-06-20 231333](https://github.com/user-attachments/assets/1aa90ec9-4cd6-4ea3-8245-ee4c53448b2c)
The next step would be the find the event through queries to find additonal details regarding the event. For this incident, we can use a query such as 

### "type = "Exchange" AND 
### source_address = "132.232.40.201" AND 
### destination_port = 25 AND 
### time >= "2025-03-13T00:00:00Z" AND 
### time < "2025-03-14T00:00:00Z"

to locate the event

### Screenshot 2025-06-20 231333.png  
![Screenshot 2025-06-20 231333.png](./Screenshot%202025-06-20%20231333.png)  
**Description:** The phishing attack begins with a seemingly legitimate email from `update@windows-update.site`, appearing to offer a free upgrade to Windows 11 Pro. The email subject is designed to entice users into clicking without suspicion, leveraging urgency and familiarity with Microsoft branding.

---

### Screenshot 2025-06-20 231439.png  
![Screenshot 2025-06-20 231439.png](./Screenshot%202025-06-20%20231439.png)  
**Description:** Upon investigating the suspicious domain, a VirusTotal scan shows that `windows-update.site` is flagged as malicious by 10 vendors. This confirms the domain is not only suspicious but actively identified in threat intelligence as part of phishing infrastructure.

---

### Screenshot 2025-06-20 231448.png  
![Screenshot 2025-06-20 231448.png](./Screenshot%202025-06-20%20231448.png)  
**Description:** Threat intelligence correlation tools link the domain to the Lumma Stealer malware family. This type of malware is an infostealer that exfiltrates credentials, browser data, crypto wallets, and more.

---

### Screenshot 2025-06-20 231513.png  
![Screenshot 2025-06-20 231513.png](./Screenshot%202025-06-20%20231513.png)  
**Description:** The organization's email security platform shows that the phishing email bypassed initial filtering and was delivered to the target's inbox. This highlights a gap in detection rules or threat feed updates.

---

### Screenshot 2025-06-20 231625.png  
![Screenshot 2025-06-20 231625.png](./Screenshot%202025-06-20%20231625.png)  
**Description:** This screenshot captures the phishing landing page, which mimics Microsoft's official upgrade portal. The attackers use deceptive UI elements such as timers and official logos to increase the chance of user interaction.

---

### Screenshot 2025-06-19 212223.png  
![Screenshot 2025-06-19 212223.png](./Screenshot%202025-06-19%20212223.png)  
**Description:** Log details reveal the originating SMTP server's IP: `132.232.40.201`. This helps identify the attack's infrastructure and aids in IP blocking or retroactive email trace across other users.

---

### Screenshot 2025-06-20 233616.png  
![Screenshot 2025-06-20 233616.png](./Screenshot%202025-06-20%20233616.png)  
**Description:** SOC analysts classify the incident (EventID: 316) as a true positive. The note specifies the threat was verified and containment measures were taken, closing the loop on this alert.

---

### Screenshot 2025-06-20 233627.png  
![Screenshot 2025-06-20 233627.png](./Screenshot%202025-06-20%20233627.png)  
**Description:** The infected machine, an internal Exchange Server with IP `172.16.20.3`, has been contained. This is a critical asset, and rapid containment minimized potential impact.

---

### Screenshot 2025-06-20 233722.png  
![Screenshot 2025-06-20 233722.png](./Screenshot%202025-06-20%20233722.png)  
**Description:** Host investigation details include last logged-in user, OS version, and browser. The attack vector was confirmed to be via Chrome browser on a Windows Server 2012 system.

---

### Screenshot 2025-06-20 233745.png  
![Screenshot 2025-06-20 233745.png](./Screenshot%202025-06-20%20233745.png)  
**Description:** Process logs show Chrome as the initial vector, confirming that the phishing link was clicked and opened via a web browser. This helps identify whether user action led to execution.

---

### Screenshot 2025-06-20 233950.png  
![Screenshot 2025-06-20 233950.png](./Screenshot%202025-06-20%20233950.png)  
**Description:** Command-line logs reveal mshta.exe being invoked, which is a known tactic for DLL side-loading. The malware attempts to communicate with `overcoatpassably.shop`, another known malicious domain.

---

### Screenshot 2025-06-20 234350.png  
![Screenshot 2025-06-20 234350.png](./Screenshot%202025-06-20%20234350.png)  
**Description:** SOC playbook instructs analysts to determine if the malicious file or link was interacted with. This is critical to assess user behavior and potential execution of the payload.

---

### Screenshot 2025-06-20 234406.png  
![Screenshot 2025-06-20 234406.png](./Screenshot%202025-06-20%20234406.png)  
**Description:** Delivery metadata reconfirms that the phishing email made it past the filtering layers and was presented to the user. The presence of a timestamp helps align events on a timeline.

---

### Screenshot 2025-06-20 234419.png  
![Screenshot 2025-06-20 234419.png](./Screenshot%202025-06-20%20234419.png)  
**Description:** Playbook validation confirms that the malicious message was successfully delivered. This step ensures the alert is not a false positive and that the investigation proceeds appropriately.

---

### Screenshot 2025-06-20 235005.png  
![Screenshot 2025-06-20 235005.png](./Screenshot%202025-06-20%20235005.png)  
**Description:** Final threat validation on VirusTotal shows persistent flags for phishing and malware, confirming the risk posed by this campaign. This validates earlier assessments and supports reporting.

---
