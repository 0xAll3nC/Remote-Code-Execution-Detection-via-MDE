# 🛡️ Remote Code Execution Detection via Microsoft Defender for Endpoint (Hard Mode)

This project simulates a real-world Remote Code Execution (RCE) attack using PowerShell and demonstrates how to detect, contain, and investigate it using Microsoft Defender for Endpoint (MDE). The setup includes custom KQL-based detection rules, automated VM isolation, and forensic investigation package analysis — showcasing a complete incident response workflow.

---

## 🎯 Project Objectives

- Detect simulated RCE attempts using PowerShell automation
- Create custom detection rules scoped to a specific VM
- Automatically isolate compromised endpoints
- Collect and analyze forensic investigation data

---

## 📁 Project Structure


mde-rce-detection-lab/
├── README.md
│   ├── 1\_setup\_environment.md
│   ├── 2\_custom\_detection\_rule.md
│   ├── 3\_trigger\_response.md
│   └── 4\_investigation\_analysis.md

---

## 🔍 What This Project Covers

- ✔️ Provisioning and securing a Windows VM
- ✔️ Disabling firewall for discoverability (simulated attack exposure)
- ✔️ Onboarding the VM to MDE and verifying visibility
- ✔️ Writing a KQL detection query for `Invoke-WebRequest` + `Start-Process`
- ✔️ Creating a custom detection rule with automated isolation & investigation
- ✔️ Triggering an RCE attempt via PowerShell
- ✔️ Confirming alert response and analyzing collected artifacts

---

## 📄 Documentation

| Step | Description |
|------|-------------|
| [1. Setup Environment](1_setup_environment.md) | Create a Windows VM and onboard it to MDE |
| [2. Create Detection Rule](2_custom_detection_rule.md) | Write KQL to catch PowerShell RCE behavior |
| [3. Trigger the Attack](3_trigger_response.md) | Execute simulated PowerShell RCE and trigger alert |
| [4. Investigate & Respond](4_investigation_analysis.md) | Review collected investigation package and resolve |

---

## 🛠️ Tools & Technologies

- Microsoft Defender for Endpoint (MDE)
- Microsoft 365 Security Portal
- Kusto Query Language (KQL)
- PowerShell (for simulating RCE)
- Azure VM / Hyper-V / VMware

---

## 📚 Learning Outcomes

- Understand how endpoint detection systems like MDE respond to RCE threats
- Learn to write custom KQL detection rules
- Gain experience in automatic isolation workflows
- Analyze investigation package data for real-world forensic insights

---

## 👨‍💻 About Me

Hi! I’m Allen Clement Justine Clement, a cybersecurity practitioner passionate about threat detection, SOC operations, and incident response.  
This project is part of my hands-on exploration into real-world attack detection and automated response using Microsoft tools.

Feel free to connect or explore my other security projects on GitHub!

---

