# SentinelTrace Investigation Report

## Endpoint Threat Hunting & Digital Forensics

**Platform:** macOS  
**Tool:** Velociraptor 0.77.2  
**Investigation Period:** September 2026  
**Assessment:** No Malware Indicators Identified

---

## 1. Executive Summary

SentinelTrace is an endpoint threat-hunting and digital-forensics investigation conducted using Velociraptor on a macOS endpoint.

The investigation examined process activity, network connections, persistence-related artifacts, system property lists, quarantine events, and software installation history.

The collected evidence did not identify obvious indicators of malicious processes, unexplained external network connections, unknown persistence identifiers, suspicious download activity, or obvious malicious software installation.

The assessment is limited to the artifacts collected and reviewed during the investigation period. It does not establish that the endpoint was permanently malware-free.

---

## 2. Investigation Scope

The following Velociraptor artifacts were examined:

1. `MacOS.Sys.Pslist`
2. `MacOS.Network.Netstat`
3. `MacOS.Detection.Autoruns`
4. `MacOS.System.Plists`
5. `MacOS.System.QuarantineEvents`
6. `MacOS.Detection.InstallHistory`
7. `MacOS.Detection.Yara.Process`
8. `MacOS.System.TCC`
9. `MacOS.System.Wifi`

---

## 3. Process Analysis

### Artifact

`MacOS.Sys.Pslist`

### Evidence

- 491 processes were examined.
- No deleted processes were identified.
- Three user-writable executable-path records were associated with the authorized Velociraptor lab environment.
- Targeted searches for suspicious command-line indicators returned no matches.
- Root-process review identified the authorized Velociraptor client.
- Process ancestry was consistent with the investigation environment.

### Assessment

No obvious malicious process was identified in the collected process snapshot.

---

## 4. Network Analysis

### Artifact

`MacOS.Network.Netstat`

### Evidence

- 27 network records were examined.
- External connections observed in the snapshot were attributable to Dropbox over TCP/443.
- Local Velociraptor, WebKit, Apple services, and Dropbox connections were observed.
- Listening services included Velociraptor and normal macOS/application services.
- No unexplained external destination was identified.

### Assessment

No obvious malicious network connection was identified in the collected evidence.

---

## 5. Persistence Analysis

### Artifact

`MacOS.Detection.Autoruns`

### Evidence

The artifact contained disabled login-item identifiers associated with recognizable Apple and third-party software.

Observed identifiers included components associated with:

- Apple
- Microsoft Teams
- Microsoft Update
- Spotify
- Surfshark
- Grammarly

### Assessment

No unknown or obviously suspicious persistence identifier was identified.

### Limitation

This artifact does not represent a complete inventory of every possible macOS persistence mechanism.

---

## 6. System Property List Analysis

### Artifact

`MacOS.System.Plists`

### Evidence

47 plist records were examined.

Targeted searches included:

- `RunAtLoad`
- `KeepAlive`
- `ProgramArguments`
- `Program`
- `ExecutablePath`
- `LaunchAgent`
- `LaunchDaemon`

The relevant matches were associated with Apple system configuration, including PowerManagement and NetworkExtension configuration.

The login-window configuration did not reveal an obvious persistence mechanism.

### Assessment

No obvious malicious persistence configuration was identified in the examined plist records.

---

## 7. Quarantine and Download Analysis

### Artifact

`MacOS.System.QuarantineEvents`

### Evidence

93 quarantine records were examined.

Observed agents included:

- Messages
- sharingd
- Safari
- Homebrew Cask

Targeted searches for suspicious executable/archive extensions and malware-related keywords returned no matches.

### Assessment

No obvious malicious download indicator was identified.

### Limitation

External URL reputation and threat-intelligence enrichment were not performed.

---

## 8. Software Installation Analysis

### Artifact

`MacOS.Detection.InstallHistory`

### Evidence

283 installation records were examined.

Installation activity included Apple software-update components, XProtect-related packages, and other normal installation processes.

Targeted security-related keyword matches were explainable and included:

- Apple XProtect payloads
- Apple audio content
- Wireshark `ChmodBPF`

No suspicious third-party package was identified.

### Assessment

No obvious malicious software installation was identified.

---

## 9. YARA Process Analysis

### Artifact

`MacOS.Detection.Yara.Process`

The artifact returned log output but no usable process-result rows.

### Assessment

No YARA detection was reported.

### Evidence Limitation

Complete process-scan coverage could not be independently verified from the returned artifact.

Therefore, this result should not be interpreted as proof that every process was successfully scanned.

---

## 10. TCC Analysis

### Artifact

`MacOS.System.TCC`

The artifact returned logs without usable result rows.

### Assessment

No conclusion was drawn because the available evidence was insufficient.

---

## 11. Wi-Fi Analysis

### Artifact

`MacOS.System.Wifi`

The artifact returned logs without usable result rows.

### Assessment

No conclusion was drawn because the available evidence was insufficient.

---

## 12. Evidence Quality

| Artifact | Quality |
|---|---|
| Process list | High |
| Network connections | High |
| Autoruns | Medium–High |
| System plists | High |
| Quarantine events | High |
| Install history | High |
| YARA process scan | Low / Incomplete |
| TCC | Insufficient |
| Wi-Fi | Insufficient |

Overall confidence is moderate-to-high for the specific indicators examined.

---

## 13. Final Assessment

# No Malware Indicators Identified

The collected evidence did not identify obvious indicators of:

- Malicious processes
- Unexplained external network connections
- Unknown persistence identifiers
- Obvious malicious plist persistence
- Suspicious download activity
- Obvious malicious software installation
- Reported YARA detections

This assessment applies only to the artifacts collected and reviewed during the September 2026 investigation.

---

## 14. Limitations

This investigation represents endpoint triage rather than a complete forensic examination.

Limitations include:

- Point-in-time collection
- No memory-forensics analysis
- No complete disk-image examination
- No enterprise-wide correlation
- No full threat-intelligence enrichment
- Incomplete YARA result coverage
- Insufficient TCC results
- Insufficient Wi-Fi results
- Limited persistence coverage

Absence of an indicator does not prove absence of compromise.

---

## 15. Skills Demonstrated

### DFIR

- Velociraptor
- Endpoint triage
- Process analysis
- Network analysis
- Persistence analysis
- macOS artifact analysis
- Quarantine-event analysis
- Software installation analysis
- YARA-based detection

### Investigation

- IOC-oriented filtering
- Suspicious command-line analysis
- Process ancestry review
- Network listener analysis
- Persistence artifact review
- Regex-based searches
- Evidence validation
- Evidence-quality assessment
- Investigation limitation analysis

### Documentation

- Evidence preservation
- CSV artifact analysis
- Reproducible investigation workflow
- Git/GitHub version control
- Privacy sanitization

---

## 16. Conclusion

SentinelTrace demonstrates a practical endpoint threat-hunting workflow using Velociraptor.

The investigation produced no identified malware indicators within the specific artifacts examined. The project also demonstrates an important DFIR principle: a defensible conclusion must distinguish between confirmed findings, negative findings, and areas where evidence is insufficient.

---

## Disclaimer

This project was performed in a controlled personal/lab environment for educational and portfolio purposes.

The findings represent analysis of collected artifacts at the time of investigation and should not be interpreted as a guarantee that the endpoint was never compromised.
