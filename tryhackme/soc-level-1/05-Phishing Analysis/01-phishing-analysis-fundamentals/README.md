# Phishing Analysis Fundamentals

## Overview

This room introduces the fundamental concepts required to analyze suspicious emails and identify potential phishing attacks.

It covers the structure of email addresses, email delivery protocols, email headers, email bodies, attachments, and common types of phishing.

The room also introduces techniques for safely analyzing suspicious emails and identifying indicators that may reveal malicious intent.

As a SOC analyst, understanding how to analyze email components is important for determining whether a message is malicious or benign and for gathering information that can help improve an organization's security posture.

---

## Learning Objectives

After completing this room, I am able to:

- Understand the basic structure of an email address.
- Understand how emails are delivered.
- Explain the roles of SMTP, POP3, and IMAP.
- Analyze email headers.
- Inspect the raw source of an email.
- Analyze email bodies and HTML source code.
- Identify embedded links and images.
- Understand how email attachments are stored.
- Identify common types of phishing.
- Recognize characteristics of phishing emails.
- Safely analyze suspicious URLs and email addresses.
- Identify potential security threats within an email.

---

# Email Address

An email address consists of several components that determine where an email should be delivered.

The three main components are:

```text
username@domain
```
# Username

The username identifies the specific recipient's mailbox on the email server.

@ Symbol

The @ symbol separates the username from the domain.

# Domain Name

The domain identifies the mail server responsible for receiving the message.

For example:
```text
david@tryhackme.com
```
In this example:

* david → Username
* @ → Separates the username and domain
* tryhackme.com → Domain

## Email Delivery

Several protocols work together to send and receive email.

# SMTP

Simple Mail Transfer Protocol (SMTP) is used to send emails.

The sender's email client communicates with the sender's mail server using SMTP.

# POP3

Post Office Protocol 3 (POP3) is used to download emails to a device.

Characteristics of POP3 include:

* Emails are downloaded and stored on a single device.
* Sent messages are stored on the device from which the email was sent.
* Emails are generally accessed from the device to which they were downloaded.
* Emails are typically removed from the server after download.

# IMAP

Internet Message Access Protocol (IMAP) allows emails to remain stored on the server and synchronize across multiple devices.

Characteristics of IMAP include:

* Emails remain stored on the server.
* Emails can be accessed from multiple devices.
* Sent messages are stored on the server.
* Messages are synchronized across devices.
* Emails remain on the server unless explicitly deleted.
* Email Journey

The delivery of an email can be represented as:
```text
Sender
   │
   ▼
Email Client
   │
   │ SMTP
   ▼
Sender Mail Server
   │
   │ DNS Query
   ▼
DNS
   │
   │ Recipient Mail Server
   ▼
Recipient Mail Server
   │
   │ POP3 / IMAP
   ▼
Recipient Email Client
```
The process can be summarized as:

The sender sends an email.
The sender's email client sends the message to the mail server using SMTP.
The sending mail server queries DNS for the recipient's mail server.
DNS provides the address of the recipient's mail server.
The email is delivered to the recipient's mail server.
The recipient's email client connects to the mail server.
The message is retrieved using POP3 or synchronized using IMAP.

Understanding this process helps an analyst understand where information about the email's origin and delivery can be found.

## Email Structure

An email consists of two main parts:
```text
Email
├── Header
└── Body
```
# Email Header

The header contains metadata about the email, including information about:

* Sender
* Recipient
* Email servers
* Delivery
* Date and time
* Subject

# Email Body

The body contains the actual message.

It can be formatted as:

* Plain text
* HTML

HTML emails can contain:

* Images
* Links
* Styling
* Embedded content

## Email Headers

Important email header fields include:

# From

The sender's email address.

# To

The recipient's email address.

# Reply-To

The address where replies will be sent.

This field is not required and can sometimes provide useful information during phishing analysis.

# Subject

The subject line of the email.

# Date

The date and time the email was sent.

## Viewing the Message Source

The standard email interface does not always display all of the technical information contained within an email.

Viewing the raw message source allows an analyst to inspect:

* Full email headers.
* Email body source.
* Technical information.
* Originating IP addresses.
* Embedded content.

In Thunderbird, the message source can be accessed through:
```text
View → Message Source
```
The keyboard shortcut is:
```text
Ctrl + U
```
Viewing the raw source provides additional information that may not be visible in the normal email interface.

## Email Body Analysis

The email body contains the actual message presented to the recipient.

Emails can be sent as:

* Plain text
* HTML

HTML allows emails to contain:

* Images
* Hyperlinks
* Styling
* Other embedded elements

When analyzing a suspicious email, it is useful to inspect the underlying HTML source rather than relying only on the rendered message.

## HTML Source Analysis

Viewing the HTML source allows the analyst to understand how the email is structured behind the scenes.

The source may reveal:

* Links.
* Images.
* Embedded elements.
* HTML structure.
* Content that may not be visible in the rendered email.

Some email clients may block images by default.

Therefore, inspecting the source can reveal information that is not immediately visible to the recipient.

## Email Attachments

Emails can contain attachments such as:

* Documents
* Images
* PDFs
* Other file types

Attachments can also be analyzed by inspecting the raw email source.

Important headers associated with an attachment include:

# Content-Type

Indicates the type of file.

Example:
```text
application/pdf
```

# Content-Disposition

Specifies that the content is an attachment and can include the filename.

# Content-Transfer-Encoding

Specifies how the attachment is encoded.

One example is:
```text
base64
```
The Base64 data that follows represents the encoded file.

It can be decoded to reconstruct the original attachment using tools such as:

* CyberChef
* Base64 decoding tools

## Types of Phishing

Email remains one of the most common entry points for cyber attacks.

Attackers often use social engineering to convince users to perform an action.

Common types of malicious email include:

# Spam

Unsolicited bulk emails sent to a large number of recipients.

A more malicious form of spam is commonly referred to as malspam.

# Phishing

Phishing emails impersonate trusted entities to trick recipients into revealing sensitive information.

The attack may attempt to:

* Steal credentials.
* Obtain sensitive information.
* Deliver malware.
* Gain unauthorized access.

# Spear Phishing

Spear phishing is a targeted form of phishing aimed at a specific individual or organization.

Attackers often use personalized information to make the message appear legitimate.

# Whaling

Whaling is a form of spear phishing that specifically targets high-level executives.

Examples of targets include:

* CEO
* CFO
* Other senior executives

The objective may include obtaining sensitive information or financial access.

# Smishing

Smishing is phishing conducted through SMS or text messages.

The attack targets users through their mobile devices.

# Vishing

Vishing is phishing conducted through voice calls.

Attackers use social engineering techniques over the phone to manipulate victims.

## Anatomy of a Phishing Email

Phishing emails often contain recognizable characteristics.

Spoofed From Address

The sender address may be manipulated to appear as though it belongs to a trusted organization.

Example:
```text
noreply@microsof.com
```
The domain appears similar to a legitimate organization but contains a subtle difference.

## Urgent Subject or Message

Attackers may create a sense of urgency to pressure the victim into acting quickly.

Example:
```text
Your account will be locked in 24 hours
```
The goal is to discourage the recipient from carefully evaluating the message.

## Brand Impersonation

The email may imitate a legitimate organization through:

* Logos
* Colors
* Branding
* Visual design

This can make the email appear trustworthy.

## Grammar and Spelling Issues

Phishing emails may contain:

* Grammar mistakes.
* Spelling errors.
* Awkward wording.
* Unnatural language.

However, these indicators are becoming less reliable as attackers can use AI to generate more natural-looking messages.

## Generic Content

The email may use generic greetings rather than personal information.

Example:
```text
Dear Customer
```
instead of addressing the recipient by name.

#Hidden or Shortened Links

Hyperlinks may disguise their true destination.

Example:
```text
bit.ly/secure-login
```
The visible link may not reveal where the user will actually be redirected.

## Malicious Attachments

Attackers may disguise malicious files as legitimate documents.

Example:
```text
invoice.pdf.exe
```
The filename attempts to make the file appear to be a PDF while actually using an executable extension.

## Safe Analysis

When analyzing suspicious emails, hyperlinks and attachments must be handled carefully.

An analyst should avoid accidentally clicking suspicious links or opening potentially malicious files.

One technique used during analysis is defanging.

# Defanging

Defanging makes URLs, domains, and email addresses unclickable.

It works by replacing special characters with alternative characters.

Example:
```text
Original:
http://www.suspiciousdomain.com


Defanged:
hxxp[://]www[.]suspiciousdomain[.]com
```
This reduces the risk of accidentally accessing a malicious resource during investigation.

## Phishing Analysis Workflow

A basic phishing analysis process can be represented as:
```text
Suspicious Email
       │
       ▼
Analyze Email Address
       │
       ▼
Analyze Headers
       │
       ▼
Inspect Raw Message
       │
       ▼
Analyze Email Body
       │
       ▼
Inspect Links
       │
       ▼
Inspect Attachments
       │
       ▼
Identify Phishing Indicators
       │
       ▼
Determine Malicious / Benign
```
The analyst should gather information from multiple parts of the email rather than relying on a single indicator.

## Business Email Compromise

The room also introduces Business Email Compromise (BEC).

BEC is an attack in which an adversary gains access to a legitimate internal email account and uses it to trick others into performing unauthorized or fraudulent actions.

This demonstrates why simply trusting the sender's email address is not always sufficient.

An account may be legitimate while the activity performed through it is malicious.

## SOC Analyst Perspective

Phishing analysis is an important SOC activity because phishing can provide attackers with an initial foothold in an organization's network.

A SOC analyst may need to determine whether an email is:

* Benign.
* Spam.
* Phishing.
* Malicious.

The analyst can investigate:

* Email addresses.
* Headers.
* Originating IP addresses.
* Message source.
* HTML content.
* Links.
* Attachments.
* Social engineering indicators.

The information gathered during analysis can also help improve future security measures.

## Skills Acquired

This room strengthened my understanding of:

* Email architecture.
* Email addresses.
* SMTP.
* POP3.
* IMAP.
* Email delivery.
* DNS in email delivery.
* Email headers.
* Raw message source.
* HTML email analysis.
* Email attachment analysis.
* Base64 encoding.
* Phishing.
* Spear phishing.
* Whaling.
* Smishing.
* Vishing.
* Spam and malspam.
* Phishing indicators.
* Defanging.
* Safe email analysis.
* Business Email Compromise (BEC).

## Analyst Notes
# Key Takeaways
* Email is one of the most common entry points for cyber attacks.
* Understanding email delivery helps analysts understand how a message travels from sender to recipient.
* SMTP is used to send emails.
* POP3 downloads emails to a device.
* IMAP synchronizes emails across devices.
* Email headers contain important metadata about a message.
* Viewing the raw message source can reveal technical information not visible in the normal inbox.
* Email bodies can contain HTML, links, images, and other embedded elements.
* Attachments can be analyzed through their associated headers and encoded data.
* Phishing can involve spoofed addresses, urgency, brand impersonation, suspicious links, and malicious attachments.
* Spear phishing targets specific individuals or organizations.
* Whaling targets high-level executives.
* Smishing uses SMS messages.
* Vishing uses voice calls.
* Defanging helps prevent accidental interaction with malicious indicators.
* BEC can involve compromised legitimate internal email accounts.
* Phishing analysis requires examining multiple components of an email rather than relying on a single indicator.

## New Terminology

* POP3
* SMTP
* IMAP
* Email Header
* Email Body
* Message Source
* HTML
* Base64
* Spam
* Malspam
* Phishing
* Spear Phishing
* Whaling
* Smishing
* Vishing
* Defanging
* Business Email Compromise (BEC)
* Content-Type
* Content-Disposition
* Content-Transfer-Encoding

## Personal Reflection

This room helped me understand that phishing analysis is more than simply looking at whether an email appears suspicious.

An analyst needs to understand how email works and investigate multiple components of the message, including the email address, headers, raw source, body, links, and attachments.

I also learned that attackers can use techniques such as spoofing, urgency, brand impersonation, malicious attachments, and disguised links to make phishing emails appear legitimate.

The concept of safe analysis was particularly important because investigating malicious emails must be done carefully to avoid accidentally interacting with dangerous links or files.

Overall, this room provided the fundamental technical knowledge needed to begin analyzing phishing emails from a SOC analyst perspective.

## References
* TryHackMe — SOC Level 1
* Phishing Analysis Fundamentals

