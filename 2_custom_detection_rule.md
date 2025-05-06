# Step 2: Create a Custom Detection Rule in MDE

In this step, we’ll write a custom detection rule using KQL (Kusto Query Language) to detect potential Remote Code Execution (RCE) attempts via PowerShell. We’ll configure it to automatically isolate the VM and collect an investigation package.

---

## Objective

- Detect PowerShell-based RCE (e.g., `Invoke-WebRequest` + `Start-Process`)
- Create a custom detection rule scoped to your VM
- Automate isolation and investigation package collection on detection

---

## What We'll Detect

We simulate an RCE scenario where PowerShell is used to download and silently install 7-Zip using this command:

```powershell
cmd.exe /c powershell.exe -ExecutionPolicy Bypass -NoProfile -Command "Invoke-WebRequest -Uri 'https://sacyberrange00.blob.core.windows.net/vm-applications/7z2408-x64.exe' -OutFile C:\ProgramData\7z2408-x64.exe; Start-Process 'C:\ProgramData\7z2408-x64.exe' -ArgumentList '/S' -Wait"
````

---

## KQL Query to Detect the Behavior

Update `"my-vm-name"` to match your actual VM name.

```kql
let VMName = "my-vm-name";
DeviceProcessEvents
| where DeviceName == VMName
| where InitiatingProcessCommandLine contains "Invoke-WebRequest"
  and InitiatingProcessCommandLine contains "Start-Process"
```

> This query detects PowerShell scripts attempting to download and execute files.

---

## Create the Detection Rule in MDE

1. Log in to [https://security.microsoft.com](https://security.microsoft.com)
2. Go to:

   ```
   Hunting → Custom Detection Rules
   ```
3. Click on **+ Create** to begin creating a new rule
4. Paste the KQL query from above
5. Scope it specifically to your VM using the `DeviceName` filter
6. Configure the rule settings:

   * **Alert Title**: `Potential PowerShell RCE Detected on VM`
   * **Severity**: `High`
   * **Category**: `Execution`

---

## Automated Actions

Enable the following:

* Isolate Device
* Collect Investigation Package

These actions ensure that once the rule fires:

* The VM is immediately cut off from the network
* All forensic data is captured for analysis

---

## Why Scope It to Your VM?

Since this is a shared lab environment (or production environment with multiple assets), we **only want your detection rule to act on your own machine**. Avoid using a wildcard match or targeting all endpoints.

---

## Outcome

Once this step is complete:

* A detection rule is actively monitoring your VM
* If the defined behavior is triggered, MDE will:

  * Fire an alert
  * Automatically isolate your VM
  * Collect a complete investigation package

---

> Remember to delete this rule after testing so it doesn't interfere with other devices or experiments.
