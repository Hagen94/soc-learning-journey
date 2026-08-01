# Study Guide - Systems as Attack Vectors

> Module 01 - Blue Team Introduction

---

# 1. Learning Summary

This room focuses on **systems as attack vectors** and explains why threat actors target systems directly.

A system can be a physical server, a lab machine, or a cloud platform such as Microsoft 365. Compromising a system can provide attackers with significantly more access than compromising a single user.

The room covers:

* Systems as attack targets
* Human-led attacks against systems
* Software vulnerabilities
* Supply chain attacks
* Zero-days and CVEs
* Misconfigurations
* Mitigation and detection
* The SOC analyst's role in protecting systems

**Goal:** Understand how systems can be attacked, why they are valuable to threat actors, and how a SOC analyst can help protect them.

---

# 2. Key Concepts

## Systems as Attack Vectors

Threat actors can attack insecure systems directly without the user's knowledge.

Examples of systems include:

* Physical servers
* Lab machines
* Cloud platforms
* Mail servers
* Network servers
* Website management panels

The value of a compromised system depends on what access or resources it provides.

---

## Why Systems Are Valuable

Compromising a single user may provide access to one mailbox.

Compromising a mail server could provide access to **thousands of mailboxes**.

Examples from the room:

| System                              | Possible Attacker Objective                      |
| ----------------------------------- | ------------------------------------------------ |
| Student's personal laptop           | Steal a Steam profile and add the PC to a botnet |
| Bank IT administrator's laptop      | Access internal banking systems                  |
| Criminal law company's mail server  | Dump mailboxes and blackmail the victim          |
| Industrial network server           | Encrypt the network with ransomware              |
| Government website management panel | Damage website content                           |

**Key idea:** The value of a system depends on the access and resources available through it.

---

# 3. Attacks on Systems

The room introduces three major ways systems can be attacked:

1. Human-led attacks
2. Vulnerabilities
3. Supply chain attacks

---

## Human-Led Attacks

Users can unintentionally initiate attacks against systems.

Examples include:

* Inserting a malicious USB device.
* Downloading malware from pirated resources.
* Reusing weak passwords.

The room states that **81% of breaches involve stolen or breached passwords**.

### Key idea

A system can be technically vulnerable because of how users interact with it.

---

# 4. Software Vulnerabilities

Every piece of software can contain security flaws.

A vulnerability may remain undiscovered for years.

### Example

The room uses **Shellshock** as an example of a major Linux vulnerability that existed since 1992 but was not discovered until 2014.

---

## Zero-Day

A **zero-day** is a vulnerability discovered by attackers before defenders have had an opportunity to address it.

This creates a difficult situation for defenders because there may not yet be an available patch.

### Key idea

```text
Vulnerability discovered by attacker
            ↓
No patch available
            ↓
Potential exploitation
            ↓
SOC monitors for exploitation
```

---

## CVE

Once a vulnerability becomes public, it is assigned a **Common Vulnerabilities and Exposures (CVE)** number.

After disclosure, attackers may develop exploits while defenders work to update affected systems.

---

# 5. Responding to Vulnerabilities

The normal answer to a CVE is a **patch** supplied by the software vendor.

For zero-days, defenders may need to wait for a patch while monitoring for exploitation.

The room gives several temporary defensive measures:

### Restrict Access

Restrict access to the affected system to trusted IP addresses.

### Vendor Temporary Measures

Apply temporary measures provided by the vendor.

### Block Attack Patterns

Block known attack patterns using:

* IPS
* WAF

### Key Idea

When a permanent patch is unavailable, temporary defensive controls can reduce exposure.

---

# 6. Supply Chain Attacks

A **supply chain attack** occurs when attackers compromise software or a library used by other organizations and distribute the compromise through an update.

Modern systems depend on many applications and libraries.

If an attacker compromises one of these components and pushes a malicious update, many users can become compromised.

### Examples from the room

* SolarWinds
* 3CX

Both affected thousands of companies.

---

## Why Supply Chain Attacks Are Difficult

Organizations cannot always control every piece of software installed on:

* Laptops
* Servers
* Web applications

This makes supply chain attacks particularly difficult to defend against.

The room also notes that TryHackMe experienced a supply chain incident involving **Lottie Player**, a library used for room animations.

---

# 7. Misconfigurations

A **misconfiguration is not a software bug**.

It is a mistake in how a system was configured.

These mistakes often happen because administrators want to make systems easier to manage.

### Examples from the room

* Weak passwords such as `1111`
* Exposed systems
* Misconfigured cloud environments
* Insecure database configurations
* Smart fridges used in botnet attacks

---

## Vulnerability vs Misconfiguration

This distinction is important.

| Vulnerability                   | Misconfiguration                       |
| ------------------------------- | -------------------------------------- |
| Security flaw in software       | Incorrect system setup                 |
| Usually requires a software fix | Requires correcting the configuration  |
| Vendor patch may be required    | Better configuration may be sufficient |

### Remember

> Vulnerability = flaw in the software.

> Misconfiguration = mistake in how the system was configured.

---

# 8. Responding to Misconfigurations

Unlike vulnerabilities, misconfigurations do not require a software update.

They require the system to be configured correctly.

The room identifies three approaches:

## Penetration Testing

Ethical hackers simulate attacks and report discovered security flaws.

---

## Vulnerability Scans

Tools can periodically identify problems such as:

* Default passwords
* Outdated software

---

## Configuration Audits

Systems are manually reviewed against security best practices such as **CIS benchmarks**.

---

# 9. Mitigation and Detection

Attackers may choose whichever path is easiest.

They don't necessarily distinguish between attacking humans and attacking systems.

Therefore organizations should protect both.

The room emphasizes combining:

**Mitigation + Detection**

---

# 10. System Mitigation Measures

## Patch Management

A process of tracking and patching vulnerable systems.

**Purpose:** Reduce the chance of a successful attack.

---

## Training for IT

IT personnel should understand the risks associated with misconfigurations.

**Purpose:** Reduce configuration mistakes.

---

## Network Protection

Restrict access to systems to trusted people or IP addresses.

**Purpose:** Make systems harder to breach.

---

## Antivirus Protection

Antivirus can prevent or detect many attacks.

**Purpose:** Detect or stop malicious activity.

---

# 11. SOC Analyst Perspective

SOC analysts do not typically manage systems directly.

However, they should understand common system attacks and defenses.

The SOC can:

* Detect attacks.
* Investigate suspicious activity.
* Understand common vulnerabilities.
* Identify potential misconfigurations.
* Share security information with IT.
* Recommend security improvements.
* Stay updated on emerging threats.

### Key idea

The SOC and IT department can work together.

```text
SOC
 ↓
Detect / Investigate
 ↓
Share findings
 ↓
IT
 ↓
Remediate / Improve configuration
```

---

# 12. Active Recall

Answer these questions **without looking at the README or this guide**.

## Basic

1. What is a system?

2. Why can systems be valuable targets?

3. What are the three major system attack categories covered in this room?

4. What is a vulnerability?

5. What is a zero-day?

6. What is a CVE?

7. What is a supply chain attack?

8. What is a misconfiguration?

9. What is patch management?

10. What is network protection?

---

## Intermediate

11. Why could compromising a mail server be more valuable than compromising a single mailbox?

12. How can users unintentionally help attackers compromise systems?

13. What is the difference between a vulnerability and a misconfiguration?

14. Why are zero-days difficult to defend against?

15. What happens after a vulnerability becomes public?

16. Why are supply chain attacks difficult to protect against?

17. How can penetration testing help identify security problems?

18. How can configuration audits help protect systems?

---

## SOC Analyst Challenge

19. A critical vulnerability has been discovered but no patch is available. What temporary measures could defenders use?

20. A server is exposed because of an insecure configuration. Is this necessarily a software vulnerability? Explain.

21. An application receives a malicious update from a compromised third-party library. What type of attack could this represent?

22. Why should a SOC analyst understand system vulnerabilities even if they don't directly manage the systems?

23. How should the SOC and IT department work together after identifying a system security problem?

---

# 13. Flashcards

| Front                                    | Back                                                                                                              |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| What is a system?                        | A physical server, lab machine, cloud platform, or other infrastructure storing or providing access to resources. |
| Why are systems valuable targets?        | They can provide access to large amounts of data, users, networks, or critical resources.                         |
| What is a vulnerability?                 | A security flaw in software.                                                                                      |
| What is a zero-day?                      | A vulnerability discovered by attackers before defenders can address it.                                          |
| What is a CVE?                           | A Common Vulnerabilities and Exposures identifier assigned to a publicly known vulnerability.                     |
| What is a supply chain attack?           | An attack where compromised software or libraries distribute malicious content to their users.                    |
| What is a misconfiguration?              | A mistake in how a system was configured.                                                                         |
| What is the normal response to a CVE?    | Apply a patch supplied by the software vendor.                                                                    |
| What can defenders do during a zero-day? | Monitor for exploitation and apply temporary defensive measures.                                                  |
| What is penetration testing?             | Simulating attacks to identify security weaknesses.                                                               |
| What is a vulnerability scan?            | A scan that can identify problems such as default passwords or outdated software.                                 |
| What is a configuration audit?           | Reviewing system configurations against security best practices.                                                  |
| What is patch management?                | Tracking and patching vulnerable systems.                                                                         |
| What is network protection?              | Restricting system access to trusted people or IP addresses.                                                      |

---

# 14. Real-World Scenarios

## Scenario 1 - Unpatched Vulnerability

A critical vulnerability is discovered in a server used by your organization.

The vendor has not released a patch yet.

### Questions

* What type of vulnerability situation is this?
* What temporary measures could be applied?
* What should the SOC monitor for?
* Which teams should be involved?

---

## Scenario 2 - Misconfiguration

A database is accidentally configured with insecure access permissions.

### Questions

* Is this necessarily a software vulnerability?
* What type of security problem is this?
* How could it be identified?
* What remediation could be performed?

---

## Scenario 3 - Supply Chain

A company receives a software update from a trusted vendor. The update contains malicious code because the vendor's software supply chain was compromised.

### Questions

* What type of attack is this?
* Why is this attack difficult to prevent?
* What should the SOC investigate?
* What could organizations do to reduce the impact?

---

## Scenario 4 - System vs Human

An attacker can either:

* Trick an employee into opening a malicious file.
* Exploit an exposed vulnerable server.

### Questions

* Which attack vector should the attacker choose?
* Why might an attacker choose one over the other?
* Why should defenders protect both humans and systems?

---

# 15. Interview Questions

1. What is considered a system in cybersecurity?

2. Why are systems attractive targets for threat actors?

3. What are common ways attackers target systems?

4. What is a software vulnerability?

5. What is a zero-day vulnerability?

6. What is a CVE?

7. How should an organization respond to a known vulnerability?

8. What can defenders do when a zero-day has no patch?

9. What is a supply chain attack?

10. Why are supply chain attacks difficult to defend against?

11. What is a misconfiguration?

12. What is the difference between a vulnerability and a misconfiguration?

13. How can organizations detect misconfigurations?

14. What is patch management?

15. How can network protection reduce risk?

16. What role does the SOC have in protecting systems?

17. Why should the SOC communicate with the IT department?

---

# 16. Common Mistakes

❌ Confusing a vulnerability with a misconfiguration.

❌ Assuming every security problem requires a software patch.

❌ Thinking a zero-day can immediately be solved with a normal patch.

❌ Assuming supply chain attacks only affect one organization.

❌ Thinking the SOC directly manages every system.

❌ Focusing only on system protection while ignoring human attack vectors.

❌ Assuming mitigation alone is enough without detection.

---

# 17. Must Know

Before moving to the next module, I should be able to explain without notes:

* [ ] Why systems are valuable attack targets.
* [ ] The main ways systems can be attacked.
* [ ] Human-led attacks.
* [ ] Software vulnerabilities.
* [ ] Zero-days.
* [ ] CVEs.
* [ ] Supply chain attacks.
* [ ] Misconfigurations.
* [ ] The difference between vulnerabilities and misconfigurations.
* [ ] Patch management.
* [ ] Network protection.
* [ ] Antivirus protection.
* [ ] The SOC's role in protecting systems.
* [ ] The importance of collaboration between SOC and IT.

---

# 18. Self Assessment

I can confidently explain:

* [ ] What a system is.
* [ ] Why attackers target systems.
* [ ] How users can unintentionally help attackers.
* [ ] What vulnerabilities are.
* [ ] What zero-days are.
* [ ] What CVEs represent.
* [ ] How supply chain attacks work.
* [ ] What misconfigurations are.
* [ ] How to respond to vulnerabilities.
* [ ] How to respond to misconfigurations.
* [ ] The main system mitigation measures.
* [ ] How detection and mitigation work together.
* [ ] The SOC's role in system security.

---

# 19. Quick Review

Before considering this room complete, answer these from memory:

1. What is a system?

2. Why can compromising a system be more valuable than compromising a single user?

3. What are the three main attack categories discussed?

4. What is a vulnerability?

5. What is a zero-day?

6. What is a CVE?

7. What is a supply chain attack?

8. What is a misconfiguration?

9. How are vulnerabilities and misconfigurations different?

10. How can organizations respond to vulnerabilities?

11. How can organizations respond to misconfigurations?

12. What are the main mitigation measures?

13. What is the SOC's role?

14. Why should SOC analysts communicate with IT?

---

# 20. Connections

This room builds directly on **Humans as Attack Vectors**.

The previous room focused on how attackers can compromise people. This room shows how attackers can instead target the systems themselves.

The key lesson from both rooms is:

> Attackers will look for the easiest path.

Therefore, an organization must protect **both humans and systems**, combining mitigation with detection.
