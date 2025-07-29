# MITRE ATT&CK-Aligned View of the Social 3ngineering Framework (S3F)

This resource maps each phase of the Social 3ngineering Framework to corresponding MITRE ATT&CK Tactics and Techniques for CSIRTs familiar with threat modeling and detection engineering.

---

## 🔍 Reconnaissance → [TA0043: Reconnaissance]
- **T1593**: Search Open Websites / Domains (e.g. LinkedIn, GitHub)
- **T1595**: Active Scanning
- **T1589**: Gather Victim Identity Information

## 🎭 Pretexting & Deception → [TA0001: Initial Access] + [TA0011: Command & Control]
- **T1566.001**: Spearphishing via Email (with pretext)
- **T1585.001**: Spoofed Profiles (LinkedIn, HR)
- **T1071.001**: Application Layer Protocol: Web (used in social platform abuse)

## 📬 Initial Contact → [TA0001: Initial Access]
- **T1566.002**: Link delivered via benign email or calendar invite
- **T1204.001**: User Execution via Interaction
- **T1129**: Shared web links with social lure

## 🧠 Manipulate Trust → [TA0009: Collection] + [TA0006: Credential Access]
- **T1110.003**: Password Spraying (exploits lowered guard)
- **T1556.003**: Web Credential Manipulation
- **T1189**: Drive-by Compromise with benign initial content

## 🧨 Exploit Trust → [TA0006: Credential Access] + [TA0008: Lateral Movement]
- **T1550.001**: Application Access Token Abuse
- **T1021.001**: Remote Services (SMB, SSH) via trust-based auth
- **T1484.001**: Domain Trust Abuse

## 🕳️ Weaponize Trust → [TA0011: Command & Control] + [TA0040: Impact]
- **T1105**: Ingress Tool Transfer over trusted channels
- **T1567.002**: Exfiltration over Cloud Services
- **T1485**: Data Destruction masked as legitimate activity

---

## 🧩 Usage for CSIRT:
- Apply this table during log triage and playbook development
- Integrate as a trust overlay on ATT&CK Navigator
- Align phase-to-technique mapping in detection dashboards

Maintainer: cbkittner@gmail.com
