# Study Guide - Humans as Attack Vectors

> Module 01 - Blue Team Introduction

---

# 1. Learning Summary

This room focuses on the **human element in cybersecurity** and explains why humans are often considered the weakest link and an important attack vector.

Threat actors may target people because compromising a human account can provide access to:

* Websites
* Mailboxes
* Databases
* VPN accounts
* Corporate networks
* Sensitive information

The room introduces **social engineering**, several common attacks against humans, and the role of a SOC analyst in detecting, investigating, and helping prevent these attacks.

### Main objectives

* Understand the role of the human element in cybersecurity.
* Understand how attackers target humans.
* Understand the SOC role in detecting and mitigating attacks.
* Practice responding to attacks against employees.

---

# 2. Key Concepts

## Humans as an Attack Vector

Attackers may choose to target humans instead of directly exploiting technical defenses.

The reason is simple:

> Humans can provide access that would otherwise be difficult to obtain.

Examples include compromising:

* An HR manager's Google account.
* A wealthy person's computer.
* An IT administrator's VPN account.
* A government worker's account or information.

The attacker's objective depends on the access obtained.

---

# 3. Why Are Humans Targeted?

Attackers target humans because of the access they can provide.

For example:

| Target                    | Possible Attacker Objective                   |
| ------------------------- | --------------------------------------------- |
| HR manager's account      | Steal the employee database                   |
| Wealthy person's computer | Hijack a web banking session                  |
| IT administrator's VPN    | Access the corporate network                  |
| Government worker         | Obtain information to simplify future attacks |

An attacker may also breach many accounts without initially knowing exactly how they will use them.

---

# 4. Social Engineering

Social engineering is the manipulation of a victim into helping the attacker, knowingly or unknowingly.

Unlike attacks that primarily exploit technical vulnerabilities, social engineering exploits **human psychology**.

For social engineering to be successful, attacks are often designed to appear:

### Trustworthy

The attacker must appear legitimate so that the victim trusts them.

### Emotional

The attack may trigger emotions such as:

* Urgency
* Fear
* Curiosity

---

# 5. Common Attacks Against Humans

## Phishing

Phishing is a form of social engineering in which an attacker uses fraudulent communication to trick a victim.

Example:

An employee receives an email claiming:

> "Your account has been compromised. Click here for details!"

The link leads to a fake login page that looks legitimate but sends the victim's credentials to the attacker.

### Key idea

```text
Phishing email
      ↓
Victim clicks link
      ↓
Fake login page
      ↓
Victim enters credentials
      ↓
Attacker obtains credentials
```

Email phishing is presented in the room as the most common form of social engineering.

---

## Malware Downloads

Attackers may trick users into downloading and installing malicious software.

The room highlights several techniques used to make these attacks more successful:

* Fake CAPTCHAs
* Malicious QR codes
* SEO poisoning

### Key idea

The victim believes they are downloading or interacting with something legitimate, but the attacker uses the action to deliver malware.

---

## Deepfakes

Deepfakes involve AI-generated or manipulated video or audio used to impersonate another person.

Attackers can use deepfakes to impersonate:

* Family members
* Colleagues
* Corporate partners
* Executives

### Example from the room

A finance worker received a deepfake video call from someone appearing to be their boss and was tricked into wiring **$25 million** for an urgent business deal.

### Key lesson

Even video or audio that appears convincing should not automatically be trusted when a request is unusual or sensitive.

---

## Impersonation

Attackers can pretend to be someone else without necessarily using deepfake technology.

For example, attackers may impersonate a company's IT department and call employees requesting that they take over their accounts for a supposed system repair.

### Key idea

The attacker abuses the victim's trust in a legitimate person or department.

---

# 6. Other Attacks

The room also identifies several other human-focused attack methods:

* USB drop campaigns
* Physical attacks
* Insider threats
* Fake job offers

These are all presented as ongoing risks to employees.

As a SOC analyst, you should be prepared to respond to these types of attacks.

---

# 7. Defending Humans

The room identifies two key defensive tasks:

## Mitigation

Mitigation aims to **prevent attacks or reduce their probability and impact**.

Examples include:

* Training employees.
* Deploying anti-phishing solutions.
* Using antivirus / EDR.
* Applying the "Trust but verify" principle.
* Security awareness training.

## Detection

Even strong mitigation measures can eventually be bypassed.

This is where the SOC becomes important.

The SOC must be able to:

* Detect attacks.
* Investigate suspicious activity.
* Respond when defensive measures are bypassed.

### Key relationship

```text
Mitigation
    ↓
Reduce / prevent attacks
    ↓
Attack bypasses mitigation
    ↓
SOC detects activity
    ↓
Investigation
    ↓
Response
```

---

# 8. Mitigation Measures

## Anti-Phishing Solution

A security solution can block phishing emails before users interact with them.

### Objective

Reduce the number of phishing emails reaching employees.

---

## Antivirus / EDR

Antivirus and EDR solutions on corporate hosts can help prevent users from successfully running malware.

### Objective

Reduce the impact of malicious downloads.

---

## "Trust but Verify"

Employees should be taught to recognize deepfakes and verify suspicious requests that appear to come from people such as:

* CEOs
* IT personnel

### Objective

Prevent employees from blindly trusting unusual requests.

---

## Security Awareness Training

Employees should be trained to identify phishing and other security threats.

The room also mentions **phishing simulations** as a way to reinforce this training.

---

# 9. SOC Analyst Perspective

The role of the SOC can vary between organizations.

Some analysts may primarily monitor alerts.

Others may have a much broader role and:

* Maintain close relationships with IT or HR.
* Propose security improvements.
* Run company-wide security training.
* Answer hotline calls from employees who suspect an attack.

### Important idea

A SOC analyst is not limited to looking at alerts.

Depending on the organization, the analyst may also participate in security improvement, employee awareness, and communication with other teams.

---

# 10. Active Recall

**Do not look at the answers or README while answering these.**

## Basic

1. Why are humans considered an important attack vector?

2. What type of access might attackers obtain by compromising a human?

3. What is social engineering?

4. What two characteristics can make social engineering attacks successful?

5. What is phishing?

6. What is impersonation?

7. What is a deepfake?

8. What is mitigation?

9. What is detection?

---

## Intermediate

10. Why might an attacker target an IT administrator's VPN account?

11. How does phishing exploit human psychology?

12. How can malware downloads be disguised as legitimate activity?

13. Why can deepfakes make social engineering more convincing?

14. What is the difference between impersonation and deepfake-based impersonation?

15. Why is security awareness training important?

16. Why are phishing simulations useful?

17. Why can't an organization rely exclusively on mitigation?

---

## SOC Analyst Challenge

18. An employee reports a suspicious email. What should a SOC analyst be interested in investigating?

19. An employee says someone claiming to be IT asked them to "take over" their account for a system repair. What type of attack could this represent?

20. An employee reports an unusual request supposedly coming from the CEO. What defensive principle from this room could apply?

21. Why might the SOC need to work with HR or IT when dealing with attacks against humans?

---

# 11. Flashcards

| Question                                          | Answer                                                                           |
| ------------------------------------------------- | -------------------------------------------------------------------------------- |
| Why are humans targeted?                          | Because they can provide access to systems, accounts, information, and networks. |
| What is social engineering?                       | Manipulating a victim into helping an attacker, knowingly or unknowingly.        |
| What does social engineering exploit?             | Human psychology.                                                                |
| What emotions can social engineering exploit?     | Urgency, fear, and curiosity.                                                    |
| What is phishing?                                 | A social engineering attack using fraudulent communication to deceive a victim.  |
| What is impersonation?                            | Pretending to be another person or organization.                                 |
| What is a deepfake?                               | AI-generated or manipulated video/audio used to impersonate someone.             |
| What are examples of other human-focused attacks? | USB drops, physical attacks, insider threats, and fake job offers.               |
| What is mitigation?                               | Preventing or reducing the likelihood and impact of attacks.                     |
| What is detection?                                | Identifying attacks that occur despite defensive measures.                       |
| What does security awareness training do?         | Teaches employees how to recognize threats such as phishing.                     |
| What can phishing simulations be used for?        | Reinforcing security awareness training.                                         |

---

# 12. Real-World Scenarios

## Scenario 1 - Phishing

An employee receives an email stating that their corporate account has been compromised. The email contains a link to "verify" their account.

### Questions

* What type of attack could this be?
* What psychological technique might the attacker be using?
* What would you investigate as a SOC analyst?
* What could have prevented the user from receiving the email?

---

## Scenario 2 - IT Impersonation

An employee receives a phone call from someone claiming to be from the company's IT department.

The caller asks the employee to take over their account for a "quick system repair."

### Questions

* What type of attack could this represent?
* Why might the victim trust the attacker?
* What security principle could help prevent this?
* What role could the SOC play?

---

## Scenario 3 - Deepfake

An employee receives a video call appearing to be from a company executive requesting an urgent financial transaction.

### Questions

* What technology could be involved?
* Why should the employee verify the request?
* Which mitigation measure from this room applies?
* Why might urgency make the attack more effective?

---

## Scenario 4 - Malware Download

A user visits a website and encounters a fake CAPTCHA. After following the instructions, malware is downloaded onto the computer.

### Questions

* How was the human element exploited?
* What technique mentioned in the room was used?
* Which security technology could help?
* What would the SOC need to investigate?

---

# 13. Interview Questions

1. Why are humans considered the weakest link in cybersecurity?

2. What is social engineering?

3. What makes a social engineering attack trustworthy and emotional?

4. Explain how a phishing attack works.

5. What is the difference between phishing and impersonation?

6. What are deepfakes and how can attackers use them?

7. What other attacks can target humans?

8. What is the difference between mitigation and detection?

9. How can an anti-phishing solution protect employees?

10. How can antivirus or EDR help prevent malware attacks against users?

11. What does "Trust but verify" mean in a cybersecurity context?

12. Why is security awareness training important?

13. How can phishing simulations improve security awareness?

14. What role can a SOC play in defending employees?

15. Why might a SOC collaborate with IT or HR?

---

# 14. Common Mistakes

❌ Thinking attackers always need to exploit a technical vulnerability.

❌ Assuming that a legitimate-looking email is automatically trustworthy.

❌ Trusting a request simply because it appears to come from a manager or IT department.

❌ Assuming deepfakes are only a media or entertainment problem.

❌ Believing mitigation can prevent every attack.

❌ Thinking the SOC's only responsibility is monitoring alerts.

---

# 15. Must Know

Before moving on, these concepts should be understood without looking at your notes:

* [ ] Humans can be an attack vector.
* [ ] Attackers target humans because of the access they can provide.
* [ ] Social engineering exploits human psychology.
* [ ] Trust and emotion are important elements of social engineering.
* [ ] Phishing is a major form of social engineering.
* [ ] Malware can be delivered through seemingly legitimate downloads.
* [ ] Deepfakes can be used for impersonation.
* [ ] Attackers can impersonate trusted people or departments.
* [ ] Mitigation reduces the likelihood or impact of attacks.
* [ ] Detection allows the SOC to identify attacks that bypass mitigation.
* [ ] Security awareness is an important defensive measure.

---

# 16. Self Assessment

I can confidently explain:

* [ ] Why humans are targeted by threat actors.
* [ ] What social engineering is.
* [ ] How phishing works.
* [ ] How malware downloads can target users.
* [ ] What deepfakes are.
* [ ] How impersonation attacks work.
* [ ] Other attacks such as USB drops, insider threats, and fake job offers.
* [ ] The difference between mitigation and detection.
* [ ] The main mitigation measures described in the room.
* [ ] The SOC's role in defending humans.
* [ ] Why the SOC may collaborate with IT and HR.

---

# 17. Quick Review

Before considering this room complete, answer these from memory:

1. Why do attackers target humans?

2. What is social engineering?

3. What makes a social engineering attack effective?

4. How does phishing work?

5. How can malware downloads exploit humans?

6. What are deepfakes?

7. What is impersonation?

8. What other attacks against humans were covered?

9. What is mitigation?

10. What is detection?

11. What tools or practices can help protect employees?

12. What role does a SOC analyst play?

---

# 18. Connections

This room builds on the previous **Junior Security Analyst Intro** room by introducing one of the major areas a SOC analyst must defend: the human element.

It also prepares the next topic:

➡️ **Systems as Attack Vectors**

An attacker may exploit a human to obtain access and then use that access to compromise organizational systems. Understanding both attack vectors is therefore essential for a SOC analyst.
