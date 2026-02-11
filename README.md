
🛡️ CyberTr0n SOC Infrastructure Build – Phase 2
# Detection Engineering & Identity Persistence Validation

Author: Orinea Mulaudzi
Status: Operational
Focus Area: Active Detection, Identity Persistence, MITRE ATT&CK
Primary Tooling: Wazuh SIEM/XDR, Windows Security Logs, Ubuntu Linux

# 📌 Project Overview

Phase 2 of the CyberTr0n SOC Infrastructure Build transitions the environment from passive log collection to active detection engineering.
The primary objective was to validate the SIEM’s ability to detect unauthorized administrative changes, a common persistence technique used by adversaries after initial access.

This phase focuses on identity-based persistence detection, mapped directly to the MITRE ATT&CK framework, using real Windows security telemetry and Wazuh’s detection engine.

# 🎯 Objectives

Validate end-to-end Windows security log ingestion

Confirm audit policy coverage for identity-related events

Detect unauthorized local account creation and enablement

Map detections to MITRE ATT&CK persistence techniques

Verify detection reliability independent of the web dashboard

# 🏗️ Architecture Context

Phase 2 builds on the Phase 1 SOC visibility architecture:

SIEM Manager: Ubuntu-based Wazuh Manager (Analysis Engine, API, Dashboard)

Monitored Endpoint: Windows 10/11 system with Wazuh Agent

Transport Security: Encrypted TLS communication over port 1514

# 🛠️ Implementation & Configuration

To establish a reliable identity-auditing baseline, the following steps were performed:

Log Ingestion Pipeline

Verified uninterrupted ingestion of Windows Security Logs

Confirmed secure telemetry flow to the Wazuh Analysis Engine over TLS

Audit Policy Validation

Ensured Windows audit policies were correctly logging:

Event ID 4720 – Local user account creation

Event ID 4722 – Local user account enabled

Service Stability & Troubleshooting

Resolved API synchronization issues caused by configuration errors

Optimized local_rules.xml to restore consistency between backend detection and dashboard visualization

Verified detection continuity via backend log analysis when GUI availability was degraded

# 🧪 Detection Validation & Evidence
Test Case: Identity Persistence

MITRE ATT&CK:

T1136.001 – Create Account: Local Account

T1098 – Account Manipulation

Attack Simulation

Action:

net user CyberTr0n_Hacker /add


Environment: Local Windows endpoint

Detection Outcome

Wazuh successfully triggered Rule 60109

Medium-severity alert generated

Alert contained:

Username created

Source process

Timestamp of activity

This confirms reliable detection of identity persistence behavior.

# 🔍 Security Metrics Observed
Metric	Result	Observation
Alert Accuracy	100%	No false positives during controlled testing
Detection Latency	Real-time	Alerts generated within seconds
Log Integrity	Verified	Correct correlation between Windows Event IDs and Wazuh rules
# 🧠 Key Learning Outcomes

Detection Engineering: Effective detections rely on correct telemetry, not just rule creation

Operational Resilience: Backend logs remain the source of truth when dashboards or APIs fail

MITRE Mapping: Persistence techniques can be validated using native OS events without custom exploit tooling

Pragmatic Security: Adjusting test methods preserves detection objectives when tooling issues arise

# 🚀 Next Phase: Phase 3 – Network Adversary Simulation

With internal identity persistence detection verified, Phase 3 will shift focus to external threat detection.

Phase 3 Goals

Deploy a Kali Linux attack platform

Simulate network reconnaissance and service probing

Validate detection of:

MITRE T1595 – Active Scanning

Verify attribution of external attacker IPs through SIEM telemetry
