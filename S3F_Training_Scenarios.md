# 🎯 S3F Training Scenarios

## Overview

This document provides realistic social engineering training scenarios mapped to the Social 3ngineering Framework (S3F). Each scenario simulates a complete attack chain, covering multiple S3F phases and techniques.

**Purpose:**
- Train security teams to recognize social engineering attacks
- Practice incident response procedures
- Build muscle memory for detection and response
- Test organizational defenses

**How to Use:**
- **Tabletop Exercises:** Walk through scenarios with team discussion
- **Phishing Simulations:** Adapt scenarios for email campaigns
- **Red Team Exercises:** Use as blueprints for realistic testing
- **Security Awareness:** Educate employees on attack patterns

---

## Scenario Index

| Scenario | Threat Actor | Target | S3F Phases | Difficulty |
|----------|--------------|--------|------------|------------|
| [1. The Helpful Vendor](#scenario-1-the-helpful-vendor) | Criminal (Financial) | Finance Dept | 1,2,3,4,5 | Intermediate |
| [2. The Midnight Insider](#scenario-2-the-midnight-insider) | Insider Threat | IT Systems | 4,5,6 | Advanced |
| [3. The Executive Emergency](#scenario-3-the-executive-emergency) | BEC Group | C-Suite/Finance | 2,3,4,6 | Beginner |

---

## Scenario 1: The Helpful Vendor

**Threat Actor Profile:** Organized cybercrime group (financially motivated)  
**Primary Target:** Finance department, accounts payable  
**Attack Duration:** 6 weeks  
**S3F Phases Covered:** 1 (Reconnaissance), 2 (Pretexting), 3 (Initial Contact), 4 (Manipulate Trust), 5 (Exploit Trust)

### Attack Timeline

---

#### Week 1: Reconnaissance (S3F Phase 1)

**Attacker Actions:**

The threat actors begin by gathering intelligence on your organization:

1. **OSINT Collection (1.1):**
   - Scrape company website for org chart and employee names
   - Harvest LinkedIn profiles of finance team members
   - Identify accounts payable manager: Sarah Chen
   - Note company uses NetSuite ERP system (from job postings)

2. **Social Media Profiling (1.3):**
   - Review Sarah Chen's LinkedIn: Recently promoted to AP Manager
   - Identify her direct reports and common vendors
   - Note she follows several NetSuite user groups
   - Find posts about Q4 vendor payment deadlines

3. **Infrastructure Analysis (1.1):**
   - Identify primary vendor: "TechSupply Solutions"
   - Register similar domain: `techsupply-invoicing.com` (vs legitimate `techsupply.com`)
   - Set up professional-looking website with copied branding
   - Create email: `billing@techsupply-invoicing.com`

**Facilitator Clues for Participants:**

> Your brand monitoring service alerts you to a new domain registration: `techsupply-invoicing.com`
> 
> **Question:** What should you do with this information?

**Expected Participant Actions:**
- Report to security team
- Check if it's legitimate (contact real TechSupply)
- Monitor for phishing attempts
- Add to threat intel

---

#### Week 2-3: Pretexting & Deception (S3F Phase 2)

**Attacker Actions:**

1. **Initial Impersonation (2.1.3 - Vendor Impersonation):**
   - Email to Sarah from `billing@techsupply-invoicing.com`:
   
   ```
   Subject: TechSupply Portal Migration - Action Required
   
   Hi Sarah,
   
   As part of our system upgrade, we're migrating to a new invoicing portal.
   To ensure uninterrupted service, please update your records:
   
   New Billing Email: billing@techsupply-invoicing.com
   New Portal: portal.techsupply-invoicing.com
   
   You'll receive invoices from this address starting next week.
   
   Thank you,
   Michael Torres
   TechSupply Billing Operations
   ```

2. **Authority & Legitimacy Building (2.2):**
   - Email appears professional with real TechSupply logo
   - Signature includes phone number (VoIP line attackers control)
   - Mentions real upcoming delivery (from reconnaissance)

**Facilitator Clues:**

> Sarah receives this email. She's busy with end-of-quarter processing.
> 
> **Questions:**
> - What red flags should Sarah notice?
> - What verification steps should she take?
> - Who should be notified?

**Red Flags:**
- Different domain (`techsupply-invoicing.com` vs `techsupply.com`)
- Unsolicited change request
- Urgency around action required
- No prior notification through normal channels

---

#### Week 3-4: Initial Contact & Engagement (S3F Phase 3)

**Attacker Actions:**

1. **Credential Harvesting Attempt (3.1 - Spear Phishing):**
   - Follow-up email with link to "new portal":
   
   ```
   Subject: Portal Access - Confirm Your Account
   
   Hi Sarah,
   
   Please confirm your account access for the new TechSupply portal.
   Click below to verify your credentials and ensure continuous access:
   
   [Confirm Account] → portal.techsupply-invoicing.com/login
   
   This is required before we process your next invoice.
   
   Best regards,
   Michael Torres
   ```

2. **Fake Login Page (3.1.5 - Custom Malicious Attachments):**
   - Login page mimics real TechSupply portal
   - Captures username and password
   - Redirects to real TechSupply site after credential capture

**Facilitator Decision Point:**

> **Scenario Branch A:** Sarah clicks the link and enters credentials
> **Scenario Branch B:** Sarah verifies with real TechSupply first
> 
> **For Facilitators:** Use Branch A to demonstrate full attack chain

---

#### Week 5: Manipulate Trust (S3F Phase 4)

**Attacker Actions (If credentials captured):**

1. **Build Relationship (4.4 - Liking & Rapport):**
   - "Michael Torres" calls Sarah: "Hi, just following up on the portal migration"
   - Friendly, professional tone
   - Mentions specific vendors and invoices (from recon)
   - Offers "help" with any questions

2. **Small Requests (4.5.1 - Small Initial Requests):**
   - Email: "Can you confirm receipt of Invoice #8844? Want to make sure our system is working"
   - Sarah confirms (normal business activity)
   - Attackers now know she's engaged

3. **Escalating Trust (4.4.6 - Active Listening):**
   - "Michael" remembers details from conversations
   - Sends "helpful" reminders about payment deadlines
   - Becomes a "trusted" contact

**Facilitator Clues:**

> Over 2 weeks, Sarah has exchanged 6 emails with "Michael" about routine billing matters.
> He's been professional and helpful.
>
> **Question:** Is this normal vendor behavior? What makes this concerning?

---

#### Week 6: Exploit Trust (S3F Phase 5)

**Attacker Actions:**

1. **The Strike (5.3 - Supply Chain Attack via Vendor Relationship):**
   - Email from "Michael Torres":
   
   ```
   Subject: URGENT: Updated Bank Account for Wire Transfer
   
   Hi Sarah,
   
   Quick heads up - TechSupply has changed our banking information.
   Please update for the wire transfer due this Friday (Invoice #9123 - $47,500):
   
   New Account Details:
   Bank: First National Bank
   Account #: 8847-2993-4421
   Routing #: 021000021
   Swift: FNBBUS33
   
   This is time-sensitive as we're closing our old account on Friday.
   Can you confirm you've updated your records?
   
   Thanks for your help!
   Michael
   ```

2. **Urgency & Authority (4.1.1 - Timeliness):**
   - Creates time pressure (Friday deadline)
   - Legitimate-looking invoice attached
   - References real purchase order number

**Facilitator Decision Point:**

> Sarah needs to process this $47,500 wire transfer by Friday.
> The invoice matches a real pending payment.
> "Michael" has been helpful for weeks.
>
> **Critical Questions:**
> - What verification should Sarah do before changing bank details?
> - What organizational controls should prevent this?
> - Who needs to approve this change?

**Correct Response:**
1. Call TechSupply's main number (not "Michael's" number)
2. Verify with procurement/contracts team
3. Require dual authorization for banking changes
4. Check vendor portal directly (not through email link)

---

### Debrief Questions

**Detection:**
1. At what point could we have detected this attack?
2. What technical controls failed or were absent?
3. Which log sources would show this activity?

**Response:**
4. If detected at Week 2, what should our response be?
5. If the wire transfer was sent, what are our recovery options?
6. How do we prevent this from happening again?

**Policy & Process:**
7. What verification procedures should exist for banking changes?
8. Should vendors be able to request banking updates via email?
9. What training would have helped Sarah recognize this?

**Lessons Learned:**
10. Map each stage to S3F phases - which detections exist in your organization?
11. What would SIEM rules for this attack look like?
12. How could we red team this scenario safely?

---

## Scenario 2: The Midnight Insider

**Threat Actor Profile:** Disgruntled employee with privileged access  
**Primary Target:** Corporate database / intellectual property  
**Attack Duration:** 3 months  
**S3F Phases Covered:** 4 (Manipulate Trust), 5 (Exploit Trust), 6 (Weaponize Trust)

### Background

David Martinez, Senior Database Administrator (10 years tenure), was passed over for promotion to IT Director. The position went to an external hire. David feels undervalued and has growing financial pressures.

---

### Month 1: Building Justification (S3F Phase 4)

**Insider Actions:**

1. **Rationalization:**
   - David convinces himself the company "owes him"
   - Begins researching data value on dark web
   - Contacts competitor recruiters (plausible deniability)

2. **Reconnaissance (Internal) (1.1 modified for insider):**
   - Reviews database schemas he already has access to
   - Identifies high-value customer data and source code repos
   - Maps data locations and access controls
   - Notes monitoring gaps (weak audit logging on certain systems)

3. **Manipulation of Colleagues (4.4 - Liking & Rapport):**
   - Asks junior DBA to "help test" a backup script
   - Script actually copies data to external staging location
   - Junior DBA unwittingly assists with exfiltration prep

**Facilitator Clues:**

> Your UEBA system flags unusual activity:
> - David accessing database schemas outside his normal responsibilities
> - Late-night VPN sessions (previously rare)
> - Spike in database query volume
>
> **Questions:**
> - Is this normal DBA activity?
> - What additional context do we need?
> - Should we investigate now or monitor?

---

### Month 2: Preparing the Theft (S3F Phase 5)

**Insider Actions:**

1. **Creating Backdoor Access (5.1.3 - Malicious Insider):**
   - Creates "service account" with DBA privileges
   - Justifies as "monitoring automation"
   - Account not tied to him personally (layer of deniability)

2. **Data Staging (5.1.6 - Data Exfiltration prep):**
   - Modifies backup scripts to copy sensitive data to staging server
   - Staging server is "old decommissioned box" he's "repurposing"
   - Data encrypted on staging server ("for security")

3. **Avoiding Detection (5.1.7 - Policy Violations):**
   - Disables certain audit logs ("performance optimization")
   - Schedules data copies during backup windows (blends in)
   - Uses approved tools (pg_dump, mysqldump) so no "malware"

**Facilitator Clues:**

> Security team receives alerts:
> 1. New service account created by David (DB_MONITOR_SVC)
> 2. Audit logging disabled on customer database
> 3. Large data transfers to internal IP 10.50.22.18
>
> David's explanation: "Performance tuning and setting up monitoring"
>
> **Questions:**
> - Do we accept this explanation?
> - What corroborating evidence should we look for?
> - Who should authorize audit log changes?

---

### Month 3: The Exfiltration (S3F Phases 5-6)

**Insider Actions:**

1. **Data Theft (5.1.6 - Data Exfiltration):**
   - Copies 500GB of customer data, source code, strategic plans
   - Compresses and encrypts as "backup-2026-06-15.tar.gz"
   - Uploads to personal cloud storage during weekend

2. **Covering Tracks:**
   - Deletes staging server logs
   - Removes service account
   - Schedules vacation time (reduce suspicion)

3. **Monetization Attempt (6.6 - Trust as Vulnerability at scale):**
   - Contacts competitor
   - Offers data for $250,000
   - Maintains plausible deniability ("consulting opportunity")

**Detection Point:**

> DLP system alerts on Sunday 2 AM:
> - Massive upload to mega.nz from David's workstation
> - Files encrypted, but metadata shows DB-related naming
> - IP address from David's home
>
> **Critical Response Questions:**
> - What immediate actions do we take?
> - Do we confront David or conduct covert investigation?
> - Who needs to be notified (Legal, HR, Law Enforcement)?
> - How do we preserve evidence?

---

### Debrief Questions

**Insider Threat Program:**
1. What behavioral indicators did we miss?
2. Should HR have flagged David's recent negative performance review?
3. What technical controls could have prevented this?

**Access Controls:**
4. Should DBAs have unrestricted access to all data?
5. How do we balance operational needs with security?
6. What separation of duties was missing?

**Detection:**
7. At what point was detection still possible?
8. What UEBA rules would catch this?
9. How do we detect legitimate tools used maliciously?

**Response:**
10. If discovered at Month 1 vs Month 3, how does response differ?
11. What legal considerations affect our response?
12. How do we handle the junior DBA who unwittingly helped?

**Prevention:**
13. How could better employee relations have prevented this?
14. What off-boarding controls should exist?
15. Should we have required two-person rule for sensitive data access?

---

## Scenario 3: The Executive Emergency

**Threat Actor Profile:** Business Email Compromise (BEC) group  
**Primary Target:** CEO and Finance Director  
**Attack Duration:** 48 hours (rapid attack)  
**S3F Phases Covered:** 2 (Pretexting), 3 (Initial Contact), 4 (Manipulate Trust), 6 (Weaponize Trust)

### Hour 0: The Setup (S3F Phase 2)

**Attacker Actions:**

1. **Reconnaissance (Pre-attack):**
   - Public research: CEO Jennifer Williams traveling to Singapore for conference
   - CFO Robert Kim listed as emergency contact
   - Discovered from LinkedIn posts and conference agenda

2. **Domain Spoofing (2.1.1 - Authority Figure Impersonation):**
   - Register domain: `yourcompany-corp.com` (vs `yourcompany.com`)
   - Setup email: `j.williams@yourcompany-corp.com`
   - Configure DMARC bypass techniques

3. **Timing:**
   - Attack launched Sunday evening (reduced scrutiny)
   - CEO actually in Singapore (14 hour time difference)
   - CFO at home with family

---

### Hour 1-6: The Emergency (S3F Phases 3-4)

**Email to CFO Robert Kim:**

```
From: Jennifer Williams <j.williams@yourcompany-corp.com>
To: Robert Kim <r.kim@yourcompany.com>
Sent: Sunday, 6:42 PM
Subject: URGENT: Confidential Acquisition

Robert,

I'm in final negotiations for acquiring DataTech Solutions - huge opportunity.
Legal needs wire transfer TONIGHT to secure deal before Monday announcement.

Can you approve emergency wire for $485,000 USD?

Board approved, but this is highly confidential. Please handle personally.
Time-sensitive - they need funds by midnight EST.

Details attached. Call my Singapore number if issues: +65-XXXX-XXXX

Jennifer
Sent from my iPhone
```

**Attachment:** Professional-looking "acquisition agreement" PDF

**Manipulation Techniques Used:**
- **Authority (4.2):** CEO requesting
- **Urgency (4.1.1):** Tonight deadline
- **Secrecy:** "Confidential, handle personally"
- **Social Proof (4.3):** "Board approved"
- **Legitimacy:** CEO actually in Singapore

**Facilitator Decision Point:**

> Robert receives this at 6:42 PM on Sunday.
> He knows Jennifer is in Singapore.
> $485,000 wire is unusual but not unprecedented.
>
> **Questions:**
> - What should Robert do immediately?
> - What verification steps are required?
> - Who can he contact to verify?

---

### Hour 6-12: The Pressure (S3F Phase 4)

**If Robert shows hesitation:**

**Follow-up Email (Hour 7):**
```
Subject: Re: URGENT: Confidential Acquisition

Robert - did you see my email? We're running out of time.

This is the deal we discussed last month. Legal is waiting.

I can't be on calls right now (in sensitive meetings), but this is critical.

Trust me on this one. Wire details in attachment.

-J
```

**Text Message (if Robert has CEO's number):**
```
[from +65 number]
"Robert, please confirm wire sent. Board is asking for status."
```

**Psychological Manipulation:**
- Repetition (4.5.5 - Foot-in-the-Door)
- Trust appeal (4.4.6)
- Time pressure intensifies
- Implied criticism ("I can't believe this isn't done yet")

---

### Hour 12-24: The Transaction (S3F Phase 6)

**Wire Transfer Request:**
```
Recipient: DataTech Solutions LLC
Bank: International Banking Corp, Singapore
Account: SG44-8821-9932-7744
Amount: $485,000 USD
Reference: Acquisition-2026-DTS
```

**Facilitator Critical Decision:**

> Robert is about to approve the wire transfer.
> Finance system requires two approvals for amounts over $100K.
> Robert can override as CFO.
>
> **Final Questions:**
> - Does Robert override and approve?
> - What verification MUST happen first?
> - What organizational controls exist?

**Correct Response:**
1. Call CEO's KNOWN cell number (not the provided number)
2. Verify through another exec (COO, General Counsel)
3. Contact Legal/M&A team directly
4. Never override dual-approval without verification
5. If unable to verify, WAIT until morning

---

### Hour 24-48: The Discovery (If wire sent)

**Reality:**
- CEO Jennifer never sent the email
- "DataTech Solutions" doesn't exist
- Singapore bank account leads to money mule network
- $485,000 transferred to cryptocurrency immediately

**Incident Response:**

**Immediate (Hour 24-26):**
1. Contact bank - attempt recall
2. File fraud report
3. Contact FBI (wire fraud)
4. Preserve all evidence
5. Reset email security

**Investigation (Hour 26-48):**
1. How did attackers know CEO travel schedule?
2. Were any accounts actually compromised?
3. Review all financial transactions from weekend
4. Check for other potential victims

**Legal/PR (Hour 48+):**
1. Determine if breach notification required
2. Insurance claim (cyber insurance)
3. Internal communication plan
4. External communication if needed

---

### Debrief Questions

**Prevention:**
1. Should executive travel be publicly disclosed?
2. What email authentication (DMARC, SPF, DKIM) gaps exist?
3. How do we detect display name spoofing?

**Policy:**
4. Should ANY wire transfers be approved outside business hours?
5. Should CFO be able to override dual-approval?
6. What should callback verification policy be?

**Detection:**
7. What SIEM rules would detect this?
8. Should email from slight domain variants be flagged?
9. How do we detect urgency keywords + financial requests?

**Response:**
10. At what point was the fraud still preventable?
11. What's our actual wire recall success rate?
12. How do we recover from this financially and reputationally?

**Organizational Culture:**
13. Does our culture allow pushing back on exec requests?
14. How do we train staff to verify, even under pressure?
15. What's the balance between speed and security?

---

## Using These Scenarios

### Tabletop Exercise Format

**Setup (15 minutes):**
- Distribute scenario to participants
- Assign roles (CFO, SOC Analyst, CISO, etc.)
- Set ground rules (no blame, learning focus)

**Walkthrough (45 minutes):**
- Present scenario phase by phase
- Pause at each decision point
- Facilitate discussion
- Document participant decisions

**Debrief (30 minutes):**
- Review what happened
- Map to S3F framework
- Identify gaps in detection/response
- Create action items

**Follow-up:**
- Assign owners to action items
- Schedule re-test in 6 months
- Update policies/procedures
- Provide training where gaps found

### Red Team Simulation

**Warning:** Only conduct with proper authorization and legal approval.

1. **Planning:**
   - Get executive and legal approval
   - Define scope and boundaries
   - Establish safe words/abort procedures
   - Brief limited team (CISO, Legal, HR)

2. **Execution:**
   - Follow scenario but adapt to organization
   - Stop before any actual harm (data loss, financial loss)
   - Document all steps taken
   - Monitor target responses

3. **Debrief:**
   - Reveal exercise to all involved
   - No punishment for "victims"
   - Focus on organizational learnings
   - Improve controls based on findings

### Security Awareness Training

1. **Use scenario as case study** in training
2. **Quiz employees:** "What would you do?"
3. **Provide actual emails/calls** from scenario
4. **Practice verification techniques**
5. **Role-play exercises**

---

## Scenario Difficulty Levels

### Beginner
- Clear red flags present
- Single S3F phase
- Limited attacker persistence
- Example: Scenario 3 (Executive Emergency)

### Intermediate
- Subtle indicators
- Multiple S3F phases
- Moderate duration (weeks)
- Example: Scenario 1 (Helpful Vendor)

### Advanced
- Highly realistic
- Full attack chain
- Long duration (months)
- Insider knowledge
- Example: Scenario 2 (Midnight Insider)

---

## Creating Custom Scenarios

### Template

1. **Define Threat Actor:**
   - Motivation (financial, espionage, hacktivism)
   - Sophistication level
   - Resources available

2. **Select Target:**
   - Department or individual
   - Why are they targeted?
   - What access/information do they have?

3. **Map S3F Phases:**
   - Which phases will be covered?
   - What techniques within each phase?
   - What's the attack timeline?

4. **Identify Decision Points:**
   - Where could victim prevent attack?
   - What are the red flags?
   - What organizational controls should exist?

5. **Create Artifacts:**
   - Sample emails
   - Fake documents
   - Phone scripts
   - Website screenshots

6. **Develop Debrief:**
   - Learning objectives
   - Discussion questions
   - Action items template

---

## Additional Resources

- [S3F_SOC_Playbook.md](S3F_SOC_Playbook.md) - Response procedures for each phase
- [S3F_TTPs.md](S3F_TTPs.md) - Complete technique taxonomy
- [S3F_Training_Simulation_Template.md](S3F_Training_Simulation_Template.md) - Simple scenario template

---

**Document Version:** 1.0  
**Last Updated:** 2026-07-03  
**Created By:** S3F Training Team  
**Contact:** cbkittner@gmail.com

**License:** GNU General Public License v3.0 (GPL-3.0)

---

*These scenarios are for training purposes only. Always obtain proper authorization before conducting any security testing or simulations.*
