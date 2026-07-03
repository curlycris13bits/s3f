# 🧠 Social 3ngineering Framework (S3F)

Welcome to the Social 3ngineering Framework (S3F), a behavioral cybersecurity framework focused on the human factor in cybersecurity, specifically, on trust manipulation tactics used in social engineering attacks.

---

## 📚 Available Resources

### Core Framework

| Resource Type | File | Description |
|---------------|------|-------------|
| **Framework Taxonomy** | [S3F_TTPs.md](S3F_TTPs.md) | Complete Social 3ngineering TTPs hierarchy with 200+ techniques |
| **Visual Hierarchy** | [ASCII_S3F](ASCII_S3F) | ASCII tree representation of all S3F tactics and techniques |
| **MITRE Mapping** | [S3F_MITRE_ATTCK_CSIRT_Reference.md](S3F_MITRE_ATTCK_CSIRT_Reference.md) | ATT&CK-aligned tactics for technical teams |

### Operational Guides

| Resource Type | File | Description |
|---------------|------|-------------|
| **SOC Playbook** | [S3F_SOC_Playbook.md](S3F_SOC_Playbook.md) | Complete incident response procedures for all 6 phases |
| **Detection Engineering** | [S3F_Detection_Engineering_Guide.md](S3F_Detection_Engineering_Guide.md) | Platform-specific SIEM rules and detection logic |
| **Detection Rules** | [detection-rules/](detection-rules/) | Ready-to-deploy rules for Splunk, Elastic, Sentinel, Sigma |

### Training & Simulation

| Resource Type | File | Description |
|---------------|------|-------------|
| **Training Scenarios** | [S3F_Training_Scenarios.md](S3F_Training_Scenarios.md) | 3 realistic attack scenarios for tabletop exercises |
| **Simulation Template** | [S3F_Training_Simulation_Template.md](S3F_Training_Simulation_Template.md) | Interactive training scenario template |

### Community

| Resource Type | File | Description |
|---------------|------|-------------|
| **Contributing Guide** | [CONTRIBUTING.md](CONTRIBUTING.md) | How to contribute to S3F |
| **Changelog** | [CHANGELOG.md](CHANGELOG.md) | Version history and updates |
| **License** | [LICENSE](LICENSE) | GNU GPL v3.0 |

<img src="S3F%20Overlay%20Visual.png" style="margin-left:20px;" width="700">


## 🧠 About S3F

[View the full S3F ASCII Tactics Tree](ASCII_S3F)

S3F breaks down the various phases of Trust Cycle similarly to MITRE ATT&CK, Lockheed Martin's Cyber Kill Chain, and others, in the following Tactics:
- Reconnaissance
- Pretexting & Deception
- Initial Contact
- Manipulate Trust
- Exploit Trust
- Weaponize Trust

Each Tactic consists of a number of Techniques, and Sub-Techniques that can be found on the TTP Dictionary.

---

## 🚀 Quick Start

### For Security Teams
1. **Understand the Framework:** Read [S3F_TTPs.md](S3F_TTPs.md)
2. **Implement Detection:** Deploy rules from [detection-rules/](detection-rules/)
3. **Build Response:** Use [S3F_SOC_Playbook.md](S3F_SOC_Playbook.md)
4. **Train Your Team:** Run scenarios from [S3F_Training_Scenarios.md](S3F_Training_Scenarios.md)

### For Detection Engineers
1. Review [S3F_Detection_Engineering_Guide.md](S3F_Detection_Engineering_Guide.md)
2. Choose your platform: Splunk, Elastic, Sentinel, or Sigma
3. Customize rules for your environment
4. Test with purple team exercises

### For Trainers
1. Use [S3F_Training_Scenarios.md](S3F_Training_Scenarios.md) for tabletop exercises
2. Adapt scenarios to your organization
3. Run simulations (with proper authorization)
4. Measure effectiveness and iterate

---

## 🤝 Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for:
- How to submit new techniques
- Detection rule contributions
- Training scenario submissions
- Documentation improvements

---

## 📖 Documentation

- **[S3F_TTPs.md](S3F_TTPs.md)** - Complete technique taxonomy
- **[S3F_SOC_Playbook.md](S3F_SOC_Playbook.md)** - Operational response procedures
- **[S3F_Detection_Engineering_Guide.md](S3F_Detection_Engineering_Guide.md)** - SIEM implementation guide
- **[CHANGELOG.md](CHANGELOG.md)** - Version history and updates

---

## 🔒 License

This project is licensed under the GNU General Public License v3.0 (GPL-3.0). See [LICENSE](LICENSE) for details.

---

📬 **Maintained by** [curlycris13bits](https://github.com/curlycris13bits) & [mshelton](https://github.com/mshelton)  
🔗 **Fork and contribute** your playbooks, simulations, or tools!  
📧 **Contact:** cbkittner@gmail.com

**Version:** 1.0.0 | **Last Updated:** 2026-07-03
