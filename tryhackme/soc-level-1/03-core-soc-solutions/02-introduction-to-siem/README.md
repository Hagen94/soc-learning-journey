# Introduction to SIEM

## Overview

This room introduces **Security Information and Event Management (SIEM)** and explains how it provides centralized visibility into security events across an organization.

It covers the purpose of SIEM solutions, log collection and ingestion, log normalization, detection rules, alert generation, and alert investigation.

The room also introduces practical SIEM concepts through examples involving Windows Event Logs, authentication activity, process execution, and suspicious network behavior.

---

## Learning Objectives

After completing this room, I am able to:

* Understand what a SIEM solution is.
* Explain why centralized log collection is important.
* Identify common sources of security logs.
* Understand different methods of log ingestion.
* Explain log normalization and field-value pairs.
* Understand how SIEM detection rules work.
* Explain how alerts are generated from correlated events.
* Investigate alerts using SIEM dashboards and associated events.
* Distinguish between True Positive and False Positive alerts.
* Understand how SIEM supports SOC analysts during investigations.

---

# What is SIEM?

**Security Information and Event Management (SIEM)** is a security solution that collects and centralizes logs and security events from different sources.

Instead of investigating each system separately, SOC analysts can use a SIEM to obtain a centralized view of activity across the organization.

```text id="siem01"
             LOG SOURCES
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
   Endpoints   Servers    Network
       │          │          │
       └──────────┼──────────┘
                  ↓
              SIEM
                  ↓
        Detection & Correlation
                  ↓
                ALERT
                  ↓
             SOC ANALYST
```

This centralized visibility helps analysts detect, investigate, and respond to suspicious activity.

---

# Log Sources

A SIEM can collect logs from many different sources.

Common examples include:

* Endpoints
* Servers
* Network devices
* Firewalls
* Applications
* Authentication systems
* Databases
* Security solutions

Each source provides different information about activity occurring within the environment.

---

## Why Logs Are Important

Logs provide evidence about what happened within a system or network.

Examples of useful information include:

* User authentication.
* Process execution.
* Network connections.
* File activity.
* Security events.
* System changes.

By centralizing these logs, a SIEM allows analysts to correlate activity across multiple systems.

---

# Log Ingestion

Before a SIEM can analyze logs, the logs must be collected and ingested.

The room introduces several common methods of log ingestion.

---

## 1. Agent / Forwarder

A lightweight agent or forwarder can be installed on an endpoint.

Its purpose is to:

* Collect relevant logs.
* Forward logs to the SIEM.
* Provide continuous visibility into endpoint activity.

For example, Splunk uses a **forwarder** to send endpoint data to the SIEM.

---

## 2. Syslog

**Syslog** is a widely used protocol for collecting and forwarding log data.

It can be used by systems such as:

* Web servers
* Databases
* Network devices
* Security appliances

The logs are sent to a centralized destination for analysis.

---

## 3. Manual Upload

Some SIEM solutions allow analysts to upload previously collected or offline log data.

This can be useful when:

* Investigating historical data.
* Analyzing a specific log file.
* Performing offline analysis.

Solutions such as Splunk and ELK can support this type of ingestion.

---

## 4. Port Forwarding

A SIEM can listen on a specific network port while endpoints forward log data to that destination.

```text id="siem02"
Endpoint
    │
    │ Logs
    ▼
Listening Port
    │
    ▼
   SIEM
```

This provides another method for centralizing log data.

---

# Log Normalization

Different systems may generate logs using different formats.

For a SIEM to efficiently search and correlate these events, the information needs to be represented consistently.

This process is known as **log normalization**.

A normalized event can be represented using **field-value pairs**:

```text id="siem03"
Field              Value
--------------------------------
Username           john.smith
Source IP          192.168.1.50
Destination IP     10.0.0.15
Event ID           4688
Process            powershell.exe
```

Normalization makes it easier for detection rules to search for specific values across different log sources.

---

# Field-Value Pairs

Detection rules often monitor specific fields and their values.

For example:

```text id="siem04"
EventCode = 4688
NewProcessName contains "whoami"
```

The SIEM can use these conditions to identify activity of interest.

This is why properly normalized logs are important for reliable detection.

---

# SIEM Detection Rules

A SIEM uses **detection rules** to identify suspicious activity.

A detection rule is essentially a logical expression that defines conditions under which an alert should be generated.

### Example

```text id="siem05"
IF
    user has 5 failed login attempts
    within 10 seconds

THEN
    Trigger Alert:
    "Multiple Failed Login Attempts"
```

Other examples include:

* Successful login after multiple failed attempts.
* USB device connected to a restricted endpoint.
* Large amounts of outbound traffic.
* Event logs being cleared.
* Suspicious process execution.

---

# Detection Rule Example: Event Log Clearing

Threat actors may attempt to remove evidence by clearing Windows Event Logs.

The room provides an example using **Event ID 104**.

```text id="siem06"
IF
    Log Source = WinEventLog
    AND
    Event ID = 104

THEN
    Trigger Alert:
    "Event Log Cleared"
```

This demonstrates how a specific event and field value can be used to create a detection rule.

---

# Detection Rule Example: whoami

Attackers may execute commands such as `whoami` during post-exploitation or privilege escalation activity.

A detection rule can use process execution information:

```text id="siem07"
IF
    Log Source = WinEventLog
    AND
    EventCode = 4688
    AND
    NewProcessName contains "whoami"

THEN
    Trigger Alert:
    "WHOAMI Command Execution Detected"
```

This example demonstrates how multiple conditions can be combined to create a more specific detection.

---

# Alert Generation

The SIEM continuously analyzes ingested logs.

When events match the conditions defined in a detection rule, the SIEM generates an alert.

```text id="siem08"
LOGS
  │
  ▼
INGESTION
  │
  ▼
NORMALIZATION
  │
  ▼
CORRELATION
  │
  ▼
DETECTION RULE
  │
  ▼
MATCH
  │
  ▼
ALERT
```

The alert indicates that activity matching a known detection condition has occurred.

However, an alert does not automatically mean that an attack has occurred.

The analyst must investigate the associated events.

---

# Alert Investigation

SOC analysts spend significant time working with SIEM dashboards because dashboards provide a summarized view of important security information.

When an alert is triggered, the analyst should examine:

* The events associated with the alert.
* The detection rule that triggered.
* The conditions that were met.
* Relevant users.
* Source and destination systems.
* Related network activity.

The goal is to determine whether the alert represents a real threat.

---

# True Positive vs False Positive

After investigating the alert, the analyst determines its classification.

## False Positive

A **False Positive** occurs when an alert is triggered but the activity is legitimate.

Possible actions include:

* Close the alert.
* Document the reason.
* Tune the detection rule to reduce similar false positives.

---

## True Positive

A **True Positive** occurs when the investigation confirms that the activity is genuinely suspicious or malicious.

Possible actions include:

* Continue the investigation.
* Contact the asset owner.
* Isolate the infected host.
* Block a suspicious IP.
* Escalate the incident.

```text id="siem09"
                 ALERT
                   │
                   ▼
              INVESTIGATE
                   │
             ┌─────┴─────┐
             ▼           ▼
        FALSE POSITIVE  TRUE POSITIVE
             │           │
          TUNE /        FURTHER
           CLOSE      INVESTIGATION
                         │
                         ▼
                    RESPONSE /
                    ESCALATION
```

---

# SIEM Investigation Workflow

The concepts from this room can be combined into a SOC investigation workflow:

```text id="siem10"
             LOG SOURCES
                  │
                  ▼
             LOG INGESTION
                  │
                  ▼
           LOG NORMALIZATION
                  │
                  ▼
          DETECTION / CORRELATION
                  │
                  ▼
                ALERT
                  │
                  ▼
             L1 TRIAGE
                  │
                  ▼
             INVESTIGATION
                  │
             ┌────┴────┐
             ▼         ▼
          FALSE       TRUE
          POSITIVE    POSITIVE
             │         │
             ▼         ▼
            CLOSE   ESCALATE /
                    RESPOND
```

This workflow shows how SIEM technology supports the daily activities of a SOC analyst.

---

# SIEM and the SOC

SIEM is one of the core technologies used by SOC teams because it provides centralized visibility into security events.

A SOC L1 analyst can use SIEM to:

* Monitor security dashboards.
* Review alerts.
* Search logs.
* Investigate events.
* Correlate activity.
* Validate detection rules.
* Determine True or False Positives.
* Provide evidence for escalation.

SIEM therefore acts as an important source of evidence during security investigations.

---

# SIEM vs EDR

The previous room introduced EDR, while this room introduces SIEM.

Both provide visibility, but from different perspectives.

| EDR                            | SIEM                                  |
| ------------------------------ | ------------------------------------- |
| Focuses primarily on endpoints | Centralizes data from many sources    |
| Uses endpoint agents           | Uses multiple log ingestion methods   |
| Provides endpoint telemetry    | Provides centralized event visibility |
| Process and command monitoring | Cross-source log correlation          |
| Endpoint response capabilities | Detection and investigation platform  |
| Host isolation                 | Alert generation and analysis         |

In a real SOC, SIEM and EDR can complement each other.

```text id="siem11"
              ENDPOINT
                  │
                  ▼
                 EDR
                  │
            Endpoint Data
                  │
                  ▼
                 SIEM
                  ▲
                  │
       ┌──────────┼──────────┐
       │          │          │
    Firewall    Server    Network
      Logs       Logs       Logs
```

An analyst can use SIEM to identify suspicious activity and then use EDR telemetry to investigate what happened on the affected endpoint.

---

# Skills Acquired

This room strengthened my understanding of:

* SIEM
* Centralized log management
* Log sources
* Log ingestion
* Agents / Forwarders
* Syslog
* Manual log uploads
* Port forwarding
* Log normalization
* Field-value pairs
* Detection rules
* Event correlation
* Alert generation
* SIEM dashboards
* Alert investigation
* True Positives
* False Positives
* Detection rule tuning
* SIEM and EDR integration

---

# Analyst Notes

## Key Takeaways

* SIEM provides centralized visibility into security events.
* Logs can originate from endpoints, servers, network devices, applications, and security solutions.
* Logs must be ingested before they can be analyzed.
* Common ingestion methods include agents/forwarders, Syslog, manual uploads, and port forwarding.
* Log normalization makes data easier to search and correlate.
* Detection rules use logical conditions based on event fields and values.
* When events satisfy a detection rule, the SIEM generates an alert.
* An alert does not automatically mean that malicious activity occurred.
* Analysts must investigate the events associated with an alert.
* Alerts can be classified as True Positives or False Positives.
* False Positives may require detection rule tuning.
* True Positives require further investigation and potentially escalation or response.
* SIEM and EDR can complement each other during investigations.

---

## New Terminology

* SIEM
* Log Ingestion
* Log Normalization
* Syslog
* Forwarder
* Field-Value Pair
* Detection Rule
* Correlation
* Alert
* True Positive
* False Positive
* Detection Rule Tuning
* Event Log
* Event ID
* SIEM Dashboard

---

## Personal Reflection

This room helped me understand how SIEM fits into the daily workflow of a SOC analyst.

I learned that SIEM is not simply a place where logs are stored. It provides centralized visibility, allows events to be correlated, and uses detection rules to identify activity that requires investigation.

The most important concept for me is the relationship between **logs, detection rules, alerts, and investigation**. A detection rule generates an alert when specific conditions are met, but the analyst still needs to examine the associated evidence to determine whether the activity is legitimate or malicious.

Understanding this process is fundamental for an L1 analyst because SIEM alerts are one of the main sources of daily SOC investigations.

---

## References

* TryHackMe — SOC Level 1
* Introduction to SIEM room
