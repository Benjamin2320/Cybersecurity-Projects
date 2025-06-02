# pfSense Captive Portal Configuration

This lab walks through configuring a Captive Portal on pfSense for a corporate guest network. The portal is set to limit bandwidth, enforce connection/session timeouts, and allow bypass for specific administrative devices.

---
**Initial Captive Portal Page**  
This screen shows the Captive Portal management interface before any zones are added. The next step is to click the green **Add** button to begin zone creation.
 ![Screenshot 2024-09-17 105240](https://github.com/user-attachments/assets/d1a942ed-9d69-47a0-9a7c-ac50c820e4c7)


---
Next, we create a zone on the GuestWi-Fi interface. This helps identify the portal's function and scope for guest access. We will also add a zone description and set the limits for maximum connections and timeout time.
 ![Screenshot 2024-09-17 105407](https://github.com/user-attachments/assets/fe18b882-8170-44c3-a891-6080bf1688a4)
 ![Screenshot 2024-09-17 105319](https://github.com/user-attachments/assets/c4955535-72d6-4770-ba8b-3e6222b0d7ec)

---
**Timeouts and Bandwidth**  
We set the following:
- **Hard timeout**: 45 minutes regardless of activity  
- Enabled **logout popup** for user awareness before disconnection
- Set the **Traffic Quota** for the client

  We did not set a value for pass-through credits.
  
 ![Screenshot 2024-09-17 105611](https://github.com/user-attachments/assets/a9a5ff3d-b13b-4c9f-9b64-b09bb10c4fa0)


---


**MAC/IP Address Bypass**  

We allow the MAC address "00:00:1C:11:22:33" to bypass the portal. This is useful for trusted devices like admin laptops that need uninterrupted access.
 ![Screenshot 2024-09-17 105844](https://github.com/user-attachments/assets/cf520b32-ad8c-448b-89f1-4e146059733c)

---
Configuring the IP rule to allow the IP address of 'security analyst's laptop' to be a allowed to connect to the network freely in both directions. 
 ![Screenshot 2024-09-17 105957](https://github.com/user-attachments/assets/59cd89cd-0dd0-4ef5-971a-6206aa297124)



---
**Authentication and Terms**  
We finalize the portal setup by:
- Adding a Terms and Conditions message: _“Don’t Break the Law!!!”_

The authentication method is currently set to 'none' which will allow users to simply move on without authentication. The 'Authentication Backend' method will be selected to require valid login credentials for access. 
 
 ![Screenshot 2024-09-17 110646](https://github.com/user-attachments/assets/2fe09c46-99a5-4d8b-b0c6-649df9ee4c60)


---

## Conclusion

The configuration ensures proper segmentation, accountability, and guest limitations on your corporate network.
