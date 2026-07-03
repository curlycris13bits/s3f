# Changelog

All notable changes to the Social 3ngineering Framework (S3F) will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Detection engineering guide with SIEM-specific rules
- Additional training simulation scenarios
- Detection rule templates for major SIEM platforms
- CONTRIBUTING.md with comprehensive contribution guidelines
- This CHANGELOG.md for version tracking

## [1.0.0] - 2026-07-03

### Added
- **S3F_SOC_Playbook.md** - Comprehensive Security Operations Center playbook with:
  - Detection indicators for all 6 S3F phases (technical & behavioral)
  - Response procedures with specific timelines
  - SIEM integration guidance with sample correlation rules
  - Detection queries for Splunk and Elastic
  - Escalation matrix with severity levels
  - Notification matrix (SOC, CISO, Legal, HR, PR, Law Enforcement)
  - Incident response workflow
  - Integration with MITRE ATT&CK
  - Metrics and KPIs for program measurement
  - Training recommendations and maintenance schedule

### Fixed
- **Critical Numbering Inconsistencies:**
  - Fixed Physical Surveillance (1.6) sub-techniques from 1.7.x to 1.6.x
  - Resolved duplicate "Reciprocity" sections (renamed 4.4 to "Liking & Rapport")
  - Fixed missing technique 5.4 (renumbered 5.5→5.4, 5.6→5.5)
  - Fixed missing technique 6.5 (renumbered 6.6→6.5)
  - Fixed formatting inconsistency in 3.1.7 (italics → bold)
  - Added missing 4.1.7 "Financial Penalty Threat" to ASCII file
  - Added missing 4.2.7 "Organizational Hierarchy" to both files

- **Completed Missing Sub-techniques:**
  - 4.4 "Liking & Rapport" completed to 7 sub-techniques
  - 4.6 "Reciprocity" completed to 7 sub-techniques
  - 5.4 "Unsecured Systems" completed to 7 sub-techniques
  - 5.5 "Physical Access" completed to 7 sub-techniques
  - 6.4 "Psychological Manipulation" completed to 7 sub-techniques
  - 6.5 "Trust as a Vulnerability" completed to 7 sub-techniques

- **File Synchronization:**
  - Ensured ASCII_S3F and S3F_TTPs.md are perfectly aligned
  - Fixed all mixed numbering issues
  - Corrected hierarchical structure throughout

### Changed
- Renamed technique 4.4 from "Reciprocity" to "Liking & Rapport" for semantic accuracy
- Enhanced sub-technique descriptions for clarity
- Improved consistency across all documentation files

## [0.9.0] - 2026-01-18 (Pre-standardization)

### Added
- Initial S3F framework structure with 6 tactical phases
- S3F_TTPs.md with comprehensive technique taxonomy
- ASCII_S3F visual hierarchy representation
- S3F_MITRE_ATTCK_CSIRT_Reference.md for ATT&CK alignment
- S3F_Training_Simulation_Template.md for tabletop exercises
- S3F Overlay Visual.png diagram
- README.md with framework overview
- LICENSE (GNU GPL v3.0)

### Known Issues (Fixed in 1.0.0)
- Physical Surveillance (1.6) incorrectly numbered with 1.7.x sub-techniques
- Duplicate "Reciprocity" sections (4.4 and 4.6)
- Missing techniques 5.4 and 6.5 (numbering gaps)
- S3F_SOC_Playbook.md referenced but contained only placeholder content
- Inconsistent sub-technique counts across techniques
- Minor formatting and synchronization issues between files

---

## Version History Summary

| Version | Date | Highlights |
|---------|------|------------|
| 1.0.0 | 2026-07-03 | Production-ready release: Fixed all numbering issues, added SOC Playbook |
| 0.9.0 | 2026-01-18 | Initial framework release with 200+ techniques |

---

## Upgrade Notes

### Upgrading from 0.9.0 to 1.0.0

**Breaking Changes:**
- Technique 4.4 renamed from "Reciprocity" to "Liking & Rapport"
- Technique 5.5 "Unsecured Systems" renumbered to 5.4
- Technique 5.6 "Physical Access" renumbered to 5.5
- Technique 6.6 "Trust as a Vulnerability" renumbered to 6.5
- Physical Surveillance sub-techniques renumbered from 1.7.x to 1.6.x

**Action Required:**
If you have integrated S3F technique IDs into your tools or documentation:
1. Update technique 4.4 references to "Liking & Rapport" (not "Reciprocity")
2. Renumber 5.5 → 5.4 and 5.6 → 5.5
3. Renumber 6.6 → 6.5
4. Update 1.7.1-1.7.7 → 1.6.1-1.6.7

**New Features:**
- S3F_SOC_Playbook.md is now fully implemented (previously placeholder)
- All techniques now have consistent 7 sub-techniques
- SIEM integration guidance available
- Detection queries and correlation rules provided

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for details on how to contribute to S3F.

---

## Semantic Versioning Guide

This project follows [Semantic Versioning](https://semver.org/):

- **MAJOR version** (X.0.0): Incompatible changes (technique renumbering, major restructuring)
- **MINOR version** (1.X.0): New functionality in a backwards-compatible manner (new techniques, new files)
- **PATCH version** (1.0.X): Backwards-compatible bug fixes (typos, clarifications, minor corrections)

### Examples:
- Adding a new technique category → MINOR version bump
- Renumbering existing techniques → MAJOR version bump
- Fixing typos or descriptions → PATCH version bump
- Adding detection rules or playbooks → MINOR version bump

---

## Release Process

1. **Development** - Changes accumulate in feature branches
2. **Integration** - Features merged to main branch
3. **Version Bump** - Update version numbers in:
   - CHANGELOG.md
   - README.md (if version displayed)
   - Documentation headers
4. **Tag Release** - Create git tag: `git tag -a vX.Y.Z -m "Release X.Y.Z"`
5. **Publish** - Push tag: `git push origin vX.Y.Z`
6. **Announce** - Update GitHub releases page

---

## Maintenance

This CHANGELOG is maintained by the S3F project team and updated with each release.

**Update Frequency:**
- Unreleased section: Updated with each significant change
- Version sections: Created upon release tagging
- Historical entries: Backfilled from git history and documentation

**Responsibilities:**
- Maintainers: Ensure CHANGELOG is updated before each release
- Contributors: Mention changes in PR descriptions (maintainers will update CHANGELOG)

---

**Current Version:** 1.0.0  
**Last Updated:** 2026-07-03  
**Maintained By:** S3F Project Team  
**Contact:** cbkittner@gmail.com
