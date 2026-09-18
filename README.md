# SOC Incident Response Simulation

## Objective

The objective of this project was to simulate a SOC Analyst L1 alert triage workflow using a SIEM environment.

The project focused on investigating security alerts, analyzing available evidence, distinguishing between True Positives and False Positives, documenting findings, and taking the appropriate SOC response action.

---

## Methodology

The following 8-step SOC L1 triage framework was used:

1. **Receive the Alert**  
   Review the alert name, severity, timestamp, and detection rule.

2. **Assign the Alert**  
   Assign the alert to the SOC Analyst L1 and move it to an active investigation status.

3. **Review Alert Details**  
   Identify relevant information such as host, user, process, IP address, domain, file, and other indicators.

4. **Investigate the Evidence**  
   Analyze the available information and surrounding context to determine what occurred.

5. **Identify Suspicious or Legitimate Activity**  
   Look for indicators that support either malicious activity or a legitimate explanation.

6. **Determine the Verdict**  
   Classify the alert as either:
   - True Positive
   - False Positive

7. **Document Findings and Take Action**  
   Record the investigation reasoning and determine whether the alert should be closed or escalated.

8. **Close or Escalate**  
   Close legitimate/handled alerts or escalate confirmed suspicious activity for further investigation.

---

# Alert 001 — Double-Extension File Creation

**Severity:** High  
**Verdict:** True Positive  
**Action:** Escalate / Close after triage

### Findings

- **Host:** `LPT-HR-009`
- **User:** `S.Conway`
- **Process:** `chrome.exe`
- **File:** `cats2025.mp4.exe`
- **Download Source:** `freecatvideoshd.monster`
- **MD5:** `14d8486f3f6387e5ef93cd240c5dc10b`

The file used a suspicious double-extension pattern:

`cats2025.mp4.exe`

The `.mp4` portion makes the file appear to be a video, while `.exe` is the actual executable extension.

The file was also downloaded from an untrusted-looking external domain.

These indicators matched the detection rule for suspicious double-extension files commonly used to disguise executable files.

### Verdict

**True Positive**

### Action

**Escalate / Close after triage**

The alert was confirmed as suspicious activity involving an executable disguised as a video file.

---

# Alert 002 — Potential Data Exfiltration

**Severity:** Critical  
**Verdict:** False Positive  
**Action:** Close

### Findings

- **Source IP:** `192.168.45.66`
- **Source Network:** `UK04/MEETINGROOM`
- **Destination:** `*.zoom.us`
- **Data Sent:** `5.8 GB`
- **Data Received:** `5.2 GB`

The alert was triggered because of the large amount of outbound network traffic.

However, the destination was associated with Zoom and the source network was identified as a meeting-room network.

The high volume of traffic in both directions was consistent with legitimate video-conferencing activity.

No evidence of malicious data exfiltration was identified.

### Verdict

**False Positive**

### Action

**Close**

The alert was determined to represent legitimate Zoom-related network activity.

---

# Alert 003 — GitHub Download

**Severity:** Low  
**Verdict:** False Positive  
**Action:** Close

### Findings

- **User:** `G.Chandler`
- **Host:** `LPT-IT-063`
- **Source Network:** `VPN/DEVELOPERS`
- **Repository:** `github.com/facebook/react`

The alert was triggered by a download/access involving GitHub.

The accessed repository was the official `facebook/react` repository, and the activity originated from a network identified as `VPN/DEVELOPERS`.

This activity was consistent with legitimate developer activity.

No suspicious indicators were identified.

### Verdict

**False Positive**

### Action

**Close**

The alert was determined to be legitimate developer activity.

---

# Summary

| Alert | Severity | Verdict | Action |
|---|---|---|---|
| Double-Extension File Creation | High | True Positive | Escalate / Close after triage |
| Potential Data Exfiltration | Critical | False Positive | Close |
| GitHub Download | Low | False Positive | Close |

> **Important SOC concept:** Alert severity and alert verdict are different. A Critical alert can still be a False Positive if investigation shows that the activity is legitimate.

---

# Skills Demonstrated

- SIEM alert triage
- Security alert investigation
- Severity vs. verdict distinction
- True Positive / False Positive classification
- False Positive identification
- Evidence-based reasoning
- Indicator analysis
- File and network activity analysis
- Investigation documentation
- SOC L1 decision-making
- Alert closure and escalation
