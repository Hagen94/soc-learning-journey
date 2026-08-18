# Introduction to SOAR

## Overview

This room introduces **Security Orchestration, Automation, and Response (SOAR)** and explains how it can help SOC teams overcome common operational challenges.

It explores how SOAR connects security tools, automates repetitive processes, organizes investigations through playbooks, and supports response actions.

The room also introduces practical SOAR playbooks and a Threat Intelligence workflow to demonstrate how manual and automated tasks can be combined during security operations.

---

## Learning Objectives

After completing this room, I am able to:

- Understand how a traditional SOC operates.
- Identify common challenges faced by SOC teams.
- Explain what SOAR is.
- Understand the three main capabilities of SOAR.
- Explain Security Orchestration.
- Explain Security Automation.
- Explain Security Response.
- Understand SOAR playbooks.
- Identify tasks that can be automated.
- Understand why SOC analysts are still required.
- Understand how SOAR can support phishing investigations.
- Understand how SOAR can support CVE patching workflows.
- Design workflows that combine manual and automated actions.

---

# Traditional SOC

A SOC is a centralized function responsible for monitoring and protecting an organization's digital assets.

Its main capabilities include:

- Monitoring and Detection
- Recovery and Remediation
- Threat Intelligence
- Communication

Monitoring and detection focuses on identifying suspicious activity, while recovery and remediation includes actions such as endpoint isolation, malware removal, and stopping malicious processes.

Threat intelligence provides information such as:

- IP addresses
- Hashes
- Domains
- Other indicators

The SOC also needs to communicate with IT teams and management during incidents.

---

# Challenges Faced by SOCs

Traditional SOC environments can face several operational challenges.

## Alert Fatigue

Security tools can generate large numbers of alerts.

Many alerts may be:

- False positives.
- Insufficient for investigation.
- Low priority.

This can overwhelm analysts and make it harder to focus on serious security events.

---

## Too Many Disconnected Tools

SOC analysts may need to work with multiple independent security tools.

For example:

```text
SIEM
 │
 ├── Firewall
 │
 ├── EDR
 │
 ├── Threat Intelligence
 │
 ├── IAM
 │
 └── Ticketing System
```


 Switching between these tools increases investigation time.
---
Manual Processes

Some SOC procedures depend heavily on manual actions and undocumented analyst knowledge.

This can:

- Slow investigations.
- Increase response times.
- Make processes less consistent.
---
Talent Shortage

The increasing complexity of security threats combined with large numbers of alerts can place additional pressure on SOC analysts.

This can contribute to:

- Analyst overload.
- Reduced efficiency.
- Longer incident response times.

---
What is SOAR?

Security Orchestration, Automation, and Response (SOAR) is a technology that unifies security tools used by a SOC.

Instead of switching between SIEM, EDR, Firewall, Threat Intelligence, IAM, and ticketing systems individually, analysts can coordinate these tools through a centralized SOAR interface.


SOAR also provides:

- Ticketing.
- Case management.
- Incident tracking.
- Structured investigation workflows.

---
The Three Core Capabilities of SOAR

SOAR is based on three main capabilities:
```text
             SOAR
               │
      ┌────────┼────────┐
      │        │        │
Orchestration Automation Response
```
---
1. Orchestration

Orchestration connects different security tools and coordinates their actions through a unified platform.

For example, during a VPN brute-force investigation, an analyst may need to use:

- SIEM
- Threat Intelligence
- IAM
- Ticketing system

SOAR connects these tools and defines the workflow through a playbook.

2. Automation

Automation means that predefined actions can be executed automatically instead of requiring manual interaction from the analyst.

For example:
```text
SIEM Alert
    │
    ▼
SOAR
    │
    ├── Query SIEM
    │
    ├── Check IP Reputation
    │
    ├── Disable User if Malicious
    │
    └── Create Ticket
```
Automation can significantly reduce the amount of repetitive work performed by SOC analysts.

3. Response

SOAR can also coordinate response actions across different security tools.

For example, following a VPN brute-force investigation, SOAR could:

Block an IP on the firewall.
Disable a user through IAM.
Open a ticket containing the investigation details.

This allows response actions to be coordinated through a single workflow.

SOAR Playbooks

A SOAR playbook is a predefined workflow that determines what actions should be taken for a specific type of alert or investigation.

Playbooks contain predefined steps and can include different paths depending on the result of each step.

Example:
```text
Alert Received
      │
      ▼
Check User Activity
      │
      ▼
Check IP Reputation
      │
      ▼
Check Successful Logins
      │
      ▼
Containment / Escalation
```
The workflow can change depending on the results.

For example, if the user normally uses the IP and the failed attempts are minimal, the playbook may stop early.

SOAR Does Not Replace SOC Analysts

SOAR can automate many repetitive tasks, but it does not replace SOC analysts.

Complex investigations still require human judgment.

SOC analysts are responsible for:

- Making critical decisions.
- Understanding the broader business context.
- Creating and maintaining playbooks.
- Performing complex investigations.
- Verifying important actions.

The role of SOAR is therefore to reduce repetitive workload and support analysts, rather than eliminate the analyst role.

# Phishing Playbook

The room introduces a phishing investigation as an example of a SOAR playbook.

A simplified workflow can look like:
```text
Suspicious Email
       │
       ▼
Create Ticket
       │
       ▼
Check URL / Attachment
       │
   ┌───┴───┐
   │       │
  URL   Attachment
   │       │
   └───┬───┘
       ▼
Threat Intelligence
       │
       ▼
Investigation
       │
       ▼
Remediation
```
The playbook contains conditional decisions based on whether the email contains a URL or attachment.

This allows repetitive investigation steps to be executed consistently.

# CVE Patching Playbook

SOAR can also support vulnerability management.

A newly disclosed CVE must be evaluated to determine whether the vulnerability exists within the organization's environment.

The room describes a playbook that can:

Analyze CVE details.
Assess the risk threshold.
Create a patching ticket.
Test the patch.
Prepare the patch for deployment.

This reduces the manual workload associated with handling frequent CVE disclosures.

# Manual vs Automated Tasks

An important concept from the room is that not every action should necessarily be automated.

A SOAR workflow can contain both:
```text
MANUAL
   │
   ├── Analyst decision
   │
   └── Human verification


AUTOMATED
   │
   ├── Query SIEM
   ├── Check Threat Intelligence
   └── Create Ticket
```
The appropriate balance depends on the workflow and the importance of human judgment.

This is particularly important for critical decisions where automation alone may not be sufficient.

Threat Intelligence Workflow

The practical task in the room focuses on creating a Threat Intelligence integration workflow.

The objective is to determine which parts of the workflow should be:

Manual.
Automated.

The workflow demonstrates how SOAR can combine different security processes into a single structured investigation.
---
# SOAR Investigation Workflow

The concepts from the room can be summarized as:
```text
              SECURITY ALERT
                    │
                    ▼
                   SOAR
                    │
          ┌─────────┼─────────┐
          │         │         │
     Orchestration Automation Response
          │         │         │
          └─────────┼─────────┘
                    │
                    ▼
                PLAYBOOK
                    │
          ┌─────────┴─────────┐
          │                   │
       Automated            Manual
        Actions             Actions
          │                   │
          └─────────┬─────────┘
                    ▼
              SOC ANALYST
                    │
                    ▼
            Decision / Escalation
```
This represents how SOAR integrates security tools and workflows while maintaining the analyst's role in critical decisions.
---
# SOAR and Core SOC Solutions

SOAR connects particularly well with the technologies studied in this section:
```text
                 SOAR
                  │
       ┌──────────┼──────────┐
       │          │          │
      SIEM       EDR       Firewall
       │          │          │
       └──────────┼──────────┘
                  │
          Threat Intelligence
                  │
                  ▼
              Playbooks
                  │
                  ▼
          Automated Response
```
The SIEM can provide alerts, EDR can provide endpoint information and response actions, threat intelligence can provide indicator information, and other tools can perform containment or remediation actions.

SOAR coordinates these capabilities through predefined workflows.

---

## Skills Acquired

This room strengthened my understanding of:

* SOAR
* Security Orchestration
* Security Automation
* Security Response
* SOC challenges
* Alert fatigue
* Tool integration
* Playbooks
* Case management
* Ticketing
* Automated workflows
* Manual vs automated actions
* Threat Intelligence workflows
* Phishing playbooks
* CVE patching playbooks
* Incident response automation
* SOC analyst decision-making
--- 
# Analyst Notes
## Key Takeaways
* Traditional SOCs can suffer from alert fatigue, disconnected tools, manual processes, and talent shortages.
* SOAR unifies security tools within a centralized interface.
* The three core SOAR capabilities are Orchestration, Automation, and Response.
* Orchestration connects different security tools and coordinates workflows.
* Automation executes predefined actions without requiring manual analyst interaction.
* Response allows SOAR to coordinate actions across security tools.
* Playbooks define predefined workflows for recurring alert types.
* Playbooks can contain different paths depending on investigation results.
* SOAR can automate repetitive investigation and response tasks.
* SOAR does not replace SOC analysts.
* Analysts remain responsible for complex investigations and critical decisions.
* Playbooks can support phishing investigations and CVE patching.
* Effective workflows can combine both manual and automated actions.

---
## New Terminology
* SOAR
* Security Orchestration
* Security Automation
* Security Response
* Playbook
* Alert Fatigue
* Case Management
* Workflow
* Automation
* Orchestration
* Threat Intelligence Workflow
* Phishing Playbook
* CVE Patching Playbook
---
## Personal Reflection

This room helped me understand how SOAR can improve the efficiency of a SOC by connecting security tools and automating repetitive tasks.

The most important concept for me was understanding the difference between orchestration, automation, and response. Orchestration connects the tools, automation executes predefined actions, and response allows those tools to be used to contain or remediate threats.

I also learned that automation does not eliminate the need for SOC analysts. Human judgment remains essential for complex investigations and critical decisions.

SOAR therefore acts as a force multiplier for the SOC, allowing analysts to spend less time on repetitive tasks and more time on investigations that require human expertise.

---
## References
* TryHackMe — SOC Level 1
* Introduction to SOAR room