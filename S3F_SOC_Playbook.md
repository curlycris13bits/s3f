# 🛡️ S3F SOC Playbook

## Overview

This playbook provides Security Operations Center (SOC) teams with actionable detection and response procedures aligned to the Social 3ngineering Framework (S3F). It maps social engineering attack phases to observable indicators, detection methods, and response workflows.

**Purpose:**
- Enable SOC analysts to identify social engineering campaigns in progress
- Provide phase-specific response procedures based on attack lifecycle
- Integrate human-focused threat intelligence into technical security operations
- Bridge the gap between behavioral attacks and technical detection

**Target Audience:**
- SOC Analysts (Tier 1, 2, 3)
- Incident Responders
- Threat Hunters
- Detection Engineers
- CSIRT Teams

---

## How to Use This Playbook

### 1. Identification
When an alert or suspicious activity is detected, use the **Detection Indicators** section to:
- Identify which S3F phase the activity corresponds to
- Classify the attack technique being employed
- Understand the attacker's current objective

### 2. Response
Once classified, follow the phase-specific **Response Procedures** to:
- Contain the immediate threat
- Investigate scope and impact
- Collect evidence
- Remediate affected systems/users
- Prevent recurrence

### 3. Escalation
Use the **Escalation Matrix** to determine:
- Severity level based on S3F phase and impact
- When to escalate to senior analysts or management
- Who needs to be notified
- Timeline expectations

---

## S3F Phase Overview

| Phase | Attacker Objective | SOC Focus |
|-------|-------------------|-----------|
| **1. Reconnaissance** | Gather intelligence on targets | Monitor external intelligence, detect enumeration |
| **2. Pretexting & Deception** | Establish false identity/scenario | Identify impersonation attempts, verify identities |
| **3. Initial Contact & Engagement** | Initiate interaction with target | Detect phishing, suspicious communications |
| **4. Manipulate Trust** | Build rapport and influence | Monitor behavioral anomalies, unusual requests |
| **5. Exploit Trust** | Leverage established trust for access | Detect privilege abuse, unauthorized access |
| **6. Weaponize Trust** | Use compromised trust at scale | Identify insider threats, widespread campaigns |

---

## Phase 1: Reconnaissance

### Detection Indicators

**Technical Indicators:**
- Unusual web scraping or API requests targeting employee directories
- Excessive LinkedIn profile views from unknown accounts
- OSINT tool signatures in web server logs (theHarvester, Recon-ng, etc.)
- Abnormal DNS queries for organization domains
- Social media monitoring tool traffic
- Increased failed authentication attempts (username enumeration)
- Suspicious Google Dorks targeting organization data

**Behavioral Indicators:**
- Reports of unfamiliar individuals asking detailed questions about staff
- Employees receiving friend requests from fake profiles
- Strangers photographing facilities or asking about security measures
- Unusual questions about organizational structure in public forums
- Discovery of organization data in breach databases or paste sites

**Log Sources:**
- Web server access logs
- DNS query logs
- Email gateway logs (external reconnaissance emails)
- Physical security logs (visitor logs, camera footage)
- LinkedIn/social media monitoring alerts
- Dark web monitoring feeds

### Response Procedures

**Immediate Actions (0-2 hours):**
1. **Document the activity** - Capture all reconnaissance indicators (IPs, domains, accounts)
2. **Check for active engagement** - Has reconnaissance led to contact attempts?
3. **Review recent communications** - Search email/Slack for unsolicited outreach
4. **Alert security awareness team** - Prepare targeted warnings for likely targets

**Investigation (2-24 hours):**
1. **Correlate with threat intelligence** - Check if IOCs match known APT/criminal groups
2. **Identify reconnaissance scope** - Which departments/individuals are being targeted?
3. **Review third-party exposure** - Check data brokers, LinkedIn, public records
4. **Assess vulnerability** - What information is publicly available?

**Containment:**
1. **Limit public exposure** - Review and restrict overly detailed public profiles
2. **Brief high-value targets** - Warn executives, HR, IT staff of increased risk
3. **Enhance monitoring** - Implement heightened alerting for targeted individuals
4. **Consider deception** - Deploy honeytokens or canary accounts

**Remediation:**
1. Update security awareness training with current tactics
2. Review and scrub excessive public information
3. Implement stricter social media policies if needed
4. Document TTPs for future detection tuning

**Escalation Criteria:**
- Reconnaissance indicates nation-state APT patterns → Escalate to Tier 3/Threat Intel
- Multiple departments targeted → Notify CISO
- Reconnaissance precedes known attack campaign → Activate Incident Response

---

## Phase 2: Pretexting & Deception

### Detection Indicators

**Technical Indicators:**
- Email from spoofed/similar domains (typosquatting)
- Caller ID spoofing detected on phone systems
- Newly registered domains mimicking organization name
- SSL certificates issued for look-alike domains
- Emails with mismatched display name and sender address
- VoIP traffic from suspicious gateways
- Deepfake detection alerts (if deployed)

**Behavioral Indicators:**
- Employees report calls from "IT support" requesting credentials
- Unusual requests from "executives" outside normal channels
- Vendors claiming changed payment details
- Unexpected "HR" requests for personal information
- Inconsistencies in communication style/language from known contacts
- Pressure tactics citing urgency or authority

**Log Sources:**
- Email gateway logs (header analysis, DMARC failures)
- Phone system logs (CDR records, caller ID data)
- Domain monitoring services (certificate transparency logs)
- DNS threat intelligence feeds
- Help desk ticket systems (unusual password reset requests)
- Badge access logs (physical impersonation attempts)

### Response Procedures

**Immediate Actions (0-1 hours):**
1. **Verify sender identity** - Call back using known phone number, check email headers
2. **Quarantine suspicious messages** - Isolate phishing emails before users interact
3. **Alert affected users** - Send targeted warnings about impersonation attempt
4. **Block malicious infrastructure** - Null-route domains, block caller IDs

**Investigation (1-12 hours):**
1. **Scope the campaign** - How many users received pretexting attempts?
2. **Identify the pretext** - What story/identity is attacker using?
3. **Check for successes** - Did anyone fall for the pretext?
4. **Trace infrastructure** - WHOIS lookups, hosting provider, registration data
5. **Review recent breaches** - Is attacker using stolen organizational knowledge?

**Containment:**
1. **Implement email filtering rules** - Block sender domains/patterns
2. **Enable stricter authentication** - Require callback verification for sensitive requests
3. **Brief reception/help desk** - Alert front-line staff about impersonation tactics
4. **Deploy warning banners** - Flag external emails prominently

**Remediation:**
1. Reset credentials if any were disclosed
2. Report malicious infrastructure (domain registrars, hosting providers)
3. Issue organization-wide security alert with examples
4. Update email security policies and filters
5. Conduct tabletop exercise with common pretexts

**Escalation Criteria:**
- CEO/executive impersonation → Notify leadership immediately
- Multiple successful pretexts → Activate Incident Response
- Financial fraud attempt → Alert Legal and Finance
- Deepfake voice/video detected → Escalate to Tier 3, notify executive team

---

## Phase 3: Initial Contact & Engagement

### Detection Indicators

**Technical Indicators:**
- Spear phishing emails with personalized content
- Malicious attachments (macros, executables, PDFs)
- Links to credential harvesting pages
- QR codes leading to phishing sites
- Watering hole compromises targeting organization
- Malicious calendar invites with embedded links
- LinkedIn messages with malware links

**Behavioral Indicators:**
- Employees report unsolicited outreach with specific references to projects
- Messages referencing recent company news or events
- Requests to open files from unknown but "trusted" senders
- Meeting invitations from external parties claiming shared connections
- Direct messages on Slack/Teams from unknown accounts
- Physical mail with USB drives or QR codes

**Log Sources:**
- Email security gateway (attachment analysis, link scanning)
- Web proxy logs (clicks on suspicious links)
- Endpoint detection (file execution, macro activity)
- Network IDS/IPS (C2 beaconing, data exfiltration)
- Authentication logs (credential harvesting attempts)
- Cloud access logs (OAuth phishing, consent grants)

### Response Procedures

**Immediate Actions (0-1 hours):**
1. **Quarantine malicious messages** - Remove from all mailboxes
2. **Block malicious URLs/domains** - Update web filters and firewalls
3. **Isolate affected endpoints** - If malware executed, contain immediately
4. **Disable compromised accounts** - If credentials harvested, reset and lock
5. **Alert users** - Send targeted warning about active campaign

**Investigation (1-8 hours):**
1. **Analyze payload** - Reverse engineer attachments/links in sandbox
2. **Identify patient zero** - Who was targeted first? Who clicked/opened?
3. **Check for compromise** - EDR analysis, memory forensics, network traffic
4. **Map campaign scope** - How many users targeted? Success rate?
5. **Attribute attacker** - TTP analysis, infrastructure correlation

**Containment:**
1. Network segmentation for affected systems
2. Revoke OAuth tokens if cloud phishing successful
3. Block C2 infrastructure at perimeter
4. Deploy detection rules for campaign-specific IOCs
5. Force password resets for exposed credentials

**Remediation:**
1. Re-image compromised systems if malware executed
2. Review and restore any deleted/encrypted files
3. Patch vulnerabilities exploited in attack chain
4. Update email filtering rules based on campaign TTPs
5. Conduct forensic timeline and document lessons learned

**Escalation Criteria:**
- Malware executed on system → Escalate to Incident Response
- Credentials compromised → Notify IAM team, force org-wide MFA check
- High-value target affected (exec, admin) → Notify CISO
- Multiple systems compromised → Declare security incident

---

## Phase 4: Manipulate Trust

### Detection Indicators

**Technical Indicators:**
- Unusual activity from legitimate user accounts (compromised or coerced)
- Email conversations with external parties showing rapport-building
- Repeated small requests escalating in sensitivity (foot-in-the-door)
- Approval workflows bypassed with "urgent" justifications
- Access requests outside normal user behavior patterns
- Data access by users with no business justification
- Abnormal working hours or geographic locations for trusted accounts

**Behavioral Indicators:**
- Users report feeling pressured by colleagues/vendors to take actions
- Requests for policy exceptions citing deadlines or authority
- Employees mentioning "helpful" external contacts offering assistance
- Unusual gift-giving or favor-trading observed
- Reports of emotional manipulation or guilt tactics
- Users second-guessing security policies due to "special circumstances"

**Log Sources:**
- Email content analysis (DLP, sentiment analysis)
- User Behavior Analytics (UBA) platforms
- Access management logs (unusual privilege requests)
- Application logs (policy override attempts)
- HR reports (employee concerns about manipulation)
- Approval workflow audit logs

### Response Procedures

**Immediate Actions (0-4 hours):**
1. **Interview affected user** - Understand the manipulation attempt context
2. **Review communication history** - Analyze emails/messages for persuasion tactics
3. **Check for policy violations** - Were any unauthorized actions taken?
4. **Verify external party identity** - Is the "helpful" contact legitimate?
5. **Alert similar targets** - Warn others who may receive same approach

**Investigation (4-24 hours):**
1. **Map the relationship** - How was trust established? Over what timeline?
2. **Identify manipulation techniques** - Authority, reciprocity, urgency, etc.
3. **Assess damage** - What information or access was gained?
4. **Check for insider involvement** - Is an internal actor complicit?
5. **Review similar patterns** - Are others being manipulated similarly?

**Containment:**
1. **Limit user permissions** - Reduce access for manipulated individuals
2. **Enhanced approval controls** - Require dual authorization for sensitive actions
3. **Monitor communications** - Flag continued interaction with suspicious parties
4. **Brief management** - Ensure leadership understands manipulation in progress
5. **Implement cooling-off periods** - Delay execution of "urgent" requests

**Remediation:**
1. Provide psychological support/counseling if needed
2. Retrain affected users on manipulation tactics
3. Update approval workflows to prevent future exploitation
4. Document manipulation playbook for awareness training
5. Review and strengthen business process controls

**Escalation Criteria:**
- Financial transaction authorized under manipulation → Notify Finance/Legal
- Sensitive data disclosed → Activate Data Breach Response
- Insider threat suspected → Engage HR and Legal
- Multiple employees manipulated → Escalate to executive team

---

## Phase 5: Exploit Trust

### Detection Indicators

**Technical Indicators:**
- Legitimate credentials used for unauthorized access
- Insider accessing systems/data outside their role
- Privilege escalation by compromised account
- Data exfiltration from trusted accounts
- Supply chain compromise (vendor access abused)
- Malicious code commits from trusted developers
- Backdoor accounts created with administrative rights
- Unusual after-hours VPN/remote access from trusted users

**Behavioral Indicators:**
- Employees noticed accessing confidential information without justification
- Vendors requesting access beyond contract scope
- Users copying large amounts of data before departing
- Trusted partners asking for architectural details
- Employees exhibiting signs of coercion or duress
- Unusual interest in security controls or monitoring gaps

**Log Sources:**
- Data Loss Prevention (DLP) alerts
- Privileged Access Management (PAM) logs
- File access audit logs (SIEM correlation)
- Database audit logs (SELECT statements on sensitive tables)
- Cloud access logs (AWS CloudTrail, Azure Activity Log)
- Version control system logs (Git, SVN)
- VPN and remote access logs
- Badge access logs (physical access anomalies)

### Response Procedures

**Immediate Actions (0-2 hours):**
1. **Suspend compromised accounts** - Disable access immediately
2. **Isolate affected systems** - Prevent lateral movement
3. **Preserve evidence** - Capture memory, logs, network traffic
4. **Assess data exposure** - What was accessed/exfiltrated?
5. **Notify legal team** - Potential insider threat or breach

**Investigation (2-48 hours):**
1. **Forensic analysis** - Full timeline of account activity
2. **Determine intent** - Malicious insider vs. compromised account?
3. **Scope exfiltration** - What data left the organization?
4. **Identify co-conspirators** - Are others involved?
5. **Review supply chain** - Are vendor/partner accesses compromised?
6. **Interview subject** - If insider, conduct HR/security interview

**Containment:**
1. Revoke all access for compromised accounts/insiders
2. Reset credentials for all privileged accounts
3. Segment networks to prevent further compromise
4. Block data exfiltration channels (USB, cloud storage, email)
5. Implement enhanced monitoring on similar privileged accounts

**Remediation:**
1. Terminate insider access (employment/contract)
2. Recover or secure exfiltrated data
3. Patch vulnerabilities that enabled privilege escalation
4. Implement Zero Trust architecture principles
5. Enhance insider threat detection capabilities
6. Legal action if warranted

**Escalation Criteria:**
- Intellectual property stolen → Notify Legal, consider law enforcement
- Financial fraud committed → Notify Finance, Legal, law enforcement
- Nation-state espionage suspected → Notify FBI, CISA
- Safety/operational impact → Escalate to executive crisis team
- Regulatory data breach → Activate breach notification procedures

---

## Phase 6: Weaponize Trust

### Detection Indicators

**Technical Indicators:**
- Deepfake audio/video of executives detected
- Mass phishing campaign using compromised legitimate accounts
- Disinformation spread through official social media channels
- AI-generated content mimicking organization communications
- Large-scale credential stuffing using leaked employee data
- Synthetic identity creation at scale
- Business Email Compromise (BEC) targeting multiple partners
- Coordinated inauthentic behavior on social platforms

**Behavioral Indicators:**
- Reports of fake audio/video of executives circulating
- Widespread confusion about contradictory "official" communications
- Multiple vendors reporting suspicious payment change requests
- Public-facing disinformation campaign targeting organization
- Employees reporting elaborate scams using leaked personal details
- Brand impersonation at scale (fake websites, social accounts)

**Log Sources:**
- Brand monitoring services
- Social media monitoring platforms
- Deepfake detection systems
- Email authentication reports (DMARC, SPF, DKIM failures)
- Threat intelligence feeds (domain/brand abuse)
- Customer service reports (impersonation complaints)
- Media monitoring services
- Dark web monitoring

### Response Procedures

**Immediate Actions (0-2 hours):**
1. **Activate crisis response team** - Executive, Legal, PR, Security
2. **Issue public statement** - Warn stakeholders of active campaign
3. **Report to platforms** - Request takedown of fake accounts/content
4. **Alert law enforcement** - FBI, Secret Service, international agencies
5. **Block malicious infrastructure** - Domains, accounts, IP ranges

**Investigation (2-72 hours):**
1. **Attribution analysis** - Who is behind the campaign? Nation-state? Criminal?
2. **Assess scale** - How many victims? What's the reach?
3. **Analyze deepfakes** - Forensic verification of synthetic media
4. **Map infrastructure** - Full C2, hosting, payment infrastructure
5. **Review origin** - How was trust initially compromised?
6. **Document impact** - Financial, reputational, operational damage

**Containment:**
1. Enhanced authentication for all external communications
2. Implement digital signatures for official statements
3. Deploy deepfake detection across communication channels
4. Coordinate with platforms for rapid content removal
5. Legal injunctions against infrastructure providers
6. Work with registrars to seize malicious domains

**Remediation:**
1. Public disclosure and transparency about attack
2. Victim notification and support
3. Reputational recovery campaign
4. Implement advanced authentication (video verification, code words)
5. Long-term monitoring for recurrence
6. Systemic security posture improvements

**Escalation Criteria:**
- Executive deepfake causing stock manipulation → SEC notification, trading halt
- Nation-state disinformation campaign → CISA, FBI, State Department
- Mass financial fraud → Multi-agency law enforcement coordination
- Public safety impact → Emergency services, relevant regulators
- ALL weaponization incidents → Board and C-suite notification required

---

## SIEM Integration

### Recommended Log Sources

**Essential:**
- Email gateway logs (phishing, spoofing detection)
- Authentication logs (AD, SSO, MFA)
- Web proxy logs (malicious link clicks)
- Endpoint detection logs (malware, suspicious processes)
- Network flow data (C2 communication, exfiltration)

**High Value:**
- Badge access logs (physical reconnaissance)
- Phone system logs (vishing attempts)
- Help desk tickets (social engineering reports)
- DLP alerts (data exfiltration)
- Cloud access logs (OAuth phishing, account compromise)

**Contextual:**
- Social media monitoring
- Dark web monitoring
- Threat intelligence feeds
- Brand monitoring services
- HR systems (insider threat indicators)

### Sample SIEM Correlation Rules

#### Rule 1: Spear Phishing Detection
```
Trigger: Email with external sender + attachment + personalized content
AND (Display name matches internal user OR Domain similar to organization)
Severity: Medium
Action: Quarantine, alert SOC
```

#### Rule 2: Credential Harvesting
```
Trigger: Multiple failed logins from single IP
FOLLOWED BY successful login
AND geolocation anomaly
Severity: High
Action: Force MFA, alert SOC, notify user
```

#### Rule 3: Insider Data Exfiltration
```
Trigger: Privileged user accessing > 100 sensitive files in 1 hour
AND (Time = after hours OR Location = unusual)
FOLLOWED BY large file upload to external service
Severity: Critical
Action: Block upload, disable account, page IR team
```

#### Rule 4: BEC Detection
```
Trigger: Email from executive account
AND (Contains financial request OR Payment change)
AND (Sent from unusual location OR Outside business hours)
Severity: High
Action: Hold for manual review, alert finance team
```

### Detection Queries

**Splunk Example - Pretexting Detection:**
```spl
index=email 
| where match(from_domain, ".*organization_name_variant.*") AND from_domain!="legitimate_domain.com"
| stats count by from_address, subject, recipients
| where count > 5
```

**Elastic Example - Reconnaissance Detection:**
```
event.category: "web" AND 
http.request.method: "GET" AND 
url.path: "/employees/*" AND 
source.ip: NOT (internal_network) AND
user_agent: ("*recon*" OR "*harvest*" OR "*scrape*")
```

---

## Escalation Matrix

### Severity Levels

| Level | S3F Phase Range | Criteria | Response Time | Escalation |
|-------|----------------|----------|---------------|------------|
| **Low** | Phase 1 | Passive reconnaissance, no active engagement | 24 hours | Tier 1 → Tier 2 if patterns emerge |
| **Medium** | Phase 2-3 | Active pretexting or phishing, no confirmed compromise | 4 hours | Tier 2, notify management |
| **High** | Phase 4-5 | Confirmed compromise, data access, privilege abuse | 1 hour | Tier 3, activate IR, notify CISO |
| **Critical** | Phase 6 | Weaponized trust, mass impact, deepfakes, BEC | 15 minutes | Full IR, executive team, legal, PR |

### Notification Matrix

| Scenario | SOC | CISO | Legal | HR | PR | Law Enforcement |
|----------|-----|------|-------|----|----|-----------------|
| Phase 1: Reconnaissance | ✓ | If APT | - | - | - | - |
| Phase 2: Pretexting | ✓ | If exec impersonation | If fraud attempt | If HR pretext | - | If financial fraud |
| Phase 3: Phishing Campaign | ✓ | If >10 users affected | - | - | - | - |
| Phase 4: Manipulation Success | ✓ | ✓ | If policy violation | ✓ | - | If criminal |
| Phase 5: Insider Threat | ✓ | ✓ | ✓ | ✓ | If public | ✓ |
| Phase 6: Weaponization | ✓ | ✓ | ✓ | - | ✓ | ✓ |

---

## Incident Response Workflow

### 1. Detection & Triage (Tier 1)
- Alert fires in SIEM
- Analyst reviews indicators
- Classifies S3F phase
- Assigns severity
- Creates ticket

### 2. Investigation & Containment (Tier 2)
- Deep-dive analysis
- Scope determination
- Immediate containment actions
- Evidence collection
- Escalate if needed

### 3. Eradication & Recovery (Tier 3 / IR)
- Remove attacker access
- Remediate vulnerabilities
- Restore affected systems
- Implement preventive controls
- Document lessons learned

### 4. Post-Incident Activities
- Root cause analysis
- Update detection rules
- Security awareness training
- Tabletop exercise development
- Metrics and reporting

---

## Integration with MITRE ATT&CK

Cross-reference S3F phases with MITRE ATT&CK for technical detection:

- **Phase 1: Reconnaissance** → TA0043 Reconnaissance
- **Phase 2: Pretexting** → T1566 Phishing, T1598 Phishing for Information
- **Phase 3: Initial Contact** → T1204 User Execution, T1566 Phishing
- **Phase 4: Manipulate Trust** → T1078 Valid Accounts (human manipulation to obtain)
- **Phase 5: Exploit Trust** → T1078 Valid Accounts, T1098 Account Manipulation
- **Phase 6: Weaponize Trust** → T1586 Compromise Accounts, T1584 Compromise Infrastructure

See [S3F_MITRE_ATTCK_CSIRT_Reference.md](S3F_MITRE_ATTCK_CSIRT_Reference.md) for detailed mapping.

---

## Metrics & KPIs

### Detection Effectiveness
- Mean Time to Detect (MTTD) per S3F phase
- False positive rate by detection rule
- Coverage percentage across S3F techniques

### Response Performance
- Mean Time to Respond (MTTR) per severity level
- Containment success rate
- Escalation accuracy (correct severity assignment)

### Program Health
- User reporting rate (employees reporting suspicious activity)
- Phishing simulation click rates (trending down)
- Repeat victim rate (same users falling for multiple attacks)

---

## References & Training

### Internal Resources
- [S3F_TTPs.md](S3F_TTPs.md) - Complete technique taxonomy
- [S3F_MITRE_ATTCK_CSIRT_Reference.md](S3F_MITRE_ATTCK_CSIRT_Reference.md) - ATT&CK mapping
- [S3F_Training_Simulation_Template.md](S3F_Training_Simulation_Template.md) - Tabletop exercises

### External Resources
- NIST SP 800-61: Computer Security Incident Handling Guide
- SANS Incident Handler's Handbook
- MITRE ATT&CK Framework
- CISA Security Awareness Training Resources

### Recommended Training
- Annual tabletop exercises covering all 6 S3F phases
- Quarterly phishing simulations using current techniques
- Monthly security awareness micro-learning (focus on 1 S3F phase per month)
- Role-specific training (executives, HR, IT staff, finance)

---

## Playbook Maintenance

**Review Schedule:**
- Quarterly review of detection rules and response procedures
- Update after each major incident involving social engineering
- Annual comprehensive revision incorporating new techniques

**Ownership:**
- SOC Manager: Overall playbook accuracy
- Detection Engineering: SIEM rules and queries
- Incident Response: Response procedures
- Security Awareness: Training integration

**Version Control:**
- Maintained in organizational security documentation repository
- Changes tracked via git commits
- Major updates require CISO approval

---

**Document Version:** 1.0  
**Last Updated:** 2026-07-03  
**Maintained By:** SOC Team  
**Contact:** cbkittner@gmail.com

**License:** GNU General Public License v3.0 (GPL-3.0)

---

*This playbook is part of the Social 3ngineering Framework (S3F). For the complete framework, visit the [main repository](https://github.com/curlycris13bits/s3f).*
