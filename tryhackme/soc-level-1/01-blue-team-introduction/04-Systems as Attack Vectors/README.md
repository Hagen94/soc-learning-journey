# Systems as Attack Vectors

## Overview

This room explains how attackers target systems instead of people by exploiting vulnerabilities, misconfigurations, and software supply chains.

It also introduces the role of the SOC in detecting attacks against critical infrastructure and supporting mitigation efforts.

---

## Learning Objectives

After completing this room, I am able to:

- Understand why systems are valuable attack targets.
- Identify common attacks against systems.
- Explain software vulnerabilities and CVEs.
- Understand the risks of system misconfigurations.
- Recognize mitigation strategies used to protect systems.

---

## Key Concepts

### Systems as Attack Targets

Systems such as servers, cloud platforms, databases, and workstations store valuable information and provide critical business services, making them attractive targets for attackers.

---

### Common System Attacks

#### Human-Led Attacks

Systems are often compromised through user actions such as weak passwords, malicious USB devices, or malware execution.

#### Software Vulnerabilities

Security flaws in software may allow attackers to gain unauthorized access or execute malicious code.

Public vulnerabilities are assigned a Common Vulnerabilities and Exposures (CVE) identifier.

#### Supply Chain Attacks

Attackers compromise trusted software vendors or third-party libraries to distribute malicious updates to legitimate users.

---

### Vulnerability Management

Protecting systems requires:

- Patch management
- Monitoring zero-day vulnerabilities
- Applying temporary mitigations
- Restricting unnecessary access

---

### Misconfigurations

Many incidents are caused by insecure configurations rather than software bugs.

Examples include:

- Weak passwords
- Publicly exposed services
- Excessive permissions
- Insecure cloud configurations

---

## SOC Perspective

SOC analysts monitor systems for indicators of compromise and collaborate with IT teams to improve security posture.

Although system administration is not their primary responsibility, understanding common weaknesses allows analysts to identify attacks more effectively.

---

## Mitigation Strategies

Examples include:

- Patch management
- Network segmentation
- Antivirus / EDR
- Vulnerability scanning
- Configuration audits
- Security training for IT teams

---

## Skills Acquired

This room strengthened my understanding of:

- Vulnerability management
- CVE lifecycle
- Zero-day attacks
- Supply chain attacks
- Secure system configuration
- System hardening

---

## Analyst Notes

### Key Takeaways

- Systems contain valuable assets that attract attackers.
- Vulnerabilities and misconfigurations are major attack vectors.
- Timely patching significantly reduces organizational risk.
- Supply chain attacks can compromise thousands of organizations simultaneously.

### New Terminology

- CVE
- Zero-day
- Patch Management
- Supply Chain Attack
- Misconfiguration
- Vulnerability Scan
- Hardening

---

## Personal Reflection

This room highlighted that protecting systems requires more than deploying security software. Proper configuration, timely patching, continuous monitoring, and collaboration between SOC analysts and IT teams are essential to reducing organizational risk.

---

## References

- TryHackMe – SOC Level 1