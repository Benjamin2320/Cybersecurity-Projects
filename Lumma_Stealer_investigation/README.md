# 🛡️ Lumma Stealer Phishing Investigation – EventID: 316

---
![Screenshot 2025-06-19 211835](https://github.com/user-attachments/assets/c30059ea-b685-454c-9600-c9d87e9729f7)

In the main alert feed, we can see the top alert being a Critical Severity alert that came in on March 13, 2025 at 9:44AM. The rule that triggered the alert was "Lumma Stealer - DLL Side-Loading via Click Fix Phishing". We can also see that the type is classified as "data leakage". From this alert, my thinking process is that we are going to be looking for a phishing link that was clicked that caused some type of malware to be downloaded for data exfiltration.

---

![Screenshot 2025-06-19 211922](https://github.com/user-attachments/assets/88d84ab2-9c39-4f1a-9624-d5ce77c6d355)

Additional details for the alert show that teh SMTP (Simple Mail Transfer Protocol) address is 132.232.40.201, the source domain is update@windows-update.site, the destination email address (dylan@letsdefend,io), the subject line, that the action was performed and the reason that an alert was triggered. 

![Screenshot 2025-06-20 233950](https://github.com/user-attachments/assets/7940ab3b-1b7a-4be4-a726-b3b713765695)

The next step would be the find the event through queries to find additonal details regarding the event. For this incident, we can use a query such as 

### "type = "Exchange" AND 
### source_address = "132.232.40.201" AND 
### destination_port = 25 AND 
### time >= "2025-03-13T00:00:00Z" AND 
### time < "2025-03-14T00:00:00Z"

to locate the event

---
![Screenshot 2025-06-20 231513](https://github.com/user-attachments/assets/02c3b6c5-3136-4da0-a892-f11d102951b3)

(The email above the highlighted log)

![Screenshot 2025-06-20 231439](https://github.com/user-attachments/assets/c0bf555c-2f7d-4ec8-b714-ec32d1bfbe9d)
![Screenshot 2025-06-20 231448](https://github.com/user-attachments/assets/29e909c8-1be9-499c-bbbc-e205812fbe47)

As we can see, the phishing email resembles and authetic email that was sent by Microsoft. This ohishing email contains factors like a sense of urgency and brand recognition in order to trick the user into falling for the ploy. 

---

![Screenshot 2025-06-20 233616](https://github.com/user-attachments/assets/af14f3ef-0b93-4276-afb6-82528ed966ed)
![Screenshot 2025-06-20 233627](https://github.com/user-attachments/assets/79b21081-d4a0-4e5a-944f-80a40ea8deb3)

  
Upon investigating the suspicious domain, a VirusTotal scan shows that `windows-update.site` is flagged as malicious by 10 vendors. This confirms the domain is not only suspicious but actively identified in threat intelligence as part of phishing infrastructure.

---
  
![Screenshot 2025-06-20 231625](https://github.com/user-attachments/assets/788bf145-6732-4e62-9dcd-877ba14071f0)
  
Threat intelligence correlation tools link the domain to the Lumma Stealer malware family. This type of malware is an infostealer that exfiltrates credentials, browser data, crypto wallets, and more.

---

![Screenshot 2025-06-20 231333](https://github.com/user-attachments/assets/e9ac5bda-6b72-4a39-81e5-a393e95f6aeb)
![Screenshot 2025-06-20 234350](https://github.com/user-attachments/assets/6a75df9c-00ba-4d96-ac31-c6919ceac5f8)

Process logs show Chrome as the initial vector, confirming that the phishing link was clicked and opened via a web browser. This helps identify whether user action led to execution.

![Screenshot 2025-06-20 234406](https://github.com/user-attachments/assets/d4873524-b658-4f78-8e9c-a6b9466a71c3)
![Screenshot 2025-06-20 234419](https://github.com/user-attachments/assets/a4ca7e9f-3135-42c2-8493-2d59e6d1afec)

After review, we deem that the alert was a true positive. The next step in the incident response paln would be to contain the devices involved and quarantine them away from the network to minimilize impact. Segmentation provides protection from lateral movement and gives us the chance to  analyze the malware dynamically in a sandbox environment or review the static code. 

--- 
![Screenshot 2025-06-20 235005](https://github.com/user-attachments/assets/191d8e66-13b5-4fb1-bc93-c9b832fbb212)
 

I was able to classify the incident (EventID: 316) as a true positive. The note specifies the threat was verified and containment measures were taken. The alert will now be escalated or closed dependent on SOP. 

---
