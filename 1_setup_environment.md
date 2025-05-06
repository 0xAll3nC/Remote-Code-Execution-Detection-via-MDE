# Step 1: Setup Environment – VM Provisioning & Onboarding to MDE

This step outlines how to set up a secure Windows Virtual Machine (VM), expose it for simulation, and onboard it to Microsoft Defender for Endpoint (MDE). This prepares the system for RCE detection and response testing.

---

## Objective

Provision a Windows VM, prepare it for remote code execution (RCE) simulation, and onboard it to Microsoft Defender for Endpoint for visibility and control.

---

## Prerequisites

- Access to the [Microsoft Defender Security Portal](https://security.microsoft.com)
- Azure, Hyper-V, or any virtualization environment to host a Windows 10/11 VM
- Administrator access to install and run onboarding scripts
- Strong internet connectivity

---

## VM Setup

1. **Provision a Windows VM**  
   Use Azure, Hyper-V, or VMware to launch a Windows 10/11 instance.

2. **Use a Strong Password**  
   Do **not** use weak default credentials like `labuser/Cyberlab123!`. Your VM could be compromised by opportunistic attackers if left exposed.

3. **Disable the Windows Firewall** *(for simulation purposes only)*  
   This helps make the VM discoverable:
   - Open Run → type `wf.msc`
   - Turn off Domain, Private, and Public profiles

---

## Onboarding to Microsoft Defender for Endpoint

1. **Log into the MDE Portal**  
   Navigate to [https://security.microsoft.com](https://security.microsoft.com)

2. **Go to the Onboarding Section**  
```
Settings → Endpoints → Device Management → Onboarding
````

3. **Download the Onboarding Package**  
- Choose the correct option (Windows 10/11 or Server)
- Download the onboarding script

4. **Install Onboarding Package on the VM**  
- Transfer the file to the VM
- Right-click → Run as Administrator

5. **Verify Successful Onboarding**  
- Go to:
  ```
  Assets → Devices
  ```
- Your VM should appear in the list with a green status

---

## Confirm Log Visibility in Advanced Hunting

1. Navigate to:
````
Hunting → Advanced Hunting
````

2. Run this query to check log visibility:

```kql
DeviceLogonEvents
| where DeviceName startswith "your-vm-name"
| order by Timestamp desc
````

Replace `"your-vm-name"` with the actual name of your virtual machine.

3. Ensure log entries are being received and displayed in real time.

---

## Outcome

At the end of this step:

* You have a properly configured Windows VM
* The VM is onboarded to MDE
* Logs are successfully visible in the Microsoft 365 Defender portal

---

> **Note: The firewall is only disabled here for lab simulation purposes. In production environments, this should never be done unless explicitly required and monitored.**
