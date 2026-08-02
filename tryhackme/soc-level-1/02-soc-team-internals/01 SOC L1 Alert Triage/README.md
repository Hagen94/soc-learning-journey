# SOC L1 Alert Reporting

## Overview

This room focuses on three essential SOC L1 skills: **alert reporting, escalation, and communication**.

During or after alert triage, an L1 analyst may need additional support to classify an alert, provide more context to L2, or respond to a real cyberattack that requires immediate attention and remediation.

The room explains how to properly document alert investigations, when and how to escalate alerts, and how to communicate effectively with senior analysts and other departments.

---

## Learning Objectives

After completing this room, I am able to:

* Understand the need for SOC alert reporting and escalation.
* Write clear and useful alert comments or case reports.
* Apply the Five Ws approach when documenting an alert.
* Identify situations where an alert should be escalated to L2.
* Understand the importance of communication during SOC operations.
* Request senior support when an alert is unclear or requires additional investigation.

---

## Key Concepts

### Alert Reporting

Alert reporting involves documenting the investigation and relevant evidence before closing or escalating an alert.

Detailed reporting is particularly important for **True Positive** alerts that require escalation.

A well-written report provides L2 analysts with the context needed to understand what happened and continue the investigation efficiently.

---

### Alert Escalation

When a True Positive requires additional actions or deeper investigation, the alert should be escalated to the appropriate L2 analyst following the organization's procedures.

L1 analysts may need to escalate when:

* The alert indicates a major cyberattack.
* Deeper investigation or DFIR is required.
* Remediation actions are needed.
* Communication with customers, partners, management, or law enforcement is required.
* The L1 analyst does not fully understand the alert and needs senior support.

---

### Communication

SOC analysts may need to communicate with other departments during or after an investigation.

For example, an analyst may need to contact the IT team to confirm administrative privileges or communicate with HR to obtain additional information about an employee.

Communication procedures may also be required during critical situations or when escalation is necessary.

---

## Alert Report Format — The Five Ws

The room recommends using the **Five Ws** to structure an alert report.

### Who

Which user performed the suspicious activity?

For example:

* Logged in
* Executed a command
* Downloaded a file

### What

What exact action or sequence of events occurred?

### When

When did the suspicious activity start and end?

### Where

Which device, IP address, or website was involved?

### Why

Why did the analyst reach the final verdict?

The reasoning behind the verdict is particularly important because it explains the analyst's conclusion.

---

## Why Alert Reports Matter

Alert reports serve several purposes:

### Provide Context for Escalation

A well-written report helps L2 analysts quickly understand what happened and reduces the need to restart the analysis from scratch.

### Preserve Findings

The report keeps important investigation context associated with the alert for future reference.

### Improve Investigation Skills

Writing a report requires the analyst to summarize and explain the investigation clearly, helping strengthen analytical skills.

---

## Escalation Process

A typical escalation process is:

```text
Alert
  ↓
Analysis
  ↓
Alert Report
  ↓
Verdict
  ↓
Escalation Required?
  ↓
Assign to L2
  ↓
L2 Continues Investigation
```

In the SOC dashboard scenario, the process is:

1. Move the alert to **In Progress** and perform the analysis.
2. Write the alert report and set the verdict.
3. If escalation is required, assign the alert to the L2 analyst on shift.
4. L2 receives the notification and starts from the alert report.

---

## Requesting L2 Support

L1 analysts should request senior support when something is unclear.

It is better to discuss an alert and clarify the appropriate SOC procedure than to close an alert that the analyst does not understand.

The exact procedure for requesting support may vary between SOC teams.

---

## Communication in Critical Situations

The room provides several scenarios where effective communication is important.

Examples include:

* An urgent critical alert requires escalation but L2 is unavailable.
* A compromised Slack or Teams account needs validation with the affected user.
* A large number of alerts arrive within a short period, including critical alerts.
* An analyst realizes that an alert was previously misclassified.
* SIEM logs cannot be properly parsed or searched.

In these situations, the analyst should follow the appropriate communication and escalation procedures rather than ignoring or skipping the alert.

---

## Analyst Workflow

The main concepts of this room can be summarized as:

```text
           ALERT
             ↓
          TRIAGE
             ↓
         ANALYSIS
             ↓
          VERDICT
             ↓
      ┌──────┴──────┐
      ↓             ↓
    CLOSE        REPORT
                    ↓
              ESCALATION?
                ↓       ↓
               NO      YES
                       ↓
                      L2
                       ↓
                 INVESTIGATION
```

---

## Skills Acquired

This room strengthened my understanding of:

* Alert reporting
* Alert escalation
* SOC communication
* Five Ws reporting
* L1 to L2 escalation
* Documentation of investigation findings
* Requesting senior support
* Handling critical communication scenarios

---

## Analyst Notes

### Key Takeaways

* Alert reporting provides important context for further investigation.
* True Positive alerts may require escalation to L2.
* A clear report helps L2 analysts continue an investigation efficiently.
* The Five Ws provide a structured way to document an alert.
* L1 analysts should request senior support when an alert is unclear.
* Communication is essential when dealing with critical or unexpected situations.
* SOC procedures may differ between teams, so analysts should follow their organization's established processes.

### New Terminology

* Alert Reporting
* Alert Escalation
* Communication
* True Positive
* L2 Analyst
* Five Ws
* DFIR
* Incident Response

---

## Personal Reflection

This room reinforced that a SOC L1 analyst's responsibility does not end after analyzing an alert.

Being able to clearly document findings, recognize when additional support is required, escalate appropriately, and communicate with other teams are essential parts of effective SOC operations.

A good alert report allows the next analyst to understand what happened without having to start the investigation from the beginning.

---

## References

* TryHackMe — SOC Level 1
* SOC L1 Alert Reporting room
