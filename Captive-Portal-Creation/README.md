# pfSense Captive Portal Configuration

This lab walks through configuring a Captive Portal on pfSense for a corporate guest network. The portal is set to limit bandwidth, enforce connection/session timeouts, and allow bypass for specific administrative devices.

---

### Screenshot: ![Screenshot 2024-09-17 105240](https://github.com/user-attachments/assets/d1a942ed-9d69-47a0-9a7c-ac50c820e4c7)
**Initial Captive Portal Page**  
This screen shows the Captive Portal management interface before any zones are added. The next step is to click the green **Add** button to begin zone creation.

---

### Screenshot: ![Screenshot 2024-09-17 105407](https://github.com/user-attachments/assets/fe18b882-8170-44c3-a891-6080bf1688a4)
 ![Screenshot 2024-09-17 105319](https://github.com/user-attachments/assets/c4955535-72d6-4770-ba8b-3e6222b0d7ec)

**Add Zone - WiFi-Guest**  
We create a new zone named `WiFi-Guest` with the description:  
> _Guest Wireless access zone_  
This helps identify the portal's function and scope for guest access.

---

### Screenshot: ![Screenshot 2024-09-17 105611](https://github.com/user-attachments/assets/a9a5ff3d-b13b-4c9f-9b64-b09bb10c4fa0)
**Timeouts and Bandwidth**  
We set the following:
- **Hard timeout**: 45 minutes regardless of activity  
- **Bandwidth limits**:  
  - Upload: **2400 Kbit/s**  
  - Download: **7000 Kbit/s**  
- Enabled **logout popup** for user awareness before disconnection

---

### Screenshot: ![Screenshot 2024-09-17 105844](https://github.com/user-attachments/assets/cf520b32-ad8c-448b-89f1-4e146059733c)

`
**MAC Address Bypass**  
We allow the MAC address `00:00:1C:11:22:33` to bypass the portal. This is useful for trusted devices like admin laptops that need uninterrupted access.

---

### Screenshot: ![Screenshot 2024-09-17 105957](https://github.com/user-attachments/assets/59cd89cd-0dd0-4ef5-971a-6206aa297124)

`
**IP Address Bypass**  
Allowed IP: `198.28.1.100/16`  
This address is given the label:  
> _Security analyst's laptop_  
and is permitted through the portal in both directions without requiring authentication.

---

### Screenshot: ![Screenshot 2024-09-17 110646](https://github.com/user-attachments/assets/2fe09c46-99a5-4d8b-b0c6-649df9ee4c60)

**Authentication and Terms**  
We finalize the portal setup by:
- Adding a Terms and Conditions message: _“Don’t Break the Law!!!”_
- Selecting **None** for authentication to allow users to click through
- Enabling **HTTPS login** to secure credential transmission

---

## Summary

This lab demonstrates real-world guest network control using pfSense’s Captive Portal. It covers:
- Session and bandwidth management
- Bypass rules for trusted users
- Secure login configuration

The configuration ensures proper segmentation, accountability, and guest limitations on your corporate network.
