# Phishing Analysis Tools

## Overview

This room builds on the phishing analysis fundamentals and practical email investigations covered in the previous rooms.

It introduces tools and techniques that allow SOC analysts to perform deeper investigations of suspicious emails, including artifact collection, email header analysis, IP and URL reputation checks, attachment analysis, malware sandboxes, and automated phishing investigation platforms.

The room also provides hands-on experience investigating real-world phishing cases from a Level 1 SOC analyst perspective.

The main focus is developing a structured methodology for collecting indicators of compromise (IOCs), validating suspicious artifacts, and documenting investigation results.

---

## Learning Objectives

After completing this room, I am able to:

- Identify the key artifacts that should be collected during a phishing investigation.
- Analyze email headers using dedicated tools.
- Investigate sender IP addresses.
- Perform IP reputation checks.
- Analyze suspicious URLs.
- Perform URL reputation checks.
- Safely analyze email attachments.
- Generate SHA256 hashes for suspicious files.
- Use malware sandboxes to investigate suspicious attachments.
- Understand the purpose of PhishTool.
- Extract indicators of compromise from phishing emails.
- Document phishing investigation findings.
- Apply a structured phishing analysis methodology.
- Investigate phishing cases from a SOC L1 analyst perspective.

---

# Phishing Investigation Methodology

A phishing investigation begins by collecting artifacts from the suspicious email.

These artifacts provide the foundation for further investigation and threat intelligence lookups.

The investigation can be represented as:

```text
Suspicious Email
       │
       ▼
Collect Artifacts
       │
       ├── Header Information
       ├── URLs
       ├── Attachments
       └── File Hashes
       │
       ▼
Analyze Indicators
       │
       ├── IP Reputation
       ├── URL Reputation
       ├── File Reputation
       └── Sandbox Analysis
       │
       ▼
Identify Malicious Activity
       │
       ▼
Document Findings
       │
       ▼
Resolve / Escalate
```
# Identifying Artifacts

The first objective during a phishing investigation is to collect the relevant **artifacts**.

These artifacts provide the information needed for **deeper investigation**.

# Header Artifacts

Important header information includes:

## Sender Email Address

Determine where the email appears to originate from.

The sender address should be compared with the **organization or service being impersonated**.

## Sender IP Address

Identify the **source IP address** of the email.

The IP can then be investigated through **reputation and intelligence services**.

A reverse lookup may also provide additional information about the infrastructure.

## Subject Line

The subject can reveal:

* Urgency
* Suspicious requests
* Calls to action

## Recipient Address

Identify who received the email.

The recipient information may include:

* **To**
* **CC**
* **BCC**

## Reply-To Address

The **Reply-To** field identifies where responses to the email will be directed.

This can provide an additional indicator during phishing analysis.

## Date and Time

The date and time indicate when the email was sent.

This information can help establish a **timeline during an investigation**.

# Body Artifacts

The email body contains additional artifacts that should be collected.

## URLs and Hyperlinks

Identify all **URLs** contained within the email.

Shortened URLs should be expanded or investigated to determine their **true destination**.

## Attachment Names

Record the names of all attachments.

The analyst should investigate:

* File names
* File extensions
* Suspicious naming conventions

## Attachment Hash

A hash can be generated from an attachment to provide a **unique identifier** for threat intelligence lookups.

The room uses **SHA256 hashing** for this purpose.

# Email Header Analysis

Some important email information is not visible directly in the normal email client.

Examples include:

* Sender IP address
* Reply-To information
* Routing information

Previously, these details were manually extracted from the email source.

Dedicated tools can make this process faster.

## Messageheader

**Messageheader**, part of the Google Admin Toolbox, can analyze email headers.

By providing the full email header, the tool can extract information such as:

* Sender IP address
* Routing path
* Potential misconfigurations

This can help analysts quickly understand how an email traveled through mail infrastructure.

## Message Header Analyzer

**Message Header Analyzer** is another tool that can analyze email headers.

It can help extract and organize information from the header, reducing the amount of manual analysis required.

# IP Reputation Analysis

Once an IP address has been identified, the analyst can investigate its reputation.

The objective is to determine:

* Where the IP is located
* Which organization is associated with it
* Whether it has been associated with malicious activity

IP reputation information can provide additional context about the infrastructure involved in an email.

## IPinfo

**IPinfo** can be used to investigate an IP address.

It provides information such as:

* Geographic location
* Associated organization

This information can help analysts determine whether the source infrastructure appears suspicious.

# URL Analysis

URLs contained in suspicious emails should be analyzed **without directly visiting potentially malicious destinations**.

A URL can be copied from an email and investigated separately.

This allows the analyst to determine where the link points without following it directly.

## URLScan.io

**URLScan.io** allows analysts to investigate websites without directly visiting them.

The service simulates a browsing session and records activity generated by the page.

It can provide:

* Screenshots
* Page behavior
* Network activity
* Information about potentially malicious content

This makes it useful for investigating suspicious URLs safely.

## Talos IP & Domain Reputation Center

The **Talos IP & Domain Reputation Center** is a Cisco threat intelligence tool.

It can be used to investigate:

* IP addresses
* Domains
* Networks

The tool can provide reputation information and classifications associated with an indicator.

# Email Body Analysis

The email body is often where the malicious intent becomes visible.

Phishing emails commonly deliver malicious content through:

* Hyperlinks
* Attachments

Links can be extracted from:

* Visible email content
* HTML source
* Raw email source

This is important because malicious URLs may be hidden or obfuscated.

## Safe URL Analysis

Instead of clicking a suspicious link, the analyst can:

1. Right-click the link.
2. Select **Copy link address**.
3. Analyze the copied URL using appropriate tools.

This allows the analyst to investigate the destination without directly visiting it.

## URL Extraction

URL extraction tools can automatically identify links embedded within raw email content.

This can:

* Save investigation time
* Reduce the chance of missing hidden URLs
* Identify obfuscated links

**CyberChef** can also be used for URL extraction and other analysis tasks.

# Email Attachment Analysis

Attachments should not be downloaded directly to a normal workstation when investigating potentially malicious emails.

They should be obtained in a:

* Controlled environment
* Lab machine
* Sandbox

This reduces the risk of accidental execution.

## SHA256 Hashing

Once an attachment has been safely obtained, a **SHA256 hash** can be generated.

Example:

```bash
sha256sum shady_attachment.pdf
```

Example output:

```text
025ba9ce4a2118a9ca7b115c8869ff73bc16bad3732ba359cef1e60ad8f961f9  shady_attachment.pdf
```

The hash can then be used for:

* Threat intelligence lookups
* File reputation checks
* Identifying known malicious files

## File Reputation

A file hash can be submitted to threat intelligence platforms to determine whether the file has previously been identified as malicious.

For example, the room demonstrates how a suspicious file can be classified as:

* Phishing
* Malicious
* Spam

This provides additional evidence about the nature of the attachment.

## VirusTotal

**VirusTotal** is a widely used threat intelligence platform.

It can be used to investigate:

* Files
* URLs
* IP addresses
* Domains

VirusTotal combines information from numerous security vendors.

This allows analysts to review:

* Detection results
* Reputation
* Security vendor classifications

VirusTotal can therefore provide valuable context during phishing investigations.

# Malware Sandboxes

Malware sandboxes allow analysts to safely observe the behavior of potentially malicious files.

Instead of executing a suspicious attachment directly on a normal system, the file can be analyzed in a **controlled environment**.

A sandbox can reveal:

* URLs contacted by the file
* Additional payloads downloaded
* Network activity
* Processes
* System changes
* Indicators of compromise

## ANY.RUN

**ANY.RUN** is an interactive malware sandbox.

It allows analysts to execute and observe suspicious files and URLs in a controlled environment.

Important capabilities include:

* Real-time process monitoring
* Network activity monitoring
* System change analysis
* Interactive investigation

This makes it useful for understanding how malicious files behave.

## Hybrid Analysis

**Hybrid Analysis** is a malware analysis sandbox that allows suspicious files to be examined in a controlled environment.

It can provide information about:

* File behavior
* System changes
* Network activity
* Indicators of compromise

## JOESandbox

**JOESandbox** is designed for advanced malware analysis.

It supports:

* Static analysis
* Dynamic analysis

It can generate reports containing:

* Malware behavior
* Indicators of compromise
* Threat classifications

# PhishTool

**PhishTool** is a platform designed to streamline phishing investigations.

It can automate many of the manual steps involved in analyzing suspicious emails.

It brings together:

* Threat intelligence
* OSINT
* Email metadata
* Automated analysis workflows

This provides analysts with a centralized view of phishing activity.

## PhishTool Artifact Analysis

After uploading an email to PhishTool, the analyst can inspect multiple components of the message.

These include:

* Rendered HTML
* Raw HTML
* Message source

This allows analysts to view the email both as the recipient sees it and in its underlying technical form.

## Further Analysis with PhishTool

PhishTool provides additional investigation capabilities through different analysis tabs.

These can include:

* Authentication results
* Transmission paths
* Embedded URLs
* Attachments

The platform also integrates with **VirusTotal**.

This allows reputation and detection information to be viewed within the phishing investigation workflow.

# Resolving a Phishing Case

After completing the investigation, PhishTool allows the analyst to document the findings.

Important artifacts can be flagged, including:

* Sender addresses
* Originating IP addresses
* Embedded URLs

The analyst can also add investigation notes.

Finally, the case can be marked as **resolved**.

This reflects the type of documentation and case closure process used in a real **SOC environment**.

# SOC L1 Perspective

In this room, the analyst assumes the role of a **Level 1 SOC Analyst**.

The L1 analyst is responsible for reviewing phishing and spam emails reported by end users.

The investigation process includes:

1. Reviewing the email.
2. Collecting important artifacts.
3. Investigating suspicious indicators.
4. Identifying signs of malicious activity.
5. Documenting findings.
6. Escalating or resolving the case as appropriate.

The results of these investigations can also help the security team develop **detection rules** to prevent similar threats from reaching other users.

# Practical Phishing Investigations

The room includes multiple hands-on investigations.

## Case 1 — Your Account Is on Hold

The analyst investigates a suspicious phishing email.

The investigation requires reviewing:

* Email header
* Email body
* Suspicious indicators

The objective is to identify signs of malicious activity and collect useful indicators.

## Case 2 — Update Payment Details

This case involves a suspicious phishing email containing a malicious attachment that impersonates a **Netflix payment notification**.

The attachment is investigated using **ANY.RUN**.

The analyst examines:

* File behavior
* Network activity
* Indicators of compromise

The goal is to understand how the attachment behaves after execution.

## Case 3 — Excel Executable

The third investigation uses **ANY.RUN** to analyze another suspicious phishing attachment.

The analyst investigates:

* Process activity
* Network connections
* Indicators of compromise
* File behavior

The objective is to understand what makes the attachment malicious and how it operates.

# Phishing Analysis Workflow

The knowledge from this room can be organized into a structured SOC workflow:

```text
User Reports Suspicious Email
            │
            ▼
       Collect Artifacts
            │
      ┌─────┴─────┐
      │           │
    Header       Body
      │           │
      ▼           ▼
Sender IP       URLs
Reply-To        Attachments
Subject
Recipient
Date/Time
      │           │
      └─────┬─────┘
            ▼
      Analyze Indicators
            │
     ┌──────┼──────┐
     │      │      │
     ▼      ▼      ▼
    IP     URL    Hash
 Reputation Reputation Reputation
     │      │      │
     └──────┼──────┘
            ▼
      Sandbox Analysis
            │
            ▼
    Identify Malicious
        Activity
            │
            ▼
      Document Findings
            │
       ┌────┴────┐
       ▼         ▼
    Resolve    Escalate
```

# Safe Analysis

Suspicious domains, URLs, IP addresses, and attachments may contain real malicious content.

Therefore, potentially dangerous artifacts should only be accessed or executed in **controlled environments**.

The room specifically warns that the domains, URLs, and IP addresses used in the practical exercises have hosted real malicious content and may still pose a risk.

Safe analysis practices include:

* Do not directly click suspicious URLs.
* Do not execute suspicious attachments on a normal workstation.
* Use controlled lab environments.
* Use malware sandboxes when appropriate.
* Use reputation services to investigate indicators.
* Treat suspicious artifacts as potentially malicious until proven otherwise.

# Skills Acquired

This room strengthened my understanding of:

* Phishing investigation methodology
* Email artifact collection
* Email header analysis
* Sender IP investigation
* IP reputation analysis
* URL reputation analysis
* URL extraction
* Attachment analysis
* SHA256 hashing
* File reputation analysis
* VirusTotal
* IPinfo
* URLScan.io
* Cisco Talos
* CyberChef
* ANY.RUN
* Hybrid Analysis
* JOESandbox
* PhishTool
* OSINT
* Threat intelligence
* Indicators of compromise
* SOC L1 phishing triage
* Case documentation
* Incident investigation

# Analyst Notes

## Key Takeaways

* A phishing investigation should begin by collecting relevant artifacts.
* Important header artifacts include sender address, sender IP, subject, recipient, Reply-To, and date/time.
* Important body artifacts include URLs, hyperlinks, attachment names, and attachment hashes.
* Email headers can reveal information that is not visible in the normal email client.
* IP reputation checks can provide context about suspicious infrastructure.
* URLs should be analyzed without directly visiting potentially malicious destinations.
* Attachments should only be downloaded in controlled environments.
* SHA256 hashes can be used to perform file reputation lookups.
* VirusTotal can provide reputation and detection information for multiple types of indicators.
* Malware sandboxes allow analysts to safely observe suspicious file behavior.
* ANY.RUN provides interactive malware analysis.
* Hybrid Analysis provides controlled malware analysis and behavioral information.
* JOESandbox supports static and dynamic analysis.
* PhishTool centralizes phishing investigation and automates many manual analysis steps.
* A SOC L1 analyst must be able to collect indicators, investigate them, document findings, and determine the appropriate next action.
* Investigation results can help create detection rules to prevent similar attacks in the future.

# New Terminology

* **Artifact**
* **Indicator of Compromise (IOC)**
* **IP Reputation**
* **URL Reputation**
* **Threat Intelligence**
* **OSINT**
* **SHA256**
* **File Hash**
* **Malware Sandbox**
* **Static Analysis**
* **Dynamic Analysis**
* **PhishTool**
* **VirusTotal**
* **IPinfo**
* **URLScan.io**
* **Talos**
* **ANY.RUN**
* **Hybrid Analysis**
* **JOESandbox**
* **Case Resolution**

# Personal Reflection

This room helped me move from basic phishing analysis toward a more structured investigation process.

Previously, I focused mainly on identifying suspicious elements within an email. This room showed me how to take those elements and investigate them further using **threat intelligence, reputation services, hashing, and malware sandboxes**.

One of the most important lessons was understanding that an indicator by itself may not provide enough evidence. An analyst should collect multiple artifacts and correlate the results to determine whether an email is malicious.

I also gained a better understanding of the role of a **SOC L1 analyst** during phishing investigations. The analyst must collect evidence, investigate suspicious indicators, document the findings, and determine whether the case should be resolved or escalated.

The introduction to tools such as **VirusTotal, ANY.RUN, and PhishTool** also demonstrated how security tools can reduce manual work and make phishing investigations more efficient.

# References

* **TryHackMe — SOC Level 1**
* **Phishing Analysis Tools**
* **Phishing Analysis Fundamentals**
* **Phishing Emails in Action**
