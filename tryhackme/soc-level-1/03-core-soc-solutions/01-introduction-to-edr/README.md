# Introduction to EDR

## Overview

This room introduces **Endpoint Detection and Response (EDR)**, one of the essential security solutions used by Security Operations Centers (SOCs).

It explains the basic architecture of EDR, how endpoint agents collect and send telemetry, how EDR solutions detect suspicious activity, and how analysts can respond to threats directly from the EDR platform.

The room also provides practical experience investigating detections through a simulated EDR dashboard.

---

## Learning Objectives

After completing this room, I am able to:

* Understand the purpose of EDR solutions.
* Explain the basic architecture of an EDR.
* Understand the role of EDR agents.
* Explain what endpoint telemetry is.
* Identify common types of telemetry collected by EDR.
* Understand behavioral and anomaly-based detection.
* Understand IOC matching and MITRE ATT&CK mapping.
* Understand the role of machine learning in EDR detection.
* Identify common EDR response capabilities.
* Understand how EDR telemetry supports security investigations.
* Investigate detections using an EDR dashboard.

---

# What is EDR?

**Endpoint Detection and Response (EDR)** is a security solution designed to continuously monitor endpoints and provide visibility into suspicious activity.

Unlike traditional antivirus solutions, EDR focuses not only on identifying known malicious files but also on collecting detailed endpoint activity and using that information to detect suspicious behavior.

EDR provides SOC analysts with visibility that can be used for:

* Detection
* Investigation
* Threat hunting
* Response
* Forensic analysis

---

# EDR Architecture

A basic EDR architecture consists of two main components:

```text id="9q3m1v"
        ENDPOINT
            │
            ▼
       EDR AGENT
            │
       Telemetry
            │
            ▼
       EDR CONSOLE
            │
            ▼
      SOC ANALYST
```

The **EDR agent** runs on the endpoint and collects information about activity occurring on the system.

The collected data is sent to the **EDR console**, where analysts and detection mechanisms can use it for investigation and response.

---

# EDR Agent

The EDR agent is installed on endpoints such as:

* Workstations
* Laptops
* Servers

Its main responsibilities include:

* Monitoring endpoint activity.
* Collecting telemetry.
* Sending telemetry to the EDR platform.
* Supporting detection and response capabilities.

The agent provides visibility into activity that may not be detected by traditional antivirus solutions.

---

# EDR Telemetry

## What is Telemetry?

Telemetry is the data collected by the EDR agent from an endpoint and sent to the EDR console.

It can be considered the **black box of an endpoint**, providing detailed information that helps analysts understand what happened on a system.

The more relevant data available to the EDR, the better the detection and investigation process can become.

---

## Process Executions and Terminations

EDR tracks running and terminated processes.

This can help analysts identify:

* Suspicious parent-child relationships.
* Suspicious executables.
* Malware payloads.
* Unusual process behavior.

For example:

```text id="4m2k7r"
winword.exe
     │
     ▼
powershell.exe
```

A Microsoft Word process spawning PowerShell may represent suspicious behavior and can be detected through behavioral analysis.

---

## Network Connections

EDR monitors endpoint network connections.

This can help identify:

* Command and Control connections.
* Unusual port usage.
* Data exfiltration.
* Lateral movement.

Network telemetry provides additional context about what an endpoint is communicating with.

---

## Command Line Activity

EDR can capture commands executed through:

* CMD
* PowerShell
* Other command-line environments

This can help identify:

* Malicious command execution.
* Obfuscated PowerShell.
* Suspicious scripts.

This visibility can reveal activity that traditional antivirus solutions may miss.

---

## File and Folder Modifications

Threat actors may modify files and folders during activities such as:

* Data staging.
* Ransomware execution.
* Malicious file dropping.

EDR monitors these modifications and can use them as part of its detection and investigation capabilities.

---

## Registry Modifications

The Windows Registry contains important information about system configuration.

Malicious activity may modify registry keys for purposes such as persistence or configuration changes.

EDR monitors registry modifications to provide additional visibility into endpoint activity.

---

# Why EDR Telemetry Matters

Advanced threats often attempt to remain hidden by using legitimate tools and processes.

Individually, each action may appear harmless.

However, when multiple events are correlated through detailed telemetry, the complete activity may reveal an attack.

```text id="k7v3p2"
Individual Events
       │
       ├── Process Execution
       ├── Network Connection
       ├── Command Execution
       ├── File Modification
       └── Registry Modification
                │
                ▼
        Correlated Telemetry
                │
                ▼
        Attack Investigation
```

Detailed telemetry can help analysts:

* Understand the full chain of events.
* Identify the root cause.
* Reconstruct the attack timeline.
* Determine whether activity is legitimate or malicious.

---

# EDR Detection Capabilities

EDR solutions use multiple techniques to identify suspicious activity.

---

## Behavioral Detection

Behavioral detection focuses on **what a process does**, rather than only matching known malware signatures.

This is useful because attackers may use legitimate applications and processes during an attack.

### Example

```text id="f2w8n6"
winword.exe
     │
     ▼
powershell.exe
```

A Word document spawning PowerShell represents an unusual parent-child process relationship and may be flagged by the EDR.

---

## Anomaly Detection

EDR can establish a baseline of normal endpoint behavior.

Activity that deviates significantly from this baseline can be flagged as suspicious.

### Example

A process modifying an auto-start registry key on a system where this behavior is uncommon may generate an alert.

Anomaly detection can sometimes produce false positives, so analysts must use the available context to determine whether the activity is legitimate.

---

## IOC Matching

EDR solutions can integrate with threat intelligence feeds.

Known Indicators of Compromise can be matched against endpoint activity.

Examples of IOCs include:

* File hashes
* Malicious files
* Known attack infrastructure

For example, if a downloaded executable has a hash associated with a known attack, the EDR can flag it.

---

## MITRE ATT&CK Mapping

EDR detections can be mapped to **MITRE ATT&CK tactics and techniques**.

This provides analysts with additional context about the stage of an attack.

### Example

If an EDR detects the creation of a scheduled task:

```text id="u8r5q1"
Tactic:
Persistence

Technique:
Scheduled Task/Job
```

This mapping can help analysts understand the likely purpose of the detected activity.

---

## Machine Learning

Modern EDR solutions may use machine learning models trained on large datasets of normal and malicious behavior.

Machine learning can identify complex patterns where individual actions may not appear malicious.

This can be useful for detecting:

* Fileless attacks.
* Multi-stage intrusions.
* Complex attack chains.

The ability to analyze the complete sequence of activity can reveal malicious behavior that may bypass simpler detection methods.

---

# EDR Response Capabilities

After detecting malicious activity, EDR solutions can provide automated and manual response capabilities.

---

## Host Isolation

An analyst can isolate a compromised endpoint from the network.

This can help prevent:

* Lateral movement.
* Further compromise.
* Communication with malicious infrastructure.

Host isolation can be particularly effective when an attack begins on a single endpoint and attempts to spread across the network.

---

## Process Termination

An analyst can terminate a malicious process directly from the EDR.

This can be useful when complete host isolation is unnecessary.

However, analysts must use this capability carefully because terminating a legitimate process can disrupt business operations.

---

## File Quarantine

Malicious files can be moved to an isolated location where they cannot be executed.

The analyst can then investigate the file and decide whether it should be:

* Restored.
* Permanently removed.

---

## Remote Access

EDR platforms may provide remote shell access to endpoints.

This allows analysts to:

* Execute commands.
* Run scripts.
* Collect additional information.
* Perform custom response actions.

This can be useful when the built-in response actions are insufficient.

The room provides an example using CrowdStrike Falcon's Real Time Response capability.

---

## Artefact Collection

EDR can allow analysts to collect artefacts from endpoints without physically accessing the device.

Common artefacts include:

* Memory dumps.
* Event logs.
* Specific folder contents.
* Registry hives.

These artefacts can support deeper forensic investigation and reporting.

---

# Detection and Response Workflow

The main EDR capabilities can be represented as:

```text id="a6j2m9"
             ENDPOINT
                 │
                 ▼
            EDR AGENT
                 │
                 ▼
             TELEMETRY
                 │
                 ▼
            DETECTION
        ┌────────┼────────┐
        │        │        │
   Behavioral  Anomaly   IOC
   Detection  Detection Matching
        │        │        │
        └────────┼────────┘
                 ▼
              ALERT
                 │
                 ▼
          SOC INVESTIGATION
                 │
                 ▼
             RESPONSE
        ┌────────┼─────────┐
        │        │         │
     Isolate  Terminate  Quarantine
      Host     Process      File
        │        │         │
        └────────┼─────────┘
                 ▼
          ARTEFACT COLLECTION
```

---

# Investigating EDR Alerts

The room includes a practical scenario in which a SOC analyst investigates medium- and high-severity detections through a simulated EDR dashboard.

The focus of the exercise is understanding the visibility provided by EDR detections and using the available information to perform triage.

The acknowledgement and response actions are outside the scope of the exercise.

---

# EDR vs Traditional Antivirus

One of the main concepts from this room is that EDR provides capabilities beyond traditional antivirus.

```text id="e5n7s4"
Traditional Antivirus
        │
        └── Primarily focused on detecting known malicious files
        

EDR
 │
 ├── Endpoint Telemetry
 ├── Behavioral Detection
 ├── Anomaly Detection
 ├── IOC Matching
 ├── MITRE ATT&CK Mapping
 ├── Machine Learning
 ├── Investigation
 └── Response
```

EDR provides much greater visibility into endpoint activity and gives SOC analysts additional capabilities for detection, investigation, and response.

---

# Skills Acquired

This room strengthened my understanding of:

* Endpoint Detection and Response
* EDR architecture
* EDR agents
* Endpoint telemetry
* Process monitoring
* Network connection monitoring
* Command-line monitoring
* File and folder monitoring
* Registry monitoring
* Behavioral detection
* Anomaly detection
* IOC matching
* MITRE ATT&CK mapping
* Machine learning detection
* Host isolation
* Process termination
* File quarantine
* Remote access
* Artefact collection
* EDR alert investigation

---

# Analyst Notes

## Key Takeaways

* EDR provides visibility into endpoint activity beyond traditional antivirus.
* EDR agents collect telemetry from endpoints and send it to the EDR console.
* Telemetry can include processes, network connections, commands, files, folders, and registry modifications.
* Correlating multiple events helps analysts understand the complete attack chain.
* Behavioral detection can identify suspicious activity even when known malware signatures are unavailable.
* Anomaly detection identifies activity that deviates from normal endpoint behavior.
* IOC matching allows EDR to identify known malicious indicators.
* MITRE ATT&CK mapping provides context about the attack stage.
* Machine learning can help detect complex and multi-stage attacks.
* EDR provides multiple response capabilities, including isolation, process termination, quarantine, and remote access.
* EDR telemetry can also support forensic investigation and attack timeline reconstruction.

---

## New Terminology

* EDR
* EDR Agent
* Endpoint Telemetry
* Behavioral Detection
* Anomaly Detection
* IOC
* MITRE ATT&CK
* Machine Learning
* Host Isolation
* Process Termination
* Quarantine
* Remote Access
* Real Time Response
* Artefact Collection
* Attack Timeline

---

## Personal Reflection

This room helped me understand why EDR is one of the essential technologies used by a SOC.

Before studying EDR, it could be easy to think of endpoint security mainly as antivirus protection. This room showed that modern EDR solutions provide much deeper visibility into what happens on an endpoint.

The ability to collect detailed telemetry, correlate events, detect suspicious behavior, and provide response capabilities gives SOC analysts the information and tools required to investigate endpoint-based threats.

Understanding EDR is particularly important for a SOC L1 analyst because many alerts investigated in a SOC can involve suspicious processes, commands, network connections, files, or other endpoint activity.

---

## References

* TryHackMe — SOC Level 1
* Introduction to EDR room
