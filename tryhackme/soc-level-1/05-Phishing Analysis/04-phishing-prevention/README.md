# Phishing Prevention

## Overview

This room focuses on the defensive measures organizations can implement to prevent, detect, and mitigate phishing attacks.

Building on the phishing identification and investigation techniques learned in the previous rooms, this room introduces email authentication mechanisms, email security controls, SMTP analysis, and user-focused security measures.

The main technologies covered are:

* Sender Policy Framework (SPF)
* DomainKeys Identified Mail (DKIM)
* Domain-based Message Authentication, Reporting, and Conformance (DMARC)
* Secure/Multipurpose Internet Mail Extensions (S/MIME)
* SMTP analysis
* Email and attachment inspection
* Secure Email Gateways
* Email filtering
* Link rewriting
* Sandboxing
* User awareness and phishing reporting

The objective is to understand how organizations can build multiple layers of defense against phishing attacks.

---

## Learning Objectives

After completing this room, I am able to:

* Understand the purpose of SPF.
* Explain how DKIM authenticates email.
* Understand how DMARC builds on SPF and DKIM.
* Explain the role of S/MIME in email security.
* Analyze SMTP responses.
* Inspect SMTP network traffic.
* Analyze suspicious email content and attachments.
* Understand technical defenses against phishing.
* Understand user-focused phishing prevention measures.
* Explain how organizations use multiple layers of protection against phishing.

---

# Email Security Controls

Modern email security relies on several complementary mechanisms.

The main authentication technologies covered in this room are:

```text
SPF
 │
 ├── Validates the sending server
 │
 ▼
DKIM
 │
 ├── Validates the message signature
 │
 ▼
DMARC
 │
 ├── Applies policy to authentication failures
 │
 ▼
S/MIME
 │
 └── Provides message signing and encryption
```

These mechanisms address different aspects of email security.

---

# Sender Policy Framework (SPF)

## What Is SPF?

Sender Policy Framework (SPF) is an email authentication mechanism designed to reduce email spoofing.

It allows a domain owner to specify which mail servers are authorized to send email on behalf of that domain.

In simple terms:

> SPF answers the question: "Is this server authorized to send email for this domain?"

---

## How SPF Works

When an email is received:

1. The receiving mail server identifies the sender's domain.
2. It queries the domain's SPF record through DNS.
3. It identifies the sending server's IP address.
4. It compares the IP address against the SPF record.
5. The receiving server determines the SPF result.

The process can be represented as:

```text
Incoming Email
      │
      ▼
Identify Sender Domain
      │
      ▼
Query SPF Record
      │
      ▼
Check Sending IP
      │
      ▼
Compare With Authorized Servers
      │
      ▼
SPF Result
```

---

## SPF Results

An SPF check can produce different results.

Common results include:

* Pass
* Fail
* SoftFail
* Neutral
* None
* TempError
* PermError

The exact handling depends on the receiving organization's email security policy.

---

## Why SPF Matters

Without SPF, attackers can more easily spoof legitimate domains.

For example, an attacker could attempt to send:

```text
From: security@legitimate-company.com
```

from infrastructure that is not authorized by the legitimate organization.

SPF helps receiving servers identify that mismatch.

---

# DomainKeys Identified Mail (DKIM)

## What Is DKIM?

DomainKeys Identified Mail (DKIM) is an email authentication mechanism that uses cryptographic signatures.

The sending mail server signs parts of the email using a private key.

The receiving mail server can then verify the signature using the public key published in DNS.

---

## How DKIM Works

The process can be represented as:

```text
Sender
  │
  ▼
Email Created
  │
  ▼
Private Key Signs Message
  │
  ▼
Email Sent
  │
  ▼
Receiving Server
  │
  ▼
Retrieve Public Key From DNS
  │
  ▼
Verify Signature
  │
  ▼
DKIM Result
```

---

## DKIM DNS Record

A DKIM public key is published as a DNS TXT record.

A simplified example is:

```text
v=DKIM1; k=rsa; p=<public_key>
```

Where:

* `v` specifies the DKIM version.
* `k` identifies the cryptographic algorithm.
* `p` contains the public key.

---

## Why DKIM Matters

DKIM provides integrity and authentication information about the email.

Unlike SPF, which evaluates the sending server's IP address, DKIM validates a cryptographic signature associated with the message.

This makes DKIM useful even when an email passes through multiple mail servers.

---

# Domain-based Message Authentication, Reporting, and Conformance (DMARC)

## What Is DMARC?

DMARC builds on SPF and DKIM.

It allows domain owners to publish a policy describing how receiving mail servers should handle messages that fail authentication checks.

DMARC also provides reporting capabilities that give domain owners visibility into email authentication activity.

---

## DMARC Policies

The main DMARC policies are:

### `p=none`

The receiving server should monitor the authentication results without enforcing a blocking action.

This is commonly used during initial DMARC deployment.

### `p=quarantine`

Messages that fail DMARC should be treated as suspicious.

They may be placed into spam or another quarantine location.

### `p=reject`

Messages that fail DMARC should be rejected.

This provides the strongest enforcement level.

---

## DMARC Policy Progression

A common progression is:

```text
p=none
   │
   ▼
Monitor
   │
   ▼
p=quarantine
   │
   ▼
Quarantine Suspicious Messages
   │
   ▼
p=reject
   │
   ▼
Reject Failing Messages
```

---

## Why DMARC Matters

DMARC helps organizations:

* Reduce domain spoofing.
* Protect their brand.
* Enforce email authentication.
* Investigate phishing campaigns.
* Obtain visibility through authentication reports.

From a SOC perspective, DMARC can help determine whether suspicious emails claiming to originate from an organization's domain were legitimately authorized.

---

# SPF vs DKIM vs DMARC

These technologies solve different problems.

| Technology | Main Purpose                                             |
| ---------- | -------------------------------------------------------- |
| SPF        | Validates whether the sending server is authorized       |
| DKIM       | Validates the cryptographic signature of the message     |
| DMARC      | Defines policy and reporting for authentication failures |

A useful way to remember them is:

```text
SPF   → Where did the email come from?
DKIM  → Was the signed message altered?
DMARC → What should happen if authentication fails?
```

Together, they form an important foundation for email security.

---

# Secure/Multipurpose Internet Mail Extensions (S/MIME)

## What Is S/MIME?

S/MIME provides cryptographic security for email.

It can provide:

* Message signing.
* Encryption.

Digital signatures can help verify the sender's identity and provide message integrity.

Encryption helps protect the confidentiality of email content.

---

## S/MIME and Phishing Prevention

S/MIME can provide stronger assurance about the identity of the sender when properly implemented.

However, it should be considered another layer of email security rather than a replacement for other controls.

---

# SMTP

## What Is SMTP?

Simple Mail Transfer Protocol (SMTP) is the protocol commonly used to transfer email between mail systems.

During an email transaction, SMTP servers exchange commands and responses.

Analyzing this communication can provide useful information during security investigations.

---

# SMTP Response Codes

SMTP uses response codes to communicate the status of email operations.

Common categories include:

```text
2xx → Successful operation
4xx → Temporary failure
5xx → Permanent failure
```

These responses can help an analyst understand how a mail server handled an email.

---

## SMTP Analysis

Analyzing SMTP traffic can help identify:

* Successful delivery.
* Failed delivery.
* Rejected messages.
* Suspicious attachments.
* Email clients.
* Communication between mail servers.

Network traffic analysis therefore provides another perspective for investigating phishing-related activity.

---

# Inspecting Emails and Attachments

Email analysis should not stop at the visible message.

Analysts can inspect:

* Email headers.
* Email body.
* SMTP traffic.
* Attachments.
* Encoded content.
* File types.

Attachments may contain malicious content that is hidden behind apparently legitimate file names.

---

## Attachment Encoding

Email attachments may be encoded before being transmitted.

Understanding email encoding allows analysts to recognize how attachments are represented within email traffic.

This can help identify potentially malicious files during network analysis.

---

# Technical Phishing Defenses

Organizations can implement multiple technical controls to reduce phishing risk.

---

## Email Filtering

Email filtering systems can analyze incoming messages using information such as:

* IP reputation.
* Domain reputation.
* Sender reputation.
* Email content.
* URLs.
* Attachments.

Suspicious messages can be:

* Blocked.
* Quarantined.
* Flagged for further investigation.

---

## Secure Email Gateways

Secure Email Gateways (SEGs) provide an additional layer of protection between the internet and an organization's mail infrastructure.

They can help detect:

* Spoofing.
* Impersonation.
* Malicious attachments.
* Suspicious URLs.
* Advanced phishing techniques.

---

## Link Rewriting

Link rewriting can replace URLs contained within emails with security-controlled links.

When the user clicks the link, the security system can analyze the destination before allowing access.

This provides an additional opportunity to detect malicious websites.

---

## Sandboxing

Sandboxing allows potentially dangerous content to be executed in an isolated environment.

For example, a suspicious attachment can be analyzed without exposing a normal employee workstation to the malware.

The sandbox can observe:

* Processes.
* Network connections.
* File changes.
* Malicious behavior.

This makes sandboxing particularly useful for detecting hidden malware inside attachments.

---

# User-Focused Phishing Defenses

Technical controls alone are not enough.

Users are also an important part of an organization's phishing defense.

---

## Warning Indicators

Email security systems can display warnings such as:

```text
External Sender
```

or:

```text
Suspicious Link
```

These indicators help users recognize potentially dangerous messages.

---

## Phishing Reporting

Organizations should provide a simple mechanism for users to report suspicious emails.

This allows security teams to:

* Investigate reported messages.
* Identify phishing campaigns.
* Block malicious indicators.
* Protect other users.

---

## Security Awareness Training

Security awareness training teaches employees how to recognize phishing techniques.

Training may cover:

* Suspicious links.
* Fake login pages.
* Spoofed senders.
* Malicious attachments.
* Social engineering.

---

## Phishing Simulations

Organizations can use controlled phishing simulations to test employee awareness.

The goal is not simply to punish users for clicking.

Instead, simulations can help:

* Measure awareness.
* Identify areas requiring additional training.
* Reinforce secure behavior.

---

# Defense in Depth

One of the most important concepts from this room is that phishing prevention should use multiple layers.

A simplified defense model is:

```text
                    INTERNET
                       │
                       ▼
               Email Authentication
               SPF / DKIM / DMARC
                       │
                       ▼
                Email Filtering
                       │
                       ▼
             Secure Email Gateway
                       │
                       ▼
             URL / Attachment Scan
                       │
                 ┌─────┴─────┐
                 ▼           ▼
             Link Scan    Sandbox
                 │           │
                 └─────┬─────┘
                       ▼
                 User Receives
                    Email
                       │
                       ▼
              User Awareness
                       │
                       ▼
               Phishing Report
                       │
                       ▼
                  SOC Analysis
```

If one layer fails, another layer may still prevent the attack from reaching its objective.

---

# SOC Analyst Perspective

Phishing prevention is directly connected to the work of a SOC Analyst.

A SOC may receive reports from:

* Email security systems.
* Secure Email Gateways.
* Users.
* SIEM platforms.
* Endpoint security systems.

The analyst can investigate:

* Sender information.
* IP addresses.
* Domains.
* URLs.
* Attachments.
* Authentication results.

The resulting intelligence can then be used to improve defensive controls.

---

# Incident Response Connection

Phishing prevention is not limited to blocking emails.

If a malicious email reaches a user, the SOC may need to:

1. Investigate the email.
2. Identify affected users.
3. Extract indicators.
4. Search for similar emails.
5. Block malicious domains or URLs.
6. Remove malicious messages.
7. Investigate possible credential compromise.
8. Escalate the incident if necessary.

This demonstrates the connection between:

```text
Prevention
    ↓
Detection
    ↓
Investigation
    ↓
Response
    ↓
Improved Prevention
```

---

# Phishing Prevention Strategy

An effective organizational strategy combines technical and human controls.

```text
Technical Controls
       +
Email Authentication
       +
Email Filtering
       +
Secure Email Gateway
       +
URL Analysis
       +
Sandboxing
       +
User Awareness
       +
Phishing Reporting
       │
       ▼
Reduced Phishing Risk
```

No single security control can prevent every phishing attack.

---

# Skills Acquired

This room strengthened my understanding of:

* Email security.
* SPF.
* DKIM.
* DMARC.
* S/MIME.
* SMTP.
* SMTP response codes.
* SMTP traffic analysis.
* Email filtering.
* Secure Email Gateways.
* Link rewriting.
* Sandboxing.
* User awareness.
* Phishing reporting.
* Phishing simulations.
* Defense in depth.
* Email authentication.
* Phishing prevention.
* SOC phishing defense.

---

# Analyst Notes

## Key Takeaways

* Phishing is a major initial access technique.
* SPF helps validate whether a server is authorized to send email for a domain.
* DKIM uses cryptographic signatures to help verify message authenticity and integrity.
* DMARC builds on SPF and DKIM and provides enforcement policies and reporting.
* `p=none` is primarily a monitoring policy.
* `p=quarantine` instructs receiving systems to treat failing messages as suspicious.
* `p=reject` provides the strongest enforcement by rejecting failing messages.
* S/MIME can provide email signing and encryption.
* SMTP analysis can reveal useful information about email delivery and communication.
* Email filtering can block or quarantine suspicious messages.
* Secure Email Gateways provide additional protection against phishing and impersonation.
* Link rewriting allows URLs to be inspected when users interact with them.
* Sandboxing provides a safe environment for analyzing suspicious attachments and links.
* User awareness remains an important part of phishing prevention.
* Phishing reporting allows the SOC to investigate and respond to suspicious messages.
* Effective phishing defense requires multiple security layers.

---

## New Terminology

* SPF
* DKIM
* DMARC
* S/MIME
* SMTP
* SMTP Response Code
* Email Authentication
* Secure Email Gateway
* Email Filtering
* Link Rewriting
* Sandboxing
* Phishing Simulation
* Security Awareness
* Defense in Depth
* Phishing Reporting

---

## Personal Reflection

This room helped me understand that phishing defense is not only about detecting suspicious emails after they reach users.

Organizations can implement multiple controls before, during, and after email delivery to reduce the probability of a successful phishing attack.

The most important concepts for me were SPF, DKIM, and DMARC because they demonstrate how email authentication can reduce spoofing and provide organizations with greater visibility into email activity.

I also learned that technical controls such as email filtering, Secure Email Gateways, link rewriting, and sandboxing should be combined with user awareness and phishing reporting.

From a SOC perspective, phishing prevention is closely connected with detection and incident response. When a suspicious email is reported, the SOC can investigate its indicators, identify other affected users, block malicious infrastructure, and use the findings to improve future defenses.

This reinforced the importance of defense in depth: security should not depend on a single control.

---

## References

* TryHackMe — SOC Level 1
* Phishing Analysis Module
* Phishing Analysis Fundamentals
* Phishing Emails in Action
* Phishing Analysis Tools
* Phishing Prevention
