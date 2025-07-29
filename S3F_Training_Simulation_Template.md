# 🧠 Interactive Simulation Template: Social Engineering Incident (S3F-Based)

## 🎯 Scenario Overview
**Title**: “The Job Offer That Wasn’t”  
**Objective**: Simulate a multi-phase social engineering attack that traverses multiple S3F phases.

---

## 🕵️ Phase 1: Reconnaissance

**Clue for Players**:
> You notice that the attacker has commented on your public GitHub repo, complimenting your infrastructure skills.

**Facilitator Guide**:
- Ask: What might the adversary have learned?
- S3F Phase: `Reconnaissance`

---

## 🎭 Phase 2: Pretexting & Deception

**Clue for Players**:
> You receive a LinkedIn message claiming to be from a recruiter looking to hire a “cloud DevOps engineer.”

**Facilitator Guide**:
- Ask: What indicators suggest this might be a pretext?
- Provide an email screenshot with slight domain spoofing
- S3F Phase: `Pretexting & Deception`

---

## 📬 Phase 3: Initial Contact

**Clue for Players**:
> The “recruiter” asks to schedule a quick Zoom chat. Nothing odd on the surface.

**Facilitator Guide**:
- Introduce benign but persistent contact
- Note the lack of company domain validation
- S3F Phase: `Initial Contact`

---

## 🧠 Phase 4: Manipulate Trust

**Clue for Players**:
> The attacker mirrors your language, references your alma mater, and uses urgency to pressure you into sending credentials to “speed up HR onboarding.”

**Facilitator Guide**:
- Watch for flattery, urgency, mirroring
- S3F Phase: `Manipulate Trust`

---

## 🧨 Phase 5: Exploit Trust

**Clue for Players**:
> The target sends over a resume database, and the attacker pivots into internal comms channels.

**Facilitator Guide**:
- Highlight privilege abuse or lateral movement
- S3F Phase: `Exploit Trust`

---

## 🕳️ Phase 6: Weaponize Trust

**Clue for Players**:
> Colleagues report strange messages from your Slack, asking for access to a Git repo.

**Facilitator Guide**:
- Highlight impersonation using previously trusted identity
- S3F Phase: `Weaponize Trust`

---

## 🧩 Debrief Questions
- At what point should the user have “Paused, Protected, Verified”?
- Which emotional manipulation techniques were used?
- How can this scenario be integrated into detection logic?

---

Facilitator Note: Use artifacts (screenshots, log events, Slack messages) to increase realism.