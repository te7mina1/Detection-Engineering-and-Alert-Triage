# Detection Engineering & Alert Triage

A hands-on Security Operations Center (SOC) project focused on designing custom detections, validating them through controlled attack simulations, and investigating generated alerts using a structured triage workflow.

The project demonstrates an end-to-end detection lifecycle:

**Log Collection → Detection Engineering → Attack Simulation → Alert Generation → Investigation → Triage → Analyst Disposition**

---

## Project Overview

This project was designed to simulate the responsibilities of a SOC Analyst and Detection Engineer.

The lab environment used Wazuh to collect telemetry from Windows and Ubuntu endpoints. Custom detection rules were developed based on selected MITRE ATT&CK techniques and tested using controlled adversary simulations.

Generated alerts were then investigated using a lightweight SOC triage playbook to determine the appropriate analyst disposition.

---

## Project Objectives

- Validate security telemetry from Windows and Ubuntu endpoints.
- Develop custom Wazuh detection rules.
- Map detections to MITRE ATT&CK techniques.
- Simulate adversary activity in a controlled environment.
- Validate and tune detection rules.
- Investigate generated alerts in Wazuh.
- Develop a SOC alert triage workflow.
- Document analyst findings and alert dispositions.

---

## Lab Environment

| Component | Purpose |
|---|---|
| Wazuh | SIEM platform used for log collection, detection, and alert investigation |
| Windows Endpoint | Generated Windows security and process telemetry |
| Ubuntu Endpoint | Generated Linux and SSH authentication telemetry |
| Sysmon | Provided enhanced Windows process and command-line visibility |
| Wazuh Agent | Forwarded endpoint telemetry to the Wazuh manager |
| Kali Linux | Used as part of the cybersecurity lab environment |
| VirtualBox | Hosted the virtual lab infrastructure |
| MITRE ATT&CK | Framework used to map detection techniques |
| Atomic Red Team | Used for controlled adversary simulation on Windows |
| Hydra | Used to simulate SSH password guessing against Ubuntu |

---

## Detection Engineering

Five custom detection scenarios were developed and mapped to MITRE ATT&CK techniques.

| Detection | Platform | MITRE ATT&CK | Tactic |
|---|---|---|---|
| Suspicious PowerShell | Windows | T1059.001 | Execution |
| Encoded PowerShell | Windows | T1059.001 | Execution |
| Windows Command Shell | Windows | T1059.003 | Execution |
| Scheduled Task | Windows | T1053.005 | Execution / Persistence |
| SSH Password Guessing | Ubuntu | T1110.001 | Credential Access |

The detection rules were written in Wazuh XML syntax and loaded into the SIEM for testing.

---

## Attack Simulation and Detection Testing

Controlled simulations were performed to generate realistic endpoint telemetry and validate the custom detection rules.

### Windows Simulation

**Invoke-AtomicTest / Atomic Red Team** was used to simulate ATT&CK-style techniques, including:

- PowerShell execution
- Encoded PowerShell activity
- Windows Command Shell execution
- Scheduled Task activity

The resulting telemetry was collected by Wazuh and reviewed to determine whether the custom rules triggered as expected.

### Linux Simulation

Hydra was used in the controlled lab environment to simulate repeated SSH authentication attempts against the Ubuntu endpoint.

```bash
sudo hydra -l ubuntu -P sshFile.txt ssh://192.168.100.142
