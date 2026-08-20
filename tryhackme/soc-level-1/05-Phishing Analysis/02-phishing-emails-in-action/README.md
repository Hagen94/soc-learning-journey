# Phishing Analysis

## Overview

This room provides practical experience analyzing real phishing email samples.

Building on the fundamentals learned in the previous room, this room focuses on identifying the techniques attackers use to imitate legitimate communications and manipulate users into interacting with malicious content.

The analysis covers:

- Email headers
- Email bodies
- Spoofed sender addresses
- URL manipulation
- URL shortening
- Tracking pixels
- Credential harvesting
- Malicious attachments
- Brand impersonation
- Social engineering
- Multi-stage redirection
- Malicious payload execution

The objective is to develop the ability to distinguish legitimate communications from sophisticated phishing attempts by identifying multiple indicators of compromise.

---

## Learning Objectives

After completing this room, I am able to:

- Identify common social engineering tactics used in phishing.
- Analyze red flags contained within phishing emails.
- Detect link manipulation.
- Identify tracking pixels.
- Analyze credential harvesting techniques.
- Identify attachment manipulation.
- Recognize spoofed sender addresses.
- Identify brand impersonation.
- Analyze suspicious URLs and redirections.
- Identify malicious attachments.
- Recognize indicators of malicious payload execution.
- Apply the phishing analysis techniques learned in the previous room to real samples.

---

# Phishing Analysis Approach

A phishing investigation should not rely on a single indicator.

Instead, the analyst should examine multiple components of the email:

```text
Suspicious Email
       │
       ├── Header
       │     ├── From
       │     ├── To
       │     └── Subject
       │
       ├── Body
       │     ├── Text
       │     ├── HTML
       │     └── Branding
       │
       ├── Links
       │     ├── Destination
       │     ├── Redirections
       │     └── Tracking
       │
       └── Attachments
             ├── File type
             ├── Embedded links
             └── Payloads
```
The combination of these observations helps determine whether an email is malicious.

## Sample 1 — Cancel Your Order

The first sample imitates an official PayPal transaction receipt.

The attacker attempts to make the message appear legitimate by using PayPal branding and a fake transaction.

# Phishing Techniques Used

* Spoofed email address.
* URL shortening.
* Branded HTML.
* Social engineering through urgency.

## Initial Observations

# Subject

The subject describes a fake transaction.

This creates urgency and encourages the recipient to react quickly.

# From Address

The displayed sender appears to be:
```text
service@paypal.com
```
However, the actual address is:
```text
gibberish@sultanbogor.com
```
The mismatch is an immediate red flag.

# To Address

The recipient address is unusual and does not appear to be a normal Yahoo address.

# Email Body

The body is designed to look like a legitimate PayPal receipt for a gift card purchase.

There are no attachments.

The main interactive element is the:
```text
Cancel the order
```
button.

# Button Investigation

Inspecting the raw email source reveals that the button points to a shortened URL.

The use of URL shortening hides the final destination.

This makes it difficult to determine where the user will be redirected simply by looking at the link.

A useful principle during analysis is:

Never interact with a suspicious link before confirming its destination.

Tools such as WhereGoes can be used to investigate shortened URLs without directly visiting the final destination.

## Sample 2 — Track Your Package

The second sample impersonates a shipping notification.

The attacker uses a fake tracking number to create urgency and encourage the recipient to click the link.

* Phishing Techniques Used
* Spoofed email address.
* Tracking pixels.
* Link manipulation.
* Social engineering through urgency.

## Initial Observations

# Subject

The subject contains a fake tracking number.

The objective is to create urgency and encourage the recipient to check the package status.

# From Address

The display name is:
```text
Distribution Center
```
However, the actual sender address is:
```text
contact@beginpro.club
```
The mismatch between the displayed sender and actual domain is a red flag.

# Hyperlink

The hyperlink appears to correspond with the tracking information in the email.

However, its final destination is not immediately known.

## Tracking Pixels

The email contains a tracking image.

Tracking pixels are very small or invisible images embedded into emails.

They can notify the sender when the email is opened.

The tracking mechanism can send information back to the attacker's or spammer's server.

Email providers may automatically block images in suspicious messages to prevent this type of tracking.

Inspecting the raw email source can reveal the image source and associated tracking information.

## Sample 3 — Download Document Here

This sample uses a multi-stage redirection chain to harvest user credentials.

The attacker abuses the reputation of legitimate services and brands, including:

* OneDrive
* Adobe
* Microsoft

The objective is to guide the victim through multiple stages until reaching a fraudulent login page.

# Phishing Techniques Used

* Artificial urgency.
* Brand impersonation.
* Link redirection.
* Credential harvesting.

## Initial Observations

# Send Date

The email was sent on:
```text
Thursday, July 15th, 2021
```
# Expiration Date

The document download link is presented as expiring on the same day.

This creates an artificial sense of urgency.

# Download Button

The email contains a:
```text
Download Document Here
```
button.

## Multi-Stage Redirection

The initial button redirects the user to a page that imitates a legitimate OneDrive document-sharing page.

The interaction then triggers another redirection to a page impersonating Adobe.

Finally, the victim reaches a fraudulent login portal.

The workflow can be represented as:
```text
Phishing Email
      │
      ▼
Download Document
      │
      ▼
Fake OneDrive Page
      │
      ▼
Fake Adobe Page
      │
      ▼
Fake Login Portal
      │
      ▼
Credential Harvesting
```

## Credential Harvesting

The final page asks the victim to log in using their email provider.

In the sample, the victim attempts to log in using Outlook.

The page does not actually authenticate the user with the legitimate email provider.

Instead, the credentials are sent directly to the attacker's server.

The displayed error message is therefore used as a distraction.

## Important Observation

Poor grammar and formatting can be useful phishing indicators.

However, they should not be treated as the only indicator.

Attackers can now use AI to generate polished and grammatically correct phishing messages.

Therefore:
```text
No spelling mistakes
        ≠
Legitimate email
```
## Sample 4 — Your Account Is on Hold

This sample impersonates a Netflix billing notification.

Instead of using a direct malicious link in the email body, the attacker uses an attachment to hide the malicious destination.

* Phishing Techniques Used
* Spoofed email address.
* Sense of urgency.
* Brand impersonation.
* Poor grammar and typos.
* Malicious attachment.

## Initial Observations

# Subject

The email claims that the recipient's account has been suspended.

This creates urgency and pressures the victim to act quickly.

# From Address

The display name is:
```text
Netllx billing
```
The spelling itself is suspicious.

The sender details also do not match a legitimate Netflix domain.

# Brand Impersonation

The email uses HTML and logos designed to imitate Netflix.

## Attachment Analysis

The email tells the user to open an attached PDF to update billing information.

The PDF contains an embedded link:

```text
Update Payment Account
```
The link redirects to a URL that is not associated with a legitimate Netflix domain.

Additional indicators include:

* An unusual phone number format.
* Use of a legitimate Netflix help-center domain to create false trust.
* A suspicious embedded destination.

## Sample 5 — Your Recent Purchase

This sample impersonates an Apple billing notification.

Unlike previous examples, the email body is completely blank.

The attack relies almost entirely on the attachment.

## Phishing Techniques Used

* Spoofed email address.
* BCC usage.
* Sense of urgency.
* Poor grammar and typos.
* Suspicious attachment.

## Initial Observations

# Subject

The recipient is told that an unauthorized purchase requires immediate action.

This creates a false sense of urgency.

# From Address

The display name is:
```text
Apple Support
```
However, the actual sender information does not match a legitimate Apple address.

There are also typos in the From and To addresses.

## BCC

The victim was not directly addressed.

Instead, the email was sent using:
```text
BCC
```
This is another suspicious characteristic.

## Attachment Analysis

The email body is completely blank.

The only content is a:
```text
.dot
```
Microsoft Word Template file.

This is unusual for a purchase receipt.

When the embedded image inside the document is interacted with, it redirects the user to a phishing site.

The URL contains familiar terms such as:
```text
apps
ios
```
However, the URL is excessively long and complex.

This is a strong indicator of malicious redirection.

# Sample 6 — Scheduled Shipment

This sample impersonates DHL Express and uses an Excel attachment as part of the attack chain.

* Phishing Techniques Used
* Spoofed email address.
* Brand impersonation.
* Malicious attachment.
* Hidden executable payload.

## Initial Observations

# Subject

The subject gives the impression that DHL is preparing to ship a package.

F# rom Address

The display name is:
```text
DHL Express
```
However, the actual sender address does not match a legitimate DHL domain.

# Brand Impersonation

The email body uses HTML templates and logos to imitate DHL.

## Attachment Analysis

The main component of the attack is the attached:
```text
.xlsx
```
file.

The document contains several inconsistencies:

* The sender uses a German domain.
* The invoice is addressed to a city in India.
* The document content is written in Mandarin.

These conflicting geographical indicators are strong red flags.

The document also contains a clickable link.

## Malicious Payload

The link inside the Excel document attempts to download and execute:
```text
regasms.exe
```
The execution results in a system error in the analysis environment.

Although the payload does not successfully execute in this environment, the attempt demonstrates the attacker's intent to execute malicious code on the victim's system.

If successfully executed, the payload could potentially:

# Establish Persistence

Create mechanisms such as:

* Backdoors.
* Scheduled tasks.

This would allow the attacker to maintain access after a reboot.

# Exfiltrate Data

Steal:

* Sensitive files.
* Credentials.
* Browser-stored passwords.

# Deploy Ransomware

Encrypt the victim's system and demand payment for recovery.

## Common Phishing Indicators

Across the analyzed samples, several indicators appear repeatedly.

# Spoofed Sender Addresses

The displayed sender name or address does not correspond to the actual domain.

Examples include impersonating:

* PayPal.
* Shipping companies.
* Netflix.
* Apple.
* DHL.

## Urgency

Attackers attempt to make victims act quickly.

Examples include:

* Fake purchases.
* Suspended accounts.
* Expiring documents.
* Package tracking.
* Unauthorized transactions.

Urgency reduces the amount of time the victim spends evaluating the message.

## Brand Impersonation

Attackers use:

* Logos.
* HTML templates.
* Corporate names.
* Familiar services.

The objective is to create a false sense of legitimacy.

## URL Manipulation

Attackers may use:

* URL shorteners.
* Redirect chains.
* Masked hyperlinks.
* Excessively long URLs.

The objective is to hide the final destination.

## Tracking Pixels

Invisible images can be embedded into emails to notify the sender when a message is opened.

## Credential Harvesting

Attackers can create fake login portals designed to capture:

* Usernames.
* Passwords.

The victim may believe they are authenticating to a legitimate service when the credentials are actually sent to the attacker.

## Malicious Attachments

Attachments can be used to:

Hide malicious URLs.
Redirect victims.
Execute malicious code.
Deliver payloads.

Examples observed in the samples include:

* PDF
* .dot
* .xlsx

## Phishing Analysis Workflow

Based on the samples analyzed in this room, a practical investigation can follow this process:
```text
Suspicious Email
       │
       ▼
Analyze Header
       │
       ├── From
       ├── To
       └── Subject
       │
       ▼
Analyze Email Body
       │
       ├── Branding
       ├── Urgency
       └── Social Engineering
       │
       ▼
Inspect Links
       │
       ├── Destination
       ├── URL Shortening
       ├── Redirections
       └── Tracking
       │
       ▼
Inspect Attachments
       │
       ├── File Type
       ├── Embedded Links
       └── Payloads
       │
       ▼
Identify Indicators
       │
       ▼
Determine Malicious Intent
```
## Safe Analysis

The samples in this room contain information from real emails.

When performing phishing analysis, suspicious:

* IP addresses.
* Domains.
* URLs.
* Attachments.

should be handled carefully.

The analyst should avoid interacting directly with potentially malicious resources unless the analysis environment is specifically designed for that purpose.

Previously learned techniques such as examining raw email source and investigating URLs without directly visiting malicious destinations should be preferred.

## SOC Analyst Perspective

A SOC analyst must be able to distinguish legitimate communications from malicious ones.

The examples in this room demonstrate that phishing attacks can use several techniques simultaneously.

A single email may contain:
```text
Spoofed Sender
      +
Urgency
      +
Brand Impersonation
      +
Suspicious Link
      +
Malicious Attachment
```
Therefore, effective phishing analysis requires examining the entire email rather than relying on a single indicator.

## Skills Acquired

This room strengthened my understanding of:

* Practical phishing analysis.
* Social engineering.
* Spoofed email addresses.
* Brand impersonation.
* URL shortening.
* Link manipulation.
* URL redirection.
* Tracking pixels.
* Credential harvesting.
* Malicious attachments.
* BCC analysis.
* HTML email analysis.
* Multi-stage phishing attacks.
* Suspicious URL analysis.
* Malicious payloads.
* Persistence.
* Data exfiltration.
* Ransomware deployment.
* Phishing investigation methodology.

## Analyst Notes

# Key Takeaways

* Phishing attacks often imitate trusted organizations to gain credibility.
* Spoofed sender addresses are a common phishing indicator.
* A displayed sender name should not automatically be trusted.
* URL shortening can hide the final destination of a malicious link.
* Redirect chains can make malicious destinations more difficult to identify.
* Tracking pixels can notify attackers when an email is opened.
* Urgency is commonly used to pressure victims into acting without careful analysis.
* Brand impersonation can make malicious emails appear legitimate.
* Credential harvesting attacks can use fake login portals to steal usernames and passwords.
* Malicious attachments can contain embedded links or executable payloads.
* A blank email body can still be malicious if an attachment is present.
* BCC usage can be another suspicious characteristic.
* Conflicting domains, locations, languages, and branding can reveal inconsistencies.
* Grammar mistakes can be useful indicators, but they are becoming less reliable because attackers can use AI to generate polished content.
* A phishing investigation should analyze headers, body content, links, and attachments together.
* The ultimate goal is to identify the attacker's intent and determine whether the communication is malicious.

## New Terminology
* Spoofed Email Address
* URL Shortening
* URL Redirection
* Tracking Pixel
* Credential Harvesting
* Brand Impersonation
* Social Engineering
* BCC
* Multi-Stage Redirection
* Malicious Payload
* Persistence
* Data Exfiltration
* Ransomware
* Phishing Campaign

## Personal Reflection

This room allowed me to apply the concepts learned in Phishing Analysis Fundamentals to realistic phishing samples.

The most important lesson was that phishing emails can look convincing when attackers combine legitimate branding, urgent messages, manipulated links, and suspicious attachments.

I learned that effective analysis requires looking beyond the visual appearance of an email. The sender address, headers, HTML source, links, redirections, attachments, and other inconsistencies can reveal the attack.

Another important lesson is that individual indicators should not be analyzed in isolation. A suspicious sender address combined with urgency, brand impersonation, and a malicious link provides much stronger evidence of phishing.

This room strengthened my ability to approach phishing emails systematically from a SOC analyst perspective.

## References
* TryHackMe — SOC Level 1
* Phishing Analysis
* Phishing Analysis Fundamentals