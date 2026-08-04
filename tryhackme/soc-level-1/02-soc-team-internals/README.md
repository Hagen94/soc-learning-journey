# SOC Team Internals

## Overview

This module explores the internal processes and practices used by a Security Operations Center (SOC) to manage, investigate, and respond to security alerts.

It focuses on the responsibilities and workflows of a SOC L1 analyst, from the initial triage of an alert through investigation, reporting, escalation, and the use of internal resources to support the investigation.

The module also introduces SOC metrics and objectives used to evaluate the efficiency and effectiveness of security operations.

---

## Learning Objectives

After completing this module, I am able to:

* Understand the SOC L1 alert triage process.
* Prioritise and investigate security alerts systematically.
* Classify alerts as True Positive or False Positive.
* Document investigation findings clearly.
* Understand when and how alerts should be escalated.
* Communicate effectively during security investigations.
* Use identity and asset inventories to enrich investigations.
* Understand the role of network diagrams during investigations.
* Use SOC workbooks and lookups to structure alert investigations.
* Understand common SOC performance metrics and objectives.
* Recognize how metrics can identify operational problems within a SOC.

---

## Module Structure

### 01 — SOC L1 Alert Triage

This section focuses on the alert lifecycle and the systematic process used by SOC L1 analysts to review, prioritise, investigate, classify, and close security alerts.

**Main concepts:**

* Alert lifecycle
* Alert properties
* Alert prioritisation
* Alert investigation
* True Positive / False Positive
* SIEM and EDR
* Alert triage

---

### 02 — SOC L1 Alert Reporting

This section focuses on documenting investigations, escalating alerts when necessary, and communicating relevant information to L2 analysts and other teams.

**Main concepts:**

* Alert reporting
* The Five Ws
* Alert escalation
* L1 to L2 communication
* Investigation documentation
* Critical situations

---

### 03 — SOC Workbooks and Lookups

This section introduces internal resources that provide additional context and structure during alert investigations.

**Main concepts:**

* Identity inventories
* Asset inventories
* Network diagrams
* Lookups
* SOC workbooks
* Playbooks
* Runbooks
* Investigation enrichment

---

### 04 — SOC Metrics and Objectives

This section introduces metrics used to evaluate SOC workload, detection capabilities, alert handling, and response performance.

**Main concepts:**

* Alerts Count
* False Positive Rate
* Alert Escalation Rate
* Threat Detection Rate
* SLA
* MTTD
* MTTA
* MTTR

---

## SOC L1 Workflow

The four sections can be connected through the overall SOC L1 workflow:

```text
                  SECURITY ALERT
                        │
                        ▼
                ALERT PRIORITISATION
                        │
                        ▼
                   ALERT TRIAGE
                        │
                        ▼
                   INVESTIGATION
                        │
              ┌─────────┴─────────┐
              │                   │
           LOOKUPS             WORKBOOK
              │                   │
              └─────────┬─────────┘
                        │
                        ▼
                     VERDICT
                        │
               ┌────────┴────────┐
               │                 │
           FALSE POSITIVE    TRUE POSITIVE
               │                 │
               │                 ▼
               │             REPORTING
               │                 │
               │                 ▼
               │             ESCALATION
               │                 │
               │                 ▼
               │                 L2
               │
               └────────┬────────┘
                        │
                        ▼
                   METRICS & SLAs
```

This workflow connects the technical investigation of alerts with the operational processes required to document, escalate, and measure SOC activities.

---

## Skills Developed

This module strengthened my understanding of:

* SOC L1 alert triage
* Alert prioritisation
* Security alert investigation
* Alert classification
* Alert reporting
* Alert escalation
* SOC communication
* Investigation documentation
* Identity and asset lookups
* Network investigation context
* SOC workbooks and runbooks
* SOC performance metrics
* SLA, MTTD, MTTA, and MTTR

---

## Module Takeaways

* Alert triage is a fundamental responsibility of SOC L1 analysts.
* Alerts must be prioritised and investigated systematically.
* Investigation findings should be properly documented.
* True Positive alerts may require escalation to L2.
* Internal lookups provide valuable context during investigations.
* Workbooks provide structured guidance for recurring investigation scenarios.
* SOC metrics help measure the effectiveness and efficiency of security operations.
* L1 analysts contribute directly to the quality and speed of SOC operations.

---

## Personal Reflection

This module helped me understand that the work of a SOC L1 analyst involves much more than simply reviewing security alerts.

An analyst needs to know how to prioritise alerts, investigate them using available evidence and internal resources, determine the appropriate verdict, document the findings, and escalate when necessary.

I also learned that SOC operations are continuously measured through metrics such as alert volume, false positive rate, detection rate, MTTD, MTTA, and MTTR.

Understanding these processes provides a more complete picture of how a SOC operates and how the work of an L1 analyst fits into the wider security operation.

---

## Repository Structure

```text
SOC Team Internals/
│
├── README.md
│
├── 01-soc-l1-alert-triage/
│   └── README.md
│
├── 02-soc-l1-alert-reporting/
│   └── README.md
│
├── 03-soc-workbooks-and-lookups/
│   └── README.md
│
└── 04-soc-metrics-and-objectives/
    └── README.md
```

---

## References

* TryHackMe — SOC Level 1
