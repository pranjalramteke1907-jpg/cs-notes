# Security Concepts Notes

Notes from ISC2 CC training, CISA Learning, and cybersecurity fundamentals study.

---

## The CIA Triad

The CIA triad is the foundation of everything in cybersecurity. Every security decision maps back to one of these three principles.

### Confidentiality
Ensures that only authorised people can access data.

- Data should be hidden from anyone who is not supposed to see it
- Broken when: a hacker steals login credentials, an employee leaks company data, unencrypted data is intercepted on a network

Examples of how confidentiality is protected:
- Passwords and multi-factor authentication
- Encryption — scrambling data so only the right person can read it
- Access controls — only giving people access to what they need for their job
- VPNs — hiding network traffic from outsiders

Real attack example: A phishing email tricks an employee into giving their password. The attacker now reads private emails. Confidentiality is broken.

---

### Integrity
Ensures that data has not been tampered with or modified without authorisation.

- Data should be accurate and trustworthy
- Broken when: a hacker modifies a file during transfer, a database record is changed without permission, malware corrupts system files

Examples of how integrity is protected:
- Hashing — a mathematical fingerprint of a file. If the file changes, the hash changes
- Digital signatures — proves a file came from a specific person and was not modified
- Checksums — used to verify file downloads are complete and unmodified
- Version control and audit logs — track every change made to data

Real attack example: An attacker intercepts a bank transfer and changes the destination account number. The amount looks correct but the money goes somewhere else. Integrity is broken.

---

### Availability
Ensures that systems and data are accessible when authorised users need them.

- Systems should be up and running when needed
- Broken when: a website goes down due to an attack, a server crashes, ransomware encrypts all files making them inaccessible

Examples of how availability is protected:
- Backups — copies of data stored separately so it can be recovered
- Redundancy — having backup servers that take over if the main one fails
- DDoS protection — filtering out fake traffic that tries to overwhelm a server
- Disaster recovery plans — documented steps to restore systems after an incident

Real attack example: A DDoS attack floods a hospital website with millions of fake requests until it crashes. Patients cannot access their records. Availability is broken.

---

### CIA Triad Quick Reference

| Principle | Question it answers | Broken by |
|-----------|-------------------|-----------|
| Confidentiality | Can only the right people see this? | Data theft, eavesdropping, weak passwords |
| Integrity | Has the data been tampered with? | Man-in-the-middle attacks, malware, unauthorised edits |
| Availability | Can people access it when they need to? | DDoS attacks, ransomware, hardware failure |

---

## Common Attack Types

### Phishing
Fake emails, messages, or websites that trick users into giving away credentials or clicking malicious links.

- Spear phishing — targeted at a specific person using personal information
- Whaling — targeted at high-value targets like CEOs or managers
- Vishing — voice phishing done over phone calls
- Smishing — phishing done via SMS text messages

How to spot it: Urgent language, generic greetings, suspicious sender address, links that look slightly wrong (go0gle.com instead of google.com), requests for passwords or payment.

---

### Malware
Malicious software designed to harm, steal from, or take control of a system.

| Type | What it does |
|------|-------------|
| Virus | Attaches itself to files and spreads when files are shared |
| Worm | Spreads automatically across networks without needing a host file |
| Trojan | Disguises itself as legitimate software |
| Ransomware | Encrypts your files and demands payment to unlock them |
| Spyware | Secretly monitors your activity and sends data to attackers |
| Keylogger | Records every key you press, capturing passwords and messages |
| Rootkit | Hides deep in the OS to give persistent access to an attacker |
| Adware | Displays unwanted ads, often bundled with free software |

---

### Man-in-the-Middle Attack (MitM)
An attacker secretly positions themselves between two communicating parties and intercepts or modifies the data.

Example: You connect to a fake WiFi hotspot at a cafe. The attacker sees all your traffic — your login credentials, messages, and browsing.

How it is prevented: HTTPS encryption, VPNs, certificate verification, avoiding public WiFi for sensitive tasks.

---

### SQL Injection
An attacker inserts SQL code into a form field on a website to manipulate the database behind it.

Example: A login form expects a username and password. An attacker types `' OR 1=1 --` as the username. The database interprets this as a valid query and lets them in without a real password.

Why it matters: SQL injection is one of the OWASP Top 10 most critical web vulnerabilities and is still extremely common in real-world applications.

---

### Cross-Site Scripting (XSS)
An attacker injects malicious JavaScript into a webpage that then runs in other users' browsers.

Example: An attacker posts a comment on a forum containing a script tag. Every user who views that comment has the script run in their browser — it can steal their session cookies and take over their account.

Types:
- Stored XSS — the malicious script is saved in the database and runs for every visitor
- Reflected XSS — the script is embedded in a URL and runs when the victim clicks it
- DOM-based XSS — manipulates the page's own JavaScript

---

### DDoS — Distributed Denial of Service
An attacker uses thousands of compromised machines (a botnet) to flood a target server with traffic until it crashes and becomes unavailable to real users.

Example: A gaming company's servers are flooded with millions of fake requests during a major event. Real players cannot connect. This is an availability attack.

---

### Brute Force Attack
An attacker systematically tries every possible password combination until they find the correct one.

- Simple brute force — tries every possible combination from scratch
- Dictionary attack — tries a list of common passwords and words first
- Credential stuffing — uses real username/password combinations leaked from other breaches

Defended against by: account lockouts after failed attempts, multi-factor authentication, strong long passwords.

---

### Social Engineering
Manipulating people rather than machines to gain access to systems or information.

Common techniques:
- Pretexting — creating a fake scenario to gain trust (pretending to be IT support)
- Baiting — leaving a USB drive in a car park hoping someone plugs it in
- Tailgating — following an authorised person through a secure door without credentials
- Quid pro quo — offering something in exchange for information or access

The most important thing to remember: humans are almost always the weakest link in any security system.

---

## Authentication vs Authorisation

These two words are often confused but mean different things.

| Term | Meaning | Example |
|------|---------|---------|
| Authentication | Proving who you are | Entering your username and password |
| Authorisation | What you are allowed to do after proving who you are | Being allowed to read files but not delete them |

Example: You log into a company system (authentication). You can view your own files but cannot access the HR department's confidential records (authorisation).

---

## Types of Authentication

### Something you know
Password, PIN, security question answer. The weakest form of authentication alone — passwords can be guessed, stolen, or leaked.

### Something you have
A physical device — phone, hardware token, smart card. Harder to steal than a password.

### Something you are
Biometrics — fingerprint, face scan, retina scan. Unique to each person.

### Multi-Factor Authentication (MFA)
Combining two or more of the above. Even if an attacker steals your password, they cannot log in without also having your phone.

Example: Entering a password (something you know) then receiving a code on your phone (something you have).

---

## Access Control Models

### DAC — Discretionary Access Control
The owner of a resource decides who can access it.
Example: You create a Google Doc and choose who can view or edit it.

### MAC — Mandatory Access Control
Access is determined by the system based on security labels — not the owner.
Example: Government and military systems where files are labelled Top Secret, Secret, or Unclassified and users have a clearance level.

### RBAC — Role-Based Access Control
Access is granted based on a user's role in the organisation.
Example: A junior developer can read code but not deploy to production. A senior developer can do both.

### ABAC — Attribute-Based Access Control
Access is based on attributes — user's department, location, time of day.
Example: Employees can only access the system between 9am and 6pm from the office network.

---

## Encryption Basics

Encryption converts readable data (plaintext) into unreadable data (ciphertext) so that only authorised parties can read it.

### Symmetric Encryption
The same key is used to encrypt and decrypt.
- Fast and efficient
- Problem: how do you securely share the key with the other person?
- Example: AES (Advanced Encryption Standard) — used in file encryption and VPNs

### Asymmetric Encryption
Two different keys — a public key and a private key.
- Public key encrypts the data — anyone can have it
- Private key decrypts the data — only the owner has it
- Solves the key-sharing problem of symmetric encryption
- Example: RSA — used in HTTPS, email encryption, digital signatures

### How HTTPS works
When you visit a secure website (https://):
1. Your browser gets the server's public key from its certificate
2. Your browser uses the public key to encrypt a session key
3. Only the server can decrypt it with its private key
4. From then on, your communication is encrypted with the session key

---

## Firewalls and IDS/IPS

### Firewall
A security device that monitors and filters incoming and outgoing network traffic based on rules.

- Allows or blocks traffic based on IP address, port, protocol
- Types: packet filtering, stateful inspection, application layer (WAF)
- Example rule: block all incoming traffic on port 23 (Telnet) because it is unencrypted

### IDS — Intrusion Detection System
Monitors network traffic for suspicious activity and raises an alert.
- It detects but does not block
- Like a security camera — it sees the intruder but cannot stop them

### IPS — Intrusion Prevention System
Monitors network traffic and actively blocks suspicious activity.
- It detects AND blocks
- Like a security guard — it sees the intruder and stops them

---

## Incident Response — Basic Process

When a security incident happens (breach, malware infection, data theft), there is a standard process followed:

| Phase | What happens |
|-------|-------------|
| 1. Preparation | Set up tools, train team, document procedures before an incident happens |
| 2. Identification | Detect that something has gone wrong — alerts, unusual behaviour, user reports |
| 3. Containment | Stop the incident from spreading — isolate infected machines from the network |
| 4. Eradication | Remove the threat — delete malware, close vulnerabilities, reset credentials |
| 5. Recovery | Restore systems to normal operation from clean backups |
| 6. Lessons Learned | Document what happened, why, and how to prevent it next time |

Memory trick: PICERI — Preparation, Identification, Containment, Eradication, Recovery, Improvements.

---

## Security Policies and Frameworks

### Principle of Least Privilege
Give users only the minimum access they need to do their job — nothing more.
Why it matters: If an account is compromised, the attacker can only do what that account could do.

### Defence in Depth
Use multiple layers of security so that if one layer fails, others still protect the system.
Example: Firewall + antivirus + MFA + encryption + monitoring. An attacker who bypasses the firewall still faces the other layers.

### Zero Trust
Never automatically trust any user or device — even inside the network. Always verify.
Motto: Never trust, always verify.

### NIST Cybersecurity Framework
A set of guidelines for managing cybersecurity risk. Five functions:
- Identify — know what assets you have
- Protect — put safeguards in place
- Detect — monitor for threats
- Respond — act when an incident happens
- Recover — restore after an incident

---

## Key Terms Quick Reference

| Term | Meaning |
|------|---------|
| Vulnerability | A weakness in a system that could be exploited |
| Threat | Something that could exploit a vulnerability |
| Risk | The likelihood and impact of a threat exploiting a vulnerability |
| Exploit | Code or technique used to take advantage of a vulnerability |
| Patch | A software update that fixes a vulnerability |
| Zero-day | A vulnerability that is unknown to the vendor and has no patch yet |
| CVE | Common Vulnerabilities and Exposures — a public database of known vulnerabilities |
| Penetration testing | An authorised simulated attack on a system to find vulnerabilities before attackers do |
| Red team | The attackers in a security exercise |
| Blue team | The defenders in a security exercise |
| SOC | Security Operations Centre — a team that monitors and responds to security events |
| SIEM | Security Information and Event Management — collects and analyses logs from all systems |

---

## Notes

- The CIA triad is asked in nearly every cybersecurity interview — know all three with real examples
- MFA is one of the single most effective security controls — stops most account takeover attacks
- Social engineering targets humans, not systems — technical controls alone cannot stop it
- Defence in depth means one layer failing should not mean the whole system is compromised
- Incident response follows the same basic process in almost every organisation
