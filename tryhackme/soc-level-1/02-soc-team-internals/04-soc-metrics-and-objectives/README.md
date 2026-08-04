# SOC Metrics and Objectives

## Overview

This room explains how SOC performance and efficiency can be measured using different indicators and metrics.

It introduces key SOC metrics such as **Alerts Count, False Positive Rate, Alert Escalation Rate, Threat Detection Rate, MTTD, MTTA, and MTTR**.

The room also explains the importance of Service Level Agreements (SLAs), how metrics can be improved, and how L1 analysts can identify and communicate performance issues within the SOC.

---

## Learning Objectives

After completing this room, I am able to:

* Understand the purpose of SOC performance metrics.
* Understand Alerts Count and what it measures.
* Explain the False Positive Rate.
* Understand the Alert Escalation Rate.
* Understand the Threat Detection Rate.
* Explain SLA, MTTD, MTTA, and MTTR.
* Identify problems indicated by poor metric values.
* Understand how SOC metrics can be improved.
* Recognize the role of an L1 analyst in improving SOC performance.

---

# Core SOC Metrics

The main goal of a SOC is to protect the **confidentiality, integrity, and availability** of an organization's digital assets.

SOC teams achieve this by developing, receiving, and triaging security alerts.

The L1 analyst's role is to reliably identify and report **True Positives** to L2.

The room introduces four core metrics for evaluating this process.

---

## Alerts Count

**Alerts Count (AC)** measures the total number of alerts received.

```text id="5h7m2k"
AC = Total Count of Alerts Received
```

### What it measures

The overall workload of SOC analysts.

A very high number of alerts can overwhelm analysts and increase the possibility of missing real threats.

However, an extremely low number of alerts can also be concerning because it may indicate problems with SIEM visibility or detection.

The room gives **5 to 30 alerts per day per L1 analyst** as a general metric, although the ideal value depends on the organization's size.

---

## False Positive Rate

**False Positive Rate (FPR)** measures the amount of alert noise.

```text id="t4n8qd"
FPR = False Positives / Total Alerts
```

A high False Positive Rate means that analysts are spending significant time investigating activity that does not represent a real threat.

This can reduce analyst vigilance and increase the possibility of missing actual threats.

A 0% False Positive Rate is considered an unachievable ideal, while **80% or higher** is identified in the room as a serious problem.

This can require **False Positive Remediation**, such as tuning detection rules and tools.

---

## Alert Escalation Rate

**Alert Escalation Rate (AER)** measures how often alerts are escalated.

```text id="8v2k9p"
AER = Escalated Alerts / Total Alerts
```

L2 analysts rely on L1 analysts to filter out noise and escalate actionable threats.

The metric can also provide an indication of the experience and independence of L1 analysts.

The room states that this rate is usually aimed to be:

* Below 50%
* Ideally below 20%

However, L1 analysts should not avoid escalation simply because they want to maintain a lower rate. If an alert is not fully understood, senior support should be requested.

---

## Threat Detection Rate

**Threat Detection Rate (TDR)** measures how reliably the SOC detects threats.

```text id="z5r4mh"
TDR = Detected Threats / Total Threats
```

The room emphasizes that the Threat Detection Rate should ideally be **100%**, because every missed threat can have serious consequences such as ransomware or data exfiltration.

A low TDR may result from:

* Broken detection rules.
* Missed alerts.
* Incorrect alert classification.

---

# Triage Performance Metrics

An alert by itself does not stop an attack.

The SOC needs to:

```text id="h4k6pt"
DETECT
  ↓
ACKNOWLEDGE
  ↓
TRIAGE
  ↓
RESPOND
```

The speed of these processes is commonly measured using **MTTD, MTTA, and MTTR**.

These requirements are often included in a **Service Level Agreement (SLA)** between the SOC and its management or customers.

---

# Service Level Agreement

A **Service Level Agreement (SLA)** defines service requirements and expected performance between parties.

In the context of the room, SLAs can define requirements related to:

* Threat detection.
* Alert acknowledgement.
* Response to threats.

Different teams may use different definitions or formulas for their metrics.

---

## Mean Time to Detect — MTTD

**MTTD** measures the average time between an attack occurring and its detection by SOC tools.

The reference SLA in the room is:

```text id="u9q3ca"
MTTD → 5 minutes
```

A high MTTD means the SOC is taking too long to detect threats.

---

## Mean Time to Acknowledge — MTTA

**MTTA** measures the average time it takes L1 analysts to begin triaging a new alert.

The reference SLA in the room is:

```text id="b7m4sn"
MTTA → 10 minutes
```

A high MTTA indicates that alerts are waiting too long before an analyst begins the triage process.

---

## Mean Time to Respond — MTTR

**MTTR** measures the average time taken by the SOC to actually stop a breach from spreading.

The reference SLA in the room is:

```text id="v3k8px"
MTTR → 60 minutes
```

Examples of response actions include:

* Isolating a device.
* Securing a compromised account.

---

# SOC Metrics Reference

| Metric                | Formula / Value          | What It Measures                        |
| --------------------- | ------------------------ | --------------------------------------- |
| Alerts Count          | Total alerts             | Overall SOC analyst workload            |
| False Positive Rate   | FP / Total Alerts        | Alert noise                             |
| Alert Escalation Rate | Escalated / Total Alerts | L1 experience and independence          |
| Threat Detection Rate | Detected / Total Threats | SOC detection reliability               |
| MTTD                  | 5 min SLA                | Time to detect a threat                 |
| MTTA                  | 10 min SLA               | Time for L1 to acknowledge/start triage |
| MTTR                  | 60 min SLA               | Time to stop the breach from spreading  |

These values come from the reference tables provided in the room.

---

# Improving SOC Metrics

Metrics are designed to make the SOC more efficient and reduce the success of attacks.

They can also be used to evaluate analyst performance and support career progression.

The room provides recommendations for several problematic metrics.

---

## High False Positive Rate

### Problem

**FPR > 80%**

The SOC receives excessive alert noise.

### Possible improvements

* Exclude trusted activities from EDR or SIEM detection rules.
* Automate common alert triage using SOAR or custom scripts.
* Tune detection rules.

---

## High MTTD

### Problem

**MTTD > 30 minutes**

Threats are being detected too slowly.

### Possible improvements

* Contact SOC engineers to improve detection rules.
* Ensure SIEM logs are collected in real time.
* Check for delays in log collection.

---

## High MTTA

### Problem

**MTTA > 30 minutes**

L1 analysts are starting alert triage too slowly.

### Possible improvements

* Ensure analysts receive real-time notifications.
* Distribute alerts evenly between analysts on shift.

---

## High MTTR

### Problem

**MTTR > 4 hours**

The SOC is unable to stop breaches quickly enough.

### Possible improvements

* Escalate threats to L2 quickly.
* Ensure attack scenarios have documented procedures.

---

# Role of the SOC L1 Analyst

Although tracking metrics is usually the responsibility of the SOC manager, L1 analysts are often the first people to notice problems.

An L1 analyst may notice:

* Excessive alert volume.
* A high False Positive Rate.
* Delays in alert triage.
* Problems with detection.
* Issues affecting response time.

The analyst should be able to communicate these problems and understand what actions may help improve the situation.

---

# Metrics Workflow

The main concepts can be connected through the following workflow:

```text id="c1v7bx"
                SECURITY EVENT
                      ↓
                  DETECTION
                      ↓
                    MTTD
                      ↓
                  NEW ALERT
                      ↓
                    MTTA
                      ↓
                 L1 TRIAGE
                      ↓
               TRUE POSITIVE
                      ↓
                 ESCALATION
                      ↓
                    MTTR
                      ↓
                   RESPONSE
```

At the same time, metrics such as **FPR, AER, TDR, and Alerts Count** help evaluate the overall effectiveness and workload of the SOC.

---

# Skills Acquired

This room strengthened my understanding of:

* SOC performance metrics
* Alerts Count
* False Positive Rate
* Alert Escalation Rate
* Threat Detection Rate
* Service Level Agreements
* MTTD
* MTTA
* MTTR
* SOC performance improvement
* Alert workload
* L1 analyst performance
* Metric-related communication

---

# Analyst Notes

## Key Takeaways

* SOC performance can be evaluated using different metrics.
* Alerts Count helps measure the overall workload of SOC analysts.
* A high False Positive Rate creates alert noise and can reduce analyst vigilance.
* Alert Escalation Rate can provide insight into L1 analyst experience and independence.
* Threat Detection Rate measures how reliably the SOC detects threats.
* MTTD measures how quickly threats are detected.
* MTTA measures how quickly L1 analysts begin triage.
* MTTR measures how quickly the SOC stops a breach from spreading.
* SLAs can define expected performance requirements.
* L1 analysts can identify metric-related problems because they work directly with alerts.
* Improving metrics can require detection tuning, automation, better notification, workload distribution, and documented response procedures.

---

## New Terminology

* Alerts Count
* False Positive Rate
* Alert Escalation Rate
* Threat Detection Rate
* SLA
* MTTD
* MTTA
* MTTR
* False Positive Remediation
* SOC Performance Metrics

---

## Personal Reflection

This room helped me understand that SOC operations are not measured only by the number of alerts analysts investigate.

The SOC also needs to evaluate how effectively it detects threats, how much alert noise analysts receive, how quickly alerts are acknowledged, and how quickly threats can be contained.

As an L1 analyst, understanding these metrics is important because my work directly contributes to several of them. Recognizing problems such as excessive alert volume, high False Positive rates, or delays in triage can help identify opportunities to improve SOC operations.

---

## References

* TryHackMe — SOC Level 1
* SOC Metrics and Objectives room
