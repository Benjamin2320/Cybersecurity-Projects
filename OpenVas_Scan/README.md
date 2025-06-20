# Vulnerability Assessment Lab with Greenbone Security Assistant (OpenVAS)

OpenVAS (Open Vulnerability Assessment System) is an open-source vulnerability scanner used for comprehensive network security assessments. It identifies a wide range of weaknesses, including outdated software, missing patches, known CVEs, default or weak credentials, exposed services, and system misconfigurations. OpenVAS supports both authenticated and unauthenticated scans, making it a powerful tool for enterprise-grade vulnerability management, compliance testing, and attack surface reduction.
This lab demonstrates a complete vulnerability assessment workflow using Greenbone Security Assistant (GSA), part of the OpenVAS vulnerability scanning suite. The scan targets a local subnet, and the task configuration includes customized scan tuning for deeper results.

---

## Lab Objectives
- Configure OpenVAS (Greenbone Security Assistant) on Kali Linux.
- Add authenticated credentials for deeper scanning.
- Create and tune scan configurations.
- Scan a local subnet and analyze high-severity findings.

---

## Environment Setup

### Starting the GVM Service

![Screenshot 2025-06-01 081406](https://github.com/user-attachments/assets/fdf6a805-81e6-471d-b1bc-9585279b98cd)
  
GVM services are started from the terminal on Kali Linux. The assistant listens on `127.0.0.1:9392`.

---

### Greenbone Dashboard Access

![Screenshot 2025-06-01 081438](https://github.com/user-attachments/assets/e6fadfab-6360-4f4e-9db6-6fb04237900e)

Accessing the web UI on localhost.

---

## Adding Credentialed Access

### Creating Default Credentials

![Screenshot 2025-06-01 081539](https://github.com/user-attachments/assets/8657b9ca-b82f-4d88-a9b0-5e2df2a4dff0)
  
A username/password credential is configured for deeper host enumeration and vulnerability detection.

---

## Creating a Scan Target

### Target Configuration

![Screenshot 2025-06-01 081905](https://github.com/user-attachments/assets/070c9e20-c459-4c56-bec1-fa0023519be0)

A target named `lan-subnet-86` is created using IPs from the file (`uphosts.txt`).

---

## Scan Configuration Tuning

### Selecting Scan Templates

![Screenshot 2025-06-01 161740](https://github.com/user-attachments/assets/4c1da34b-e1c3-4e33-8f20-02ec04f2e6be)
  
Multiple prebuilt scan templates are available; the Full and Fast template is cloned and customized to align with enterprise scanning needs and prioritize business-relevant vulnerabilities.

### Editing Scan Families

![Screenshot 2025-06-01 161820](https://github.com/user-attachments/assets/3b8c3f70-474d-4c60-8e29-b1b2a3a4383e)
 
Specific vulnerability families like buffer overflows, CentOS checks, and denial-of-service were selected to focus the scan on issues that could lead to system compromise or service outages. This helped narrow the results to threats more relevant to a typical business or enterprise environment.

![Screenshot 2025-06-01 161913](https://github.com/user-attachments/assets/3ad0d8ca-728f-4784-9574-4e23d6f538f8)

Fine-tuning continues by enabling additional vulnerability check categories.

---

## Launching the Scan Task

### Task Setup

![Screenshot 2025-06-01 162034](https://github.com/user-attachments/assets/f094fac7-bc8e-444d-bcb2-c990d614df20)

Task LAN_SCAN is configured to scan lan-subnet-86 using the customized scan configuration. The minimum QoD (Quality of Detection) was set to 70 to filter out low-confidence results and reduce false positives. Result overrides were applied to highlight or de-emphasize findings based on specific CVEs or detection rules, allowing for better prioritization of vulnerabilities. Alerts were also configured to trigger based on severity, supporting faster incident response.

### Scan Execution Parameters

![Screenshot 2025-06-01 162126](https://github.com/user-attachments/assets/36c9951d-e34c-4280-9830-02edfa724d2c)
  
Concurrency and performance settings are adjusted for efficient scanning.

---

## Scan Results

### Task Overview

![Screenshot 2025-06-01 165549](https://github.com/user-attachments/assets/72e1c88e-3635-42fd-a179-f5becbcc2ef2)
 
The completed scan shows 1 high-severity result.

### Results Breakdown

![Screenshot 2025-06-01 165616](https://github.com/user-attachments/assets/62191e2a-8f72-4d26-9eea-1c67c48f9835)

The scan identified several high-severity vulnerabilities, including outdated versions of OpenSSL, PHP, jQuery, and Apache HTTP Server. These end-of-life and misconfigured services pose significant security risks and require immediate attention.

### Nmap Validation

![Screenshot 2025-06-01 081711](https://github.com/user-attachments/assets/52692e17-9f8b-41aa-8fe3-5a30a62b23b9)

Nmap confirms open ports found on host `10.0.0.19`, verifying GSA findings.

---

## ✅ Summary

- Showcases custom scan configuration and tuning, including selective vulnerability families, QoD thresholds, and result overrides to align with enterprise risk priorities.

- Applies alerting and reporting features to simulate operational workflows in vulnerability management.

- Validates automated scan results through CLI-based recon with Nmap, ensuring accuracy and reinforcing best practices in layered security assessments.

