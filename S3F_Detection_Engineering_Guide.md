# 🔍 S3F Detection Engineering Guide

## Overview

This guide provides detection engineers with platform-specific SIEM rules, detection logic, tuning guidance, and implementation best practices for detecting social engineering attacks using the S3F framework.

**Purpose:**
- Translate S3F phases into actionable detection rules
- Provide platform-specific query examples
- Guide detection tuning and false positive reduction
- Enable comprehensive social engineering detection coverage

**Target Platforms:**
- Splunk Enterprise Security
- Elastic Security (SIEM)
- Microsoft Sentinel
- IBM QRadar
- Sigma (universal format)

**Target Audience:**
- Detection Engineers
- SIEM Administrators
- Security Architects
- Threat Detection Teams

---

## Table of Contents

1. [Detection Philosophy](#detection-philosophy)
2. [Data Requirements](#data-requirements)
3. [Phase 1: Reconnaissance Detection](#phase-1-reconnaissance-detection)
4. [Phase 2: Pretexting Detection](#phase-2-pretexting-detection)
5. [Phase 3: Initial Contact Detection](#phase-3-initial-contact-detection)
6. [Phase 4: Trust Manipulation Detection](#phase-4-trust-manipulation-detection)
7. [Phase 5: Trust Exploitation Detection](#phase-5-trust-exploitation-detection)
8. [Phase 6: Weaponized Trust Detection](#phase-6-weaponized-trust-detection)
9. [Detection Tuning](#detection-tuning)
10. [Implementation Roadmap](#implementation-roadmap)
11. [Metrics & Validation](#metrics--validation)

---

## Detection Philosophy

### Behavioral vs. Technical Detection

Social engineering attacks require a **hybrid detection approach**:

**Behavioral Indicators:**
- Unusual user behavior patterns
- Anomalous communication patterns
- Policy violations
- Out-of-character actions

**Technical Indicators:**
- Spoofed domains and sender addresses
- Malicious infrastructure
- Credential harvesting sites
- Data exfiltration patterns

### Detection Maturity Model

**Level 1: Signature-Based**
- Known bad IOCs (domains, IPs, file hashes)
- Email reputation checks
- Basic phishing detection

**Level 2: Anomaly-Based**
- Baseline user behavior (UEBA)
- Geographic anomalies
- Time-based anomalies
- Volume-based anomalies

**Level 3: Behavior-Based**
- Multi-event correlation
- Attack chain detection
- Trust relationship modeling
- Social graph analysis

**Level 4: ML/AI-Assisted**
- Natural language processing for email content
- Deepfake detection
- Predictive risk scoring
- Automated threat hunting

### S3F Detection Pyramid

```
        ┌─────────────────┐
        │  Weaponize (6)  │  ← Highest Impact, Lowest Volume
        ├─────────────────┤
        │   Exploit (5)   │
        ├─────────────────┤
        │  Manipulate(4)  │
        ├─────────────────┤
        │Initial Contact(3)│
        ├─────────────────┤
        │  Pretexting (2) │
        ├─────────────────┤
        │Reconnaissance(1)│  ← Lowest Impact, Highest Volume
        └─────────────────┘
```

**Detection Strategy:**
- **Early Phases (1-2):** High-fidelity, low-noise detection
- **Mid Phases (3-4):** Balanced detection with investigation workflows
- **Late Phases (5-6):** Aggressive detection with immediate escalation

---

## Data Requirements

### Essential Data Sources

| Data Source | S3F Phases | Critical Fields | Collection Method |
|-------------|-----------|-----------------|-------------------|
| Email Gateway Logs | 2, 3, 6 | sender, recipient, subject, headers, attachments | Proofpoint, Mimecast, O365 |
| Authentication Logs | 3, 4, 5 | username, source_ip, geo, MFA status, success/failure | AD, SSO, Okta, Azure AD |
| Web Proxy Logs | 1, 3, 5 | url, user, timestamp, user_agent, bytes | Zscaler, Palo Alto, Squid |
| Endpoint Logs | 3, 5, 6 | process, file, network, user | EDR (CrowdStrike, SentinelOne) |
| Network Traffic | 1, 5, 6 | src_ip, dst_ip, port, protocol, bytes | NetFlow, Zeek, Suricata |
| DLP Alerts | 5, 6 | file, user, destination, sensitivity | Forcepoint, Symantec DLP |
| Badge Access | 1, 2, 5 | user, door, timestamp, result | Physical security systems |
| Help Desk Tickets | 2, 3, 4 | subject, category, user, description | ServiceNow, Jira Service Desk |
| Phone System (CDR) | 2 | caller_id, called_number, duration | VoIP PBX, Cisco Call Manager |
| Cloud Access | 3, 5, 6 | user, app, action, geo, device | CASB (CloudLock, Netskope) |

### Data Enrichment

**Critical Enrichments:**
- Geolocation (IP → Country/City)
- Threat Intelligence (IP/Domain/Hash reputation)
- User context (title, department, privileges)
- Asset context (criticality, owner, location)
- Historical baselines (normal user behavior)

**Sources:**
- MaxMind GeoIP
- VirusTotal, AlienVault OTX, Abuse.ch
- LDAP/Active Directory
- CMDB/Asset Inventory
- UEBA platform or custom baselines

---

## Phase 1: Reconnaissance Detection

### Detection Strategy

Reconnaissance is **high-volume, low-fidelity**. Focus on:
- Patterns indicating targeting (not isolated events)
- Anomalous information gathering
- Correlation with known threat actors

### Rule 1.1: OSINT Tool Detection

**Description:** Detect common OSINT tools in web logs

**Splunk:**
```spl
index=web sourcetype=access_combined
| search user_agent IN ("*recon-ng*", "*theHarvester*", "*Shodan*", "*Censys*", "*Maltego*", "*SpiderFoot*", "*Amass*")
| stats count by src_ip, user_agent, url
| where count > 5
| eval severity="medium", s3f_phase="1.1", s3f_technique="OSINT"
```

**Elastic:**
```json
{
  "query": {
    "bool": {
      "must": [
        { "match": { "event.category": "web" }},
        { "terms": { "user_agent.original": ["recon-ng", "theHarvester", "Shodan", "Censys", "Maltego", "SpiderFoot", "Amass"] }}
      ]
    }
  },
  "aggs": {
    "by_ip": {
      "terms": { "field": "source.ip", "min_doc_count": 5 }
    }
  }
}
```

**Microsoft Sentinel (KQL):**
```kql
W3CIISLog
| where TimeGenerated > ago(24h)
| where csUserAgent has_any ("recon-ng", "theHarvester", "Shodan", "Censys", "Maltego", "SpiderFoot", "Amass")
| summarize count() by cIP, csUserAgent, csUriStem
| where count_ > 5
| extend S3F_Phase = "1.1", S3F_Technique = "OSINT", Severity = "Medium"
```

**Tuning Guidance:**
- Whitelist security scanning tools (Nessus, Qualys)
- Adjust threshold based on website traffic volume
- Consider time window (5 hits in 1 hour vs 24 hours)

**False Positive Scenarios:**
- Legitimate security researchers (whitelist by IP/org)
- Internal security testing (coordinate with red/purple team)
- SEO tools and web crawlers (filter by user agent)

---

### Rule 1.2: Excessive LinkedIn Profile Views

**Description:** Detect unusual LinkedIn profile scraping

**Data Source:** LinkedIn Sales Navigator logs, web proxy logs

**Splunk:**
```spl
index=proxy url="*linkedin.com/in/*" OR url="*linkedin.com/company/*"
| stats dc(url) as unique_profiles by user, src_ip
| where unique_profiles > 50
| eval severity="medium", s3f_phase="1.3", s3f_technique="Social_Media_Profiling"
```

**Elastic:**
```json
{
  "query": {
    "bool": {
      "must": [
        { "wildcard": { "url.full": "*linkedin.com/in/*" }}
      ],
      "filter": [
        { "range": { "@timestamp": { "gte": "now-1h" }}}
      ]
    }
  },
  "aggs": {
    "by_user": {
      "terms": { "field": "user.name" },
      "aggs": {
        "unique_profiles": {
          "cardinality": { "field": "url.full" }
        }
      }
    }
  }
}
```

**Tuning:**
- Whitelist recruiters and sales teams
- Adjust threshold based on job role
- Consider normal daily activity patterns

---

### Rule 1.3: Domain Reconnaissance

**Description:** Detect DNS enumeration attempts

**Splunk:**
```spl
index=dns 
| where query_type="ANY" OR query_type="TXT" OR query_type="MX"
| stats dc(query) as unique_queries by src_ip
| where unique_queries > 100
| eval severity="medium", s3f_phase="1.1", s3f_technique="Domain_Lookups"
```

**Elastic:**
```json
{
  "query": {
    "bool": {
      "must": [
        { "terms": { "dns.question.type": ["ANY", "TXT", "MX"] }}
      ]
    }
  },
  "aggs": {
    "by_source": {
      "terms": { "field": "source.ip" },
      "aggs": {
        "unique_queries": {
          "cardinality": { "field": "dns.question.name" }
        }
      }
    }
  }
}
```

**Sigma Rule:**
```yaml
title: DNS Reconnaissance Activity
id: s3f-1.1-dns-recon
status: experimental
description: Detects excessive DNS queries indicating reconnaissance
logsource:
  product: dns
detection:
  selection:
    query_type:
      - ANY
      - TXT
      - MX
  timeframe: 1h
  condition: selection | count(by=src_ip) > 100
fields:
  - src_ip
  - query
  - query_type
falsepositives:
  - DNS monitoring tools
  - Internal security scanning
level: medium
tags:
  - s3f.phase1
  - reconnaissance
```

---

## Phase 2: Pretexting Detection

### Detection Strategy

Pretexting involves **impersonation and deception**. Focus on:
- Domain spoofing and typosquatting
- Display name vs actual sender mismatches
- Newly registered domains
- Caller ID spoofing

### Rule 2.1: Domain Typosquatting

**Description:** Detect emails from domains similar to organization

**Splunk:**
```spl
index=email
| rex field=sender_domain "(?<domain_variant>.*)"
| eval org_domain="yourcompany.com"
| eval distance=levenshtein(domain_variant, org_domain)
| where distance <= 2 AND domain_variant != org_domain
| table _time, sender, recipient, subject, sender_domain, distance
| eval severity="high", s3f_phase="2.1", s3f_technique="Impersonation"
```

**Microsoft Sentinel (KQL):**
```kql
EmailEvents
| where TimeGenerated > ago(24h)
| extend SenderDomain = tostring(split(SenderFromAddress, "@")[1])
| extend OrgDomain = "yourcompany.com"
| extend Distance = damerau_levenshtein(SenderDomain, OrgDomain)
| where Distance <= 2 and SenderDomain != OrgDomain
| project TimeGenerated, SenderFromAddress, RecipientEmailAddress, Subject, SenderDomain, Distance
| extend S3F_Phase = "2.1", S3F_Technique = "Impersonation", Severity = "High"
```

**Tuning:**
- Maintain allowlist of known partner/vendor domains
- Adjust Levenshtein distance threshold
- Combine with sender reputation scores

---

### Rule 2.2: Display Name Mismatch

**Description:** Detect when email display name doesn't match sender address

**Splunk:**
```spl
index=email
| rex field=sender_display_name "(?<display_name>.*)"
| rex field=sender_email "(?<email_name>.*)@"
| eval name_match=if(lower(display_name)==lower(email_name), "match", "mismatch")
| where name_match="mismatch" AND sender_domain!="yourcompany.com"
| search display_name="*CEO*" OR display_name="*CFO*" OR display_name="*Executive*" OR display_name="*President*"
| eval severity="high", s3f_phase="2.2", s3f_technique="Authority_Figure"
```

**Elastic:**
```json
{
  "query": {
    "bool": {
      "must": [
        {
          "script": {
            "script": "doc['email.sender.display_name'].value.toLowerCase() != doc['email.sender.address'].value.split('@')[0].toLowerCase()"
          }
        },
        {
          "wildcard": { "email.sender.display_name": "*CEO*" }
        }
      ],
      "must_not": [
        { "term": { "email.sender.domain": "yourcompany.com" }}
      ]
    }
  }
}
```

**Tuning:**
- Common false positives: Legitimate marketing emails, automated systems
- Focus on high-value targets (executives, finance keywords)
- Combine with other indicators (urgency, financial requests)

---

### Rule 2.3: Newly Registered Domain

**Description:** Detect emails from recently registered domains

**Requires:** Domain age enrichment (WHOIS, DomainTools API)

**Splunk:**
```spl
index=email
| lookup domain_age_lookup sender_domain OUTPUT domain_age_days
| where domain_age_days < 30
| eval severity="medium", s3f_phase="2.5", s3f_technique="Vendor_Supplier"
```

**Microsoft Sentinel:**
```kql
let RecentDomains = externaldata(Domain: string, CreateDate: datetime)
[@"https://yourcompany.blob.core.windows.net/threatstorage/recent_domains.csv"]
with (format="csv");
EmailEvents
| where TimeGenerated > ago(24h)
| extend SenderDomain = tostring(split(SenderFromAddress, "@")[1])
| join kind=inner (RecentDomains) on $left.SenderDomain == $right.Domain
| where datetime_diff('day', now(), CreateDate) < 30
| extend S3F_Phase = "2.5", Severity = "Medium"
```

**Implementation Notes:**
- Requires external threat intel or WHOIS lookup
- High false positive rate (many legitimate new domains)
- Best combined with other pretexting indicators

---

## Phase 3: Initial Contact Detection

### Detection Strategy

Initial Contact is **the attack delivery**. Focus on:
- Phishing email characteristics
- Malicious attachments and links
- Credential harvesting attempts
- OAuth phishing

### Rule 3.1: Spear Phishing Email

**Description:** Multi-factor spear phishing detection

**Splunk:**
```spl
index=email
| eval has_attachment=if(attachment_count>0, 1, 0)
| eval has_link=if(url_count>0, 1, 0)
| eval is_external=if(sender_domain!="yourcompany.com", 1, 0)
| eval urgency_keywords=if(match(subject, "(?i)(urgent|immediate|action required|expire|suspend|verify|confirm)"), 1, 0)
| eval personalized=if(match(body, "(?i)(project|meeting|report|document|contract)"), 1, 0)
| eval risk_score = has_attachment + has_link + urgency_keywords + personalized
| where is_external=1 AND risk_score >= 3
| eval severity="high", s3f_phase="3.1", s3f_technique="Spear_Phishing"
```

**Microsoft Sentinel (Advanced):**
```kql
EmailEvents
| where TimeGenerated > ago(1h)
| extend IsExternal = iff(SenderFromDomain !in~ ("yourcompany.com"), 1, 0)
| extend HasAttachment = iff(AttachmentCount > 0, 1, 0)
| extend HasLink = iff(UrlCount > 0, 1, 0)
| extend UrgencyKeywords = iff(Subject has_any ("urgent", "immediate", "action required", "expire", "suspend", "verify"), 1, 0)
| extend Personalized = iff(Subject has_any ("project", "meeting", "report", "document", "contract"), 1, 0)
| extend RiskScore = HasAttachment + HasLink + UrgencyKeywords + Personalized
| where IsExternal == 1 and RiskScore >= 3
| extend S3F_Phase = "3.1", S3F_Technique = "Spear_Phishing", Severity = "High"
```

**Elastic (with NLP):**
```json
{
  "query": {
    "bool": {
      "must": [
        { "term": { "email.direction": "inbound" }},
        {
          "script": {
            "script": {
              "source": "int score = 0; if (doc['email.attachments'].size() > 0) score++; if (doc['email.links'].size() > 0) score++; if (params.urgency_pattern.matcher(doc['email.subject'].value).find()) score++; if (params.personalized_pattern.matcher(doc['email.body'].value).find()) score++; return score >= 3;",
              "params": {
                "urgency_pattern": "(?i)(urgent|immediate|action required|expire)",
                "personalized_pattern": "(?i)(project|meeting|report)"
              }
            }
          }
        }
      ]
    }
  }
}
```

**Tuning:**
- Adjust risk score threshold based on email volume
- Whitelist known marketing/transactional emails
- Combine with sender reputation
- Consider recipient role (executives = lower threshold)

---

### Rule 3.2: Credential Harvesting Page

**Description:** Detect clicks to credential phishing sites

**Splunk:**
```spl
index=proxy category="phishing" OR category="suspicious"
| join user [search index=email url=*]
| where urldecode(url) LIKE "%login%" OR urldecode(url) LIKE "%signin%" OR urldecode(url) LIKE "%verify%"
| eval severity="critical", s3f_phase="3.1", s3f_technique="Spear_Phishing"
```

**Microsoft Sentinel:**
```kql
let PhishingClicks = 
WebProxyLogs
| where TimeGenerated > ago(1h)
| where Category in~ ("Phishing", "Suspicious", "New Domain")
| where Url has_any ("login", "signin", "verify", "account", "update", "confirm");
EmailUrlInfo
| where TimeGenerated > ago(24h)
| join kind=inner (PhishingClicks) on $left.Url == $right.Url
| project TimeGenerated, UserPrincipalName, Url, Category, NetworkMessageId
| extend S3F_Phase = "3.1", Severity = "Critical"
```

**Response Actions:**
- Immediately disable user account
- Force password reset
- Alert SOC for investigation
- Quarantine related emails

---

### Rule 3.3: OAuth Phishing

**Description:** Detect suspicious OAuth consent grants

**Microsoft Sentinel (Azure AD):**
```kql
AuditLogs
| where TimeGenerated > ago(1h)
| where OperationName == "Consent to application"
| extend AppDisplayName = tostring(TargetResources[0].displayName)
| extend ConsentType = tostring(AdditionalDetails[0].value)
| extend Permissions = tostring(TargetResources[0].modifiedProperties)
| where Permissions has_any ("Mail.Read", "Mail.ReadWrite", "Files.Read", "Files.ReadWrite", "Contacts.Read")
| where AppDisplayName !in~ ("Microsoft Teams", "OneDrive", "SharePoint", "Outlook")
| extend S3F_Phase = "3.1", S3F_Technique = "OAuth_Phishing", Severity = "High"
```

**Splunk (O365):**
```spl
index=o365 Operation="Consent to application"
| spath path=AuditData.Target{}.ID output=AppID
| spath path=AuditData.ModifiedProperties{}.NewValue output=Permissions
| search Permissions="*Mail.Read*" OR Permissions="*Files.ReadWrite*"
| table _time, UserId, AppDisplayName, Permissions
| eval severity="high", s3f_phase="3.1"
```

**Tuning:**
- Maintain list of approved OAuth apps
- Alert on high-risk permissions (Mail, Files, Contacts)
- Consider app publisher reputation

---

## Phase 4: Trust Manipulation Detection

### Detection Strategy

Trust Manipulation is **subtle and behavioral**. Focus on:
- Unusual request patterns
- Approval workflow anomalies
- Communication pattern changes
- User behavior deviations

### Rule 4.1: Unusual Access Request

**Description:** Detect access requests outside normal patterns

**Requires:** UEBA or baseline analytics

**Splunk (with UEBA):**
```spl
| from datamodel:"Authentication"
| lookup user_baseline_access user OUTPUT avg_access_count, stddev_access_count
| eval zscore = (access_count - avg_access_count) / stddev_access_count
| where zscore > 3
| eval severity="medium", s3f_phase="4.1", s3f_technique="Scarcity_Urgency"
```

**Microsoft Sentinel (Behavioral):**
```kql
let Baseline = 
SigninLogs
| where TimeGenerated between (ago(30d) .. ago(1d))
| summarize AvgSignins = avg(SigninCount) by UserPrincipalName, bin(TimeGenerated, 1h);
SigninLogs
| where TimeGenerated > ago(1h)
| summarize CurrentSignins = count() by UserPrincipalName, bin(TimeGenerated, 1h)
| join kind=inner (Baseline) on UserPrincipalName
| where CurrentSignins > (AvgSignins * 3)
| extend S3F_Phase = "4.1", Anomaly_Type = "Access_Spike"
```

---

### Rule 4.2: Policy Override Attempts

**Description:** Detect approval workflow bypasses

**Splunk:**
```spl
index=workflow action="override" OR action="skip_approval"
| stats count by user, override_reason
| eval severity="high", s3f_phase="4.1", s3f_technique="Authority"
```

**Elastic:**
```json
{
  "query": {
    "bool": {
      "should": [
        { "term": { "workflow.action": "override" }},
        { "term": { "workflow.action": "skip_approval" }},
        { "match": { "workflow.reason": "urgent" }}
      ]
    }
  }
}
```

---

## Phase 5: Trust Exploitation Detection

### Detection Strategy

Trust Exploitation is **active compromise**. Focus on:
- Insider threat indicators
- Privilege abuse
- Data exfiltration
- Compromised accounts

### Rule 5.1: Insider Data Exfiltration

**Description:** Detect large-scale data access and exfiltration

**Splunk:**
```spl
index=dlp action="block" OR action="alert"
| stats sum(file_size) as total_bytes, dc(file_name) as unique_files by user
| where total_bytes > 1000000000 OR unique_files > 100
| eval severity="critical", s3f_phase="5.1", s3f_technique="Data_Exfiltration"
```

**Microsoft Sentinel:**
```kql
CloudAppEvents
| where TimeGenerated > ago(1h)
| where ActionType in~ ("FileUploaded", "FileCopied", "FileDownloaded")
| where Application in~ ("Box", "Dropbox", "Google Drive", "Personal OneDrive")
| summarize TotalBytes = sum(FileSize), UniqueFiles = dcount(FileName) by AccountObjectId
| where TotalBytes > 1000000000 or UniqueFiles > 100
| extend S3F_Phase = "5.1", S3F_Technique = "Insider_Threat", Severity = "Critical"
```

**Response:**
- Immediate account suspension
- Block upload destinations
- Preserve evidence
- Legal/HR notification

---

### Rule 5.2: Privilege Escalation

**Description:** Detect unauthorized privilege elevation

**Splunk:**
```spl
index=windows EventCode=4672 OR EventCode=4728 OR EventCode=4732
| stats count by Account_Name, Privilege_List
| where Privilege_List="*Admin*" OR Privilege_List="*SeDebugPrivilege*"
| eval severity="critical", s3f_phase="5.1", s3f_technique="Malicious_Insider"
```

**Elastic:**
```json
{
  "query": {
    "bool": {
      "must": [
        { "terms": { "event.code": ["4672", "4728", "4732", "4756"] }},
        { "wildcard": { "winlog.event_data.PrivilegeList": "*Admin*" }}
      ]
    }
  }
}
```

---

### Rule 5.3: After-Hours VPN Access

**Description:** Detect unusual remote access patterns

**Splunk:**
```spl
index=vpn action="connected"
| eval hour=strftime(_time, "%H")
| where (hour < 6 OR hour > 22)
| lookup user_baselines user OUTPUT typical_hours
| where hour NOT IN (typical_hours)
| eval severity="medium", s3f_phase="5.1"
```

**Microsoft Sentinel:**
```kql
SigninLogs
| where TimeGenerated > ago(1h)
| where AppDisplayName == "VPN" or NetworkLocationDetails contains "vpn"
| extend Hour = datetime_part("hour", TimeGenerated)
| where Hour < 6 or Hour > 22
| extend S3F_Phase = "5.1", Anomaly_Type = "After_Hours_Access"
```

---

## Phase 6: Weaponized Trust Detection

### Detection Strategy

Weaponized Trust is **large-scale abuse**. Focus on:
- Mass campaigns
- Deepfake detection
- BEC at scale
- Disinformation

### Rule 6.1: Deepfake Detection

**Description:** Detect synthetic media indicators

**Requires:** Specialized deepfake detection tools

**Conceptual Logic:**
```
IF media_type == "video" OR media_type == "audio":
    deepfake_score = analyze_media(file)
    IF deepfake_score > 0.8 AND content_type == "executive_communication":
        ALERT(severity="critical", s3f_phase="6.1")
```

**Integration Points:**
- Microsoft Video Authenticator
- Sensity AI
- Deeptrace
- Custom ML models

---

### Rule 6.2: Business Email Compromise (BEC) at Scale

**Description:** Detect coordinated BEC campaigns

**Splunk:**
```spl
index=email 
| search (subject="*payment*" OR subject="*invoice*" OR subject="*wire*" OR subject="*urgent*") 
    AND (sender_domain!="yourcompany.com")
    AND (recipient="finance@*" OR recipient="*payable*" OR recipient="*controller*")
| stats dc(recipient) as unique_targets, count by sender, sender_domain
| where unique_targets > 5 OR count > 10
| eval severity="critical", s3f_phase="6.6", s3f_technique="Weaponize_Trust"
```

**Microsoft Sentinel:**
```kql
EmailEvents
| where TimeGenerated > ago(24h)
| where Subject has_any ("payment", "invoice", "wire transfer", "urgent payment")
| where SenderFromDomain !in~ ("yourcompany.com")
| where RecipientEmailAddress has_any ("finance@", "payable", "controller", "accounting")
| summarize UniqueTargets = dcount(RecipientEmailAddress), TotalEmails = count() by SenderFromAddress, SenderFromDomain
| where UniqueTargets > 5 or TotalEmails > 10
| extend S3F_Phase = "6.6", S3F_Technique = "BEC_Campaign", Severity = "Critical"
```

---

### Rule 6.3: Brand Impersonation at Scale

**Description:** Detect coordinated brand abuse

**Requires:** External brand monitoring

**Splunk:**
```spl
index=brand_monitoring event_type="domain_registration" OR event_type="social_account_creation"
| search domain="*yourcompany*" OR account_name="*YourCompany*"
| where registered_domain != "yourcompany.com"
| stats count by registered_domain, registrant
| eval severity="high", s3f_phase="6.2", s3f_technique="Disinformation"
```

---

## Detection Tuning

### False Positive Reduction

**1. Whitelist Management**
```
Maintain whitelists for:
- Trusted partner domains
- Approved SaaS applications
- Known security testing teams
- Legitimate business processes
```

**2. Contextual Enrichment**
```
Enrich alerts with:
- User role and department
- Historical behavior patterns
- Business context (e.g., end-of-quarter financial activity)
- Geographic norms
```

**3. Adaptive Thresholds**
```
Adjust thresholds based on:
- Organizational size
- Industry norms
- Time of day/week
- Seasonal patterns
```

**4. Machine Learning Baselines**
```
Use ML for:
- Per-user behavioral baselines
- Department-level norms
- Communication pattern analysis
- Anomaly scoring
```

### Tuning Workflow

```
1. Deploy rule in "log only" mode
2. Collect 2+ weeks of alerts
3. Analyze false positive patterns
4. Add whitelist entries
5. Adjust thresholds
6. Enable alerting
7. Monitor precision/recall
8. Iterate monthly
```

### Metrics

**Detection Quality:**
- **Precision:** True Positives / (True Positives + False Positives)
- **Recall:** True Positives / (True Positives + False Negatives)
- **F1 Score:** 2 * (Precision * Recall) / (Precision + Recall)

**Target Metrics:**
- Precision > 70% (low false positive rate)
- Recall > 80% (catch most attacks)
- MTTD (Mean Time to Detect) < 1 hour

---

## Implementation Roadmap

### Phase 1: Foundation (Weeks 1-4)

**Objectives:**
- Establish data pipeline
- Deploy essential detections
- Baseline user behavior

**Tasks:**
1. **Week 1:** Data source inventory and gap analysis
2. **Week 2:** Configure log collection for critical sources
3. **Week 3:** Deploy Phase 2-3 detection rules (phishing, pretexting)
4. **Week 4:** Establish UEBA baselines

**Deliverables:**
- Email gateway logs in SIEM
- Auth logs with enrichment
- 5-10 core detection rules
- Initial false positive tuning

---

### Phase 2: Expansion (Weeks 5-8)

**Objectives:**
- Add behavioral detections
- Implement correlation rules
- Develop response playbooks

**Tasks:**
1. **Week 5:** Deploy Phase 4-5 rules (trust manipulation, exploitation)
2. **Week 6:** Implement multi-stage correlation
3. **Week 7:** Create automated response workflows
4. **Week 8:** Conduct detection validation exercises

**Deliverables:**
- Full S3F phase coverage
- Correlation rules for attack chains
- Automated containment actions
- Validated detection effectiveness

---

### Phase 3: Maturity (Weeks 9-12)

**Objectives:**
- Advanced analytics
- ML/AI integration
- Continuous improvement

**Tasks:**
1. **Week 9:** Integrate deepfake detection (if applicable)
2. **Week 10:** Deploy NLP for email analysis
3. **Week 11:** Implement threat hunting queries
4. **Week 12:** Establish detection metrics dashboard

**Deliverables:**
- Advanced detection capabilities
- Threat hunting program
- Detection metrics and KPIs
- Continuous tuning process

---

## Metrics & Validation

### Detection Coverage Matrix

| S3F Phase | Rule Count | Data Coverage | Tested | Production |
|-----------|-----------|---------------|--------|-----------|
| 1. Reconnaissance | 5 | ✓ Web, DNS, Email | ✓ | ✓ |
| 2. Pretexting | 8 | ✓ Email, Phone, Badge | ✓ | ✓ |
| 3. Initial Contact | 10 | ✓ Email, Endpoint, Proxy | ✓ | ✓ |
| 4. Manipulate Trust | 6 | △ UEBA, Email, HR | ✓ | △ |
| 5. Exploit Trust | 8 | ✓ DLP, PAM, Endpoint | ✓ | ✓ |
| 6. Weaponize Trust | 4 | △ Brand, Media, Email | △ | ✗ |

**Legend:** ✓ Complete | △ Partial | ✗ Not Started

---

### Validation Methods

**1. Purple Team Exercises**
- Simulate each S3F phase
- Measure detection rate
- Validate alert quality
- Test response procedures

**2. Historical Analysis**
- Replay past incidents
- Verify detections fire
- Calculate MTTD
- Identify gaps

**3. Synthetic Testing**
- Generate test events
- Validate alert triggers
- Check for false negatives
- Test edge cases

**4. Threat Intel Validation**
- Monitor real-world attacks
- Compare to S3F taxonomy
- Update detection logic
- Close coverage gaps

---

## References

### Platform Documentation

- **Splunk:** [Security Content](https://research.splunk.com/)
- **Elastic:** [Detection Rules](https://www.elastic.co/guide/en/security/current/detection-engine-overview.html)
- **Microsoft Sentinel:** [Detection Gallery](https://github.com/Azure/Azure-Sentinel)
- **QRadar:** [Use Case Manager](https://www.ibm.com/docs/en/qsip/7.4?topic=qradar-use-case-manager)
- **Sigma:** [Rules Repository](https://github.com/SigmaHQ/sigma)

### S3F Resources

- [S3F_TTPs.md](S3F_TTPs.md) - Full technique taxonomy
- [S3F_SOC_Playbook.md](S3F_SOC_Playbook.md) - Response procedures
- [S3F_MITRE_ATTCK_CSIRT_Reference.md](S3F_MITRE_ATTCK_CSIRT_Reference.md) - ATT&CK mapping

### Detection Engineering

- [Palantir ADS Framework](https://github.com/palantir/alerting-detection-strategy-framework)
- [MITRE Cyber Analytics Repository](https://car.mitre.org/)
- [Sigma HQ](https://github.com/SigmaHQ/sigma)

---

**Document Version:** 1.0  
**Last Updated:** 2026-07-03  
**Maintained By:** Detection Engineering Team  
**Contact:** cbkittner@gmail.com

**License:** GNU General Public License v3.0 (GPL-3.0)
