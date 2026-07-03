# S3F Detection Rules

This directory contains ready-to-deploy detection rules for identifying social engineering attacks mapped to the S3F framework.

## Directory Structure

```
detection-rules/
├── README.md (this file)
├── splunk/ - Splunk Enterprise Security rules
├── elastic/ - Elastic Security detection rules
├── sentinel/ - Microsoft Sentinel KQL queries
└── sigma/ - Sigma universal rules (convert to any SIEM)
```

## Usage

### Splunk
1. Copy `.spl` files to your Splunk search app
2. Create saved searches/correlation searches
3. Adjust index names and field mappings
4. Set appropriate alert actions

### Elastic
1. Import detection rules via Kibana Security UI
2. Or use Detection Rules API
3. Adjust index patterns and field names
4. Configure alert actions

### Microsoft Sentinel
1. Copy KQL queries to Analytics Rules
2. Adjust table names for your workspace
3. Set severity and alert grouping
4. Configure automation playbooks

### Sigma
1. Convert to your SIEM format using sigmac:
   ```bash
   sigmac -t splunk rule.yml
   sigmac -t elastalert rule.yml
   sigmac -t sentinel rule.yml
   ```
2. Deploy converted rules to your platform

## Rule Naming Convention

```
s3f_[phase]_[technique]_[platform].[ext]
```

**Examples:**
- `s3f_phase2_pretexting_domain_spoof.spl` (Splunk)
- `s3f_phase3_phishing_detection.ndjson` (Elastic)
- `s3f_phase5_insider_exfiltration.kql` (Sentinel)
- `s3f_phase2_bec.yml` (Sigma)

## Rule Metadata

All rules include:
- **S3F Phase:** Which attack phase (1-6)
- **S3F Technique:** Specific technique ID
- **Severity:** Low, Medium, High, Critical
- **MITRE ATT&CK:** Corresponding ATT&CK technique
- **False Positives:** Known FP scenarios
- **Tuning:** Guidance for customization

## Quick Start

### High-Priority Rules (Deploy First)

1. **Phase 2:** Domain Spoofing / Typosquatting
2. **Phase 3:** Spear Phishing Detection
3. **Phase 3:** Credential Harvesting
4. **Phase 5:** Insider Data Exfiltration
5. **Phase 6:** BEC Detection

See `QUICK_START_RULES.md` for minimal viable detection coverage.

## Testing

Before deploying to production:

1. **Test Mode:** Deploy in "log only" mode
2. **Baseline:** Collect 1-2 weeks of alerts
3. **Tune:** Adjust thresholds and whitelists
4. **Validate:** Purple team testing
5. **Production:** Enable alerting

## Support

For issues or questions:
- GitHub Issues: https://github.com/curlycris13bits/s3f/issues
- Email: cbkittner@gmail.com

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines on submitting new detection rules.

## License

GNU General Public License v3.0 (GPL-3.0)
