# SOC Workbooks and Lookups

## Overview

This room explains how SOC L1 analysts can use internal resources such as identity inventories, asset inventories, network diagrams, and SOC workbooks to improve the accuracy and efficiency of alert triage.

These resources provide additional context about users, hosts, IP addresses, and network activity, helping analysts understand suspicious events and make better-informed decisions.

---

## Learning Objectives

After completing this room, I am able to:

* Understand the purpose of identity and asset inventories.
* Use internal lookups to enrich alert investigations.
* Understand how network diagrams provide context during investigations.
* Understand what SOC workbooks are and why they are useful.
* Follow a structured workbook during alert triage.
* Divide an investigation into logical stages.
* Understand the relationship between enrichment, investigation, and escalation.
* Build simple workbooks around common investigation processes.

---

## Key Concepts

### Identity Inventory

An identity inventory provides information about users within an organization.

It can help an analyst understand:

* Who the user is.
* The user's role.
* The user's department.
* Whether the user's activity is expected.

Identity information can provide important context during alert investigations.

---

## Sources of Identity Information

Organizations can maintain identity information using different solutions.

Examples include:

| Source              | Example                      |
| ------------------- | ---------------------------- |
| Active Directory    | On-prem AD, Entra ID         |
| HR Systems          | Employee records             |
| Identity Management | Corporate identity platforms |
| Custom Solutions    | CSV or Excel files           |

Active Directory can be particularly useful because it provides identity information while also helping with asset inventory.

---

## Asset Inventory

An asset inventory provides information about devices belonging to an organization.

Typical information can include:

* Hostname
* Location
* IP address
* Operating system
* Owner
* Purpose

For example:

| Hostname | Location      | IP           | OS         | Owner        | Purpose       |
| -------- | ------------- | ------------ | ---------- | ------------ | ------------- |
| PC-891D  | London Office | 192.168.5.13 | Windows 11 | Tech Support | Stationary PC |
| L007694  | Remote        | N/A          | macOS 13   | A.Kelly      | DevOps laptop |
| L005325  | Remote        | N/A          | macOS 13   | J.Eldridge   | HR laptop     |

This information can help analysts determine whether activity involving a host is expected or suspicious.

---

## Sources of Asset Information

Common sources of asset information include:

* Active Directory
* SIEM
* EDR
* MDM solutions
* Custom asset inventories

Examples include:

| Solution         | Examples               |
| ---------------- | ---------------------- |
| Active Directory | On-prem AD, Entra ID   |
| SIEM / EDR       | Elastic, CrowdStrike   |
| MDM              | Microsoft Intune, Jamf |
| Custom Solutions | CSV or Excel           |

SIEM and EDR agents may collect information about monitored hosts, while MDM solutions are specifically designed to manage and inventory devices.

---

# Network Diagrams

## Purpose

Network diagrams provide a visual representation of an organization's network structure.

They can show:

* Locations
* Subnets
* Network connections
* Security boundaries
* Relationships between network segments

For SOC analysts, network diagrams provide valuable context when investigating suspicious network activity.

---

## Example Investigation

Consider the following sequence:

```text id="0i5o7c"
08:00
103.61.240.174
       │
       ▼
Corporate Firewall
TCP/10443
       │
       ▼
08:23
10.10.0.53
       │
       ▼
172.16.15.0/24
Network Scan
       │
       ▼
08:32
172.16.23.0/24
Network Scan
```

The analyst needs to determine:

* What service is running on TCP/10443.
* Why the external IP connected to that service.
* Which subnet contains `10.10.0.53`.
* Why the host attempted to access other subnets.
* Whether the activity represents an attack.

A network diagram can provide the missing context required to understand these relationships.

---

## Reconstructing an Attack Path

Using the available network information, the scenario can be reconstructed as:

```text id="g4r8d9"
Threat Actor
     │
     ▼
103.61.240.174
     │
     ▼
VPN
     │
     ▼
Successful Login
     │
     ▼
VPN Subnet
     │
     ▼
Database Subnet
     │
   BLOCKED
     │
     ▼
Office Subnet
     │
     ▼
Next Target
```

The investigation shows how an external threat actor could move from VPN access toward internal network segments.

---

# SOC Workbooks

## Definition

A **SOC workbook**, also known as a:

* Playbook
* Runbook
* Workflow

is a structured document that defines the steps required to investigate and remediate specific threats efficiently and consistently.

Workbooks are especially useful for L1 analysts because they provide structured guidance for investigation scenarios.

Senior analysts often prepare these resources to help less experienced analysts perform consistent and complete triage.

---

## Why Workbooks Are Important

Some investigations may require many steps.

Without a structured process, an analyst could:

* Miss important evidence.
* Perform steps in the wrong order.
* Reach a verdict without enough information.
* Produce inconsistent investigations.

Workbooks help reduce these risks by providing a defined investigation process.

---

# Workbook Investigation Structure

The room presents a workbook for investigating unusual login activity.

The workbook is divided into three logical stages:

```text id="9a9x9s"
┌─────────────────┐
│   ENRICHMENT    │
└────────┬────────┘
         ↓
┌─────────────────┐
│  INVESTIGATION  │
└────────┬────────┘
         ↓
┌─────────────────┐
│   ESCALATION    │
└─────────────────┘
```

---

## 1. Enrichment

The analyst gathers additional information about the affected user.

Possible resources include:

* Threat Intelligence
* Identity inventory
* Asset inventory

The goal is to obtain enough context before making a decision.

---

## 2. Investigation

The analyst uses the gathered information together with SIEM logs to determine whether the activity is expected.

The analyst evaluates the available evidence and reaches a verdict.

---

## 3. Escalation

If necessary, the analyst:

* Escalates the alert to L2.
* Communicates with the affected user.
* Follows the organization's established escalation procedures.

---

# Building Workbooks

Different SOC teams may use different approaches when creating workbooks.

Some organizations may have:

* Hundreds of detailed workbooks.
* Workbooks for specific detection rules.
* High-level workbooks for common attack vectors.
* More experienced L1 analysts who rely more heavily on their own judgement.

Regardless of the approach, L1 analysts should understand how to divide investigations into **modular blocks** and build simple workbooks around them.

---

## Workbook Design Concept

A simple investigation can be structured as:

```text id="5l2f6k"
ALERT
  │
  ▼
ENRICHMENT
  │
  ├── Identity Lookup
  ├── Asset Lookup
  └── Threat Intelligence
  │
  ▼
INVESTIGATION
  │
  └── SIEM / EDR Logs
  │
  ▼
VERDICT
  │
  ▼
ESCALATION / COMMUNICATION
```

This modular approach helps analysts perform investigations consistently.

---

# Lookups vs Workbooks

It is important to distinguish between the two concepts.

### Lookups

Provide **context and information**.

Examples:

* Identity inventory
* Asset inventory
* Network diagrams
* Threat intelligence

### Workbooks

Provide **instructions and structure**.

They tell the analyst:

> What should I investigate and in what order?

Therefore:

```text id="r2k6jz"
LOOKUPS
   ↓
CONTEXT
   ↓
WORKBOOK
   ↓
INVESTIGATION
   ↓
VERDICT
```

---

## SOC L1 Workflow

The concepts from this room can be combined into the following workflow:

```text id="q5k7mz"
              ALERT
                ↓
        INITIAL TRIAGE
                ↓
          LOOKUPS
        ┌───────┼────────┐
        ↓       ↓        ↓
     IDENTITY  ASSET   NETWORK
        │       │        │
        └───────┼────────┘
                ↓
           WORKBOOK
                ↓
          INVESTIGATION
                ↓
             VERDICT
                ↓
       ┌────────┴────────┐
       ↓                 ↓
    CLOSE            ESCALATE
```

---

## Skills Acquired

This room strengthened my understanding of:

* Identity inventory
* Asset inventory
* Network diagrams
* Security lookups
* Alert enrichment
* SOC workbooks
* Playbooks
* Runbooks
* Structured investigation
* Investigation modularity
* L1 alert triage
* Escalation workflows

---

## Analyst Notes

### Key Takeaways

* Internal lookups provide important context during alert investigations.
* Identity inventories help analysts understand users and their roles.
* Asset inventories provide information about hosts and devices.
* Network diagrams help analysts understand relationships between IPs, subnets, and network segments.
* Workbooks provide structured investigation procedures.
* Workbooks help L1 analysts avoid missing important investigation steps.
* A typical workbook can be divided into enrichment, investigation, and escalation.
* Lookups provide context, while workbooks provide investigation structure.
* Different SOC teams may use different levels of workbook complexity.
* Investigations can be divided into modular blocks to create simple and reusable workbooks.

### New Terminology

* Identity Inventory
* Asset Inventory
* Network Diagram
* Lookup
* Enrichment
* Workbook
* Playbook
* Runbook
* Workflow
* Threat Intelligence
* MDM
* Asset Management

---

## Personal Reflection

This room helped me understand that SOC analysts do not investigate alerts using only the information contained in the alert itself.

Additional context from identity inventories, asset inventories, network diagrams, and threat intelligence can significantly improve the investigation.

I also learned that workbooks provide a structured way to perform investigations consistently, which is particularly valuable for L1 analysts.

The combination of **lookups for context** and **workbooks for structured investigation** can make alert triage more efficient and reduce the risk of missing important evidence.

---

## References

* TryHackMe — SOC Level 1
* SOC Workbooks and Lookups room
