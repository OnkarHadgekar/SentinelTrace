# SentinelTrace — Endpoint Threat Hunting & Digital Forensics

SentinelTrace is a hands-on endpoint threat hunting and digital forensics project built with **Velociraptor** on macOS.

The project demonstrates a structured investigation of endpoint processes, network activity, persistence mechanisms, downloaded files, software installation history, and selected system artifacts.

> **Assessment:** No Malware Indicators Identified in the collected evidence examined during the September 2026 investigation window. This is a point-in-time assessment and does not establish that the endpoint was permanently malware-free.

---

## 1. Project Objectives

The investigation was designed to:

- Identify suspicious or anomalous processes
- Examine active network connections and listeners
- Investigate persistence-related artifacts
- Review macOS property-list configuration
- Examine download/quarantine history
- Review software installation activity
- Evaluate available YARA process-scan results
- Document evidence quality and investigation limitations
- Preserve investigation artifacts for reproducibility

---

## 2. Environment

| Component | Details |
|---|---|
| Operating System | macOS |
| Architecture | ARM64 |
| Endpoint | MacBook Air |
| DFIR Platform | Velociraptor 0.77.2 |
| Investigation Type | Endpoint Threat Hunting / Digital Forensics |
| Investigation Period | September 2026 |

---

## 3. Investigation Methodology

The investigation followed a layered endpoint-triage approach:

```text
Endpoint Collection
       │
       ├── Process Enumeration
       │
       ├── Network Connections
       │
       ├── Persistence / Autoruns
       │
       ├── System Plists
       │
       ├── Quarantine / Download History
       │
       ├── Software Installation History
       │
       ├── YARA Process Scan
       │
       └── Additional System Artifacts
              │
              ▼
       Evidence Review
              │
              ▼
       Indicator Assessment
              │
              ▼
       Evidence Quality + Limitations
              │
              ▼
       Final Assessment

