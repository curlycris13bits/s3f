# Contributing to S3F

Thank you for your interest in contributing to the Social 3ngineering Framework (S3F)! This framework thrives on community contributions from security professionals, researchers, and practitioners who understand the human element of cybersecurity.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Contribution Types](#contribution-types)
- [Submission Process](#submission-process)
- [Style Guidelines](#style-guidelines)
- [Review Process](#review-process)
- [Recognition](#recognition)

---

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive environment for all contributors, regardless of background, experience level, gender identity, sexual orientation, disability, personal appearance, race, ethnicity, age, religion, or nationality.

### Expected Behavior

- Use welcoming and inclusive language
- Respect differing viewpoints and experiences
- Accept constructive criticism gracefully
- Focus on what's best for the community and the framework
- Show empathy toward other community members

### Unacceptable Behavior

- Harassment, trolling, or insulting/derogatory comments
- Public or private attacks on individuals
- Publishing others' private information without permission
- Other conduct that would be inappropriate in a professional setting

### Enforcement

Instances of unacceptable behavior may be reported to the project maintainers at cbkittner@gmail.com. All complaints will be reviewed and investigated promptly and fairly.

---

## How Can I Contribute?

### Reporting Gaps or Inaccuracies

If you notice missing techniques, incorrect descriptions, or outdated information:

1. **Check existing issues** to see if it's already reported
2. **Open a new issue** with:
   - Clear title describing the gap
   - Affected file and line number
   - Proposed correction or addition
   - Supporting references or real-world examples

### Suggesting New Techniques

Social engineering evolves constantly. If you've observed a new technique:

1. **Verify it's not already documented** - Check S3F_TTPs.md thoroughly
2. **Open an issue** titled "New Technique: [Name]" with:
   - Technique name and description
   - Which S3F phase it belongs to (1-6)
   - Real-world examples or case studies
   - Detection indicators
   - References to documented attacks or research

### Improving Documentation

Documentation improvements are always welcome:

- Clarifying existing descriptions
- Adding practical examples
- Fixing typos or formatting
- Improving readability
- Translating to other languages (future)

### Contributing Detection Rules

Help SOC teams by contributing:

- SIEM correlation rules
- Detection queries
- Response playbooks
- Investigation procedures
- Integration guides for security tools

### Sharing Training Materials

Contribute:

- Tabletop exercise scenarios
- Phishing simulation templates
- Security awareness training content
- Case studies mapped to S3F
- Red team/purple team scenarios

---

## Contribution Types

### 1. Technique Additions

**What:** Adding new social engineering techniques or sub-techniques to the S3F taxonomy.

**Requirements:**
- Must fit within existing S3F phase structure (Phases 1-6)
- Must have clear, concise description
- Should include real-world examples or references
- Must follow existing numbering scheme
- Should maintain 7 sub-techniques per technique (ideal, not required)

**Example:**
```markdown
### X.X New Technique Name

* **X.X.1 Sub-technique Name:** Clear description of the sub-technique.
* **X.X.2 Another Sub-technique:** Description with specific tactics.
```

### 2. Playbook Contributions

**What:** Adding or improving SOC/CSIRT response procedures.

**Requirements:**
- Must align with S3F phases
- Include specific detection indicators
- Provide actionable response steps
- Specify log sources and tools
- Include escalation criteria

**Files to contribute to:**
- `S3F_SOC_Playbook.md` - SOC operational procedures
- New playbook files for specific scenarios

### 3. Detection Rules

**What:** SIEM-specific detection rules and queries.

**Requirements:**
- Must target specific S3F technique(s)
- Should be tested in target SIEM platform
- Include clear description of what it detects
- Specify false positive considerations
- Provide tuning guidance

**Supported formats:**
- Splunk SPL
- Elastic Query DSL
- Microsoft Sentinel KQL
- Sigma rules (universal format)
- QRadar AQL
- Chronicle YARA-L

### 4. Training Scenarios

**What:** Realistic social engineering simulation scenarios.

**Requirements:**
- Cover multiple S3F phases
- Include facilitator guidance
- Provide participant materials
- Specify learning objectives
- Include debrief questions

**Template:** See `S3F_Training_Simulation_Template.md`

### 5. Case Studies

**What:** Real-world attack analysis mapped to S3F.

**Requirements:**
- Public attacks only (disclosed breaches, documented campaigns)
- Map techniques to specific S3F IDs
- Include timeline and attack chain
- Cite authoritative sources
- Extract lessons learned

### 6. Tool Integration

**What:** Guides for integrating S3F into security tools.

**Requirements:**
- Step-by-step integration instructions
- Screenshots or examples
- Configuration files (sanitized)
- Testing/validation procedures
- Troubleshooting guidance

---

## Submission Process

### 1. Fork the Repository

```bash
git clone https://github.com/curlycris13bits/s3f.git
cd s3f
git checkout -b feature/your-contribution-name
```

### 2. Make Your Changes

- Follow the [Style Guidelines](#style-guidelines)
- Test your changes (if applicable)
- Ensure all files use consistent formatting
- Update relevant documentation

### 3. Commit Your Changes

Use clear, descriptive commit messages:

```bash
git add <modified-files>
git commit -m "Add technique 2.8: Deepfake Voice Impersonation

- Add 7 sub-techniques for deepfake voice attacks
- Update S3F_TTPs.md and ASCII_S3F
- Include detection indicators in SOC playbook"
```

**Commit message format:**
- First line: Brief summary (50 chars or less)
- Blank line
- Detailed description with bullet points
- Reference issue numbers if applicable

### 4. Push to Your Fork

```bash
git push origin feature/your-contribution-name
```

### 5. Create a Pull Request

1. Go to the [S3F repository](https://github.com/curlycris13bits/s3f)
2. Click "New Pull Request"
3. Select your fork and branch
4. Fill out the PR template:
   - **Title:** Clear, concise description
   - **Description:** What changed and why
   - **Type:** Technique addition, documentation, detection rule, etc.
   - **Testing:** How you validated the changes
   - **Related Issues:** Link any related issues

### 6. Respond to Feedback

Maintainers will review your PR and may request changes:

- Be responsive to feedback
- Make requested changes promptly
- Ask questions if anything is unclear
- Be patient - reviews take time

---

## Style Guidelines

### Markdown Formatting

**Headings:**
```markdown
# Top-level heading (file title only)
## Major sections
### Sub-sections
#### Technique names
```

**Lists:**
- Use `*` for unordered lists
- Use `1.` for ordered lists
- Indent sub-items with 4 spaces
- Keep list items concise

**Emphasis:**
- Use `**bold**` for technique IDs and emphasis
- Use `*italics*` sparingly
- Use `code blocks` for technical terms, IDs, commands

### Technique Numbering

**Format:** `X.Y.Z`
- `X` = Phase (1-6)
- `Y` = Technique within phase (1-N)
- `Z` = Sub-technique (1-7 ideally)

**Example:**
```markdown
### 2.3 Technical Support

* **2.3.1 Password Reset Scam:** Description here.
* **2.3.2 Software Installation Scam:** Description here.
```

**Rules:**
- Maintain sequential numbering
- Update both `S3F_TTPs.md` AND `ASCII_S3F` files
- Preserve alignment in ASCII tree structure
- Aim for 7 sub-techniques per technique (for consistency)

### Writing Style

**Technique Descriptions:**
- Start with a verb or action word
- Be concise but specific
- Focus on the "what" not the "why"
- Use present tense
- Avoid jargon unless necessary

**Good:**
```markdown
* **3.1.2 Personalized Content:** Tailoring phishing messages using target-specific information.
```

**Avoid:**
```markdown
* **3.1.2 Personalized Content:** This is when attackers might try to use personal information that they found during reconnaissance to make their phishing emails seem more legitimate and trustworthy.
```

**Detection Indicators:**
- Be specific and measurable
- Include both technical and behavioral indicators
- Reference log sources
- Provide concrete examples

**Response Procedures:**
- Use numbered steps
- Specify timelines
- Include decision points
- Be actionable

### File-Specific Guidelines

**S3F_TTPs.md:**
- Maintain existing structure
- Use consistent formatting
- Keep descriptions concise (1-2 sentences)
- Cross-reference related techniques when helpful

**ASCII_S3F:**
- Preserve tree structure alignment
- Use exact spacing (spaces, not tabs)
- Test visual rendering after changes
- Ensure consistency with S3F_TTPs.md

**S3F_SOC_Playbook.md:**
- Include specific log sources
- Provide timeline estimates
- Specify escalation criteria
- Add SIEM query examples when possible

**Detection Rules:**
- Include rule header with metadata
- Comment complex logic
- Specify tuning parameters
- Test on sample data
- Document false positive scenarios

---

## Review Process

### Review Criteria

Contributions are evaluated based on:

1. **Accuracy** - Is the information correct and well-researched?
2. **Relevance** - Does it fit within the S3F framework?
3. **Quality** - Is it well-written and clear?
4. **Completeness** - Are all required elements included?
5. **Consistency** - Does it match existing style and format?
6. **Value** - Does it meaningfully improve the framework?

### Review Timeline

- **Initial Review:** Within 7 days
- **Feedback Response:** Please respond within 14 days
- **Final Decision:** Within 7 days of last update
- **Merge:** Once approved and all checks pass

### What Happens After Approval?

1. Maintainer merges your PR
2. Changes appear in main branch
3. Your contribution is credited in commit history
4. You're added to contributors list (if significant contribution)
5. Framework version may be bumped in CHANGELOG.md

### If Changes Are Requested

Don't be discouraged! Common requests include:

- Formatting adjustments
- Additional detail or clarification
- Numbering corrections
- Style consistency fixes
- Adding missing elements (examples, references)

Make the requested changes and push to your branch - the PR will update automatically.

---

## Recognition

### Contributors

All contributors are recognized in:

- Git commit history (with Co-Authored-By tags)
- Future contributors section (for significant contributions)
- CHANGELOG.md entries for version releases

### Significant Contributions

Contributors who make substantial impacts receive:

- Named recognition in project documentation
- Invitation to maintainer discussions
- Potential co-maintainer status for sustained contributions

**What qualifies as significant?**
- Adding entire new technique categories
- Developing comprehensive playbooks or guides
- Creating extensive detection rule sets
- Multiple high-quality contributions over time
- Translating framework to other languages
- Building community tools or integrations

---

## Questions or Need Help?

### Getting Help

- **General Questions:** Open a GitHub Discussion
- **Specific Issues:** Open a GitHub Issue
- **Private Concerns:** Email maintainers at cbkittner@gmail.com

### Resources

- [README.md](README.md) - Framework overview
- [S3F_TTPs.md](S3F_TTPs.md) - Complete technique taxonomy
- [S3F_SOC_Playbook.md](S3F_SOC_Playbook.md) - Operational procedures
- [S3F_Training_Simulation_Template.md](S3F_Training_Simulation_Template.md) - Training example

### Communication Channels

- **GitHub Issues:** Bug reports, feature requests, technique suggestions
- **GitHub Discussions:** General questions, ideas, community interaction
- **Pull Requests:** Code/content contributions

---

## License

By contributing to S3F, you agree that your contributions will be licensed under the GNU General Public License v3.0 (GPL-3.0), the same license as the project.

Your contributions must be your own work or properly attributed work you have the right to contribute under GPL-3.0.

---

## Thank You!

The S3F framework exists to help organizations defend against the human element of cyber attacks. Every contribution - no matter how small - helps security teams worldwide better understand and combat social engineering.

Your expertise and experience make this framework better for everyone. Thank you for contributing!

---

**Maintainers:**
- [curlcris13bits](https://github.com/curlycris13bits) - cbkittner@gmail.com
- [mshelton](https://github.com/mshelton)

**Last Updated:** 2026-07-03  
**Version:** 1.0
