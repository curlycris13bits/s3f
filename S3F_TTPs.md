# S3F TTP Hierarchy

This document outlines a Threat Intelligence Platform (TIP) hierarchy based on Tactics, Techniques, and Procedures (TTPs). It’s designed to provide a structured view of adversary behavior.

## 1. Tactic

*   **Definition:** A high-level objective an attacker aims to achieve during a campaign.

### 1.1 Reconnaissance

*   **Purpose:** Gathering information about the target organization and its environment.
    *   **1.1.1 Google Dorking:** Using advanced search operators in Google to uncover sensitive data.
    *   **1.1.2 Social Media Monitoring:** Tracking individuals and organizations on social media platforms for intelligence gathering.
    *   **1.1.3 Public Records Search:** Accessing publicly available records (property, legal filings, etc.).
    *   **1.1.4 Website Analysis:** Examining website architecture, technologies used, and potential vulnerabilities.
    *   **1.1.5 Domain Name Lookups:** Investigating domain registration information and associated contacts.
    *   **1.1.6 News and Media Monitoring:** Tracking news articles and media coverage for relevant events or targets.
    *   **1.1.7 Geolocation Analysis:** Determining the physical location of individuals or assets.

### 1.2 Dumpster Diving

*   **Purpose:** Retrieving discarded materials containing sensitive information.
    *   **1.2.1 Cyber Hygiene Exploitation:** Leveraging poor cyber hygiene practices (e.g., leaving documents in trash).
    *   **1.2.2 Document Shredding Backdoor:**  Exploiting poorly shredded documents to recover data.
    *   **1.2.3 Data Recovery from Discarded Media:** Attempting to retrieve data from damaged or discarded storage media.
    *   **1.2.4 Information Gathering from Discarded Items:** Searching through trash for clues and information.
    *   **1.2.5 Physical Waste Analysis (feces, urine, etc):**  (Note: This is a highly specialized and often difficult technique).
    *   **1.2.6 Discarded Hardware Exploitation:** Extracting data from obsolete or discarded computer hardware.
    *   **1.2.7 Trash Bag Analysis:** Examining trash bags for physical evidence of activity.

### 1.3 Social Media Profiling

*   **Purpose:**  Gathering information about individuals through their social media presence.
    *   **1.3.1 Emotional Vulnerability Mapping:** Identifying emotional triggers and vulnerabilities in targets.
    *   **1.3.2 Interest and Hobby Identification:** Determining a target's interests, hobbies, and affiliations.
    *   **1.3.3 Relationship Mapping:**  Analyzing social connections to understand relationships and potential access points.
    *   **1.3.4 Location Tracking:** Monitoring a target’s location through social media posts.
    *   **1.3.5 Professional Network Analysis:** Examining LinkedIn profiles and other professional networks.
    *   **1.3.6 Behavioral Pattern Recognition:** Identifying patterns in a target's online behavior.
    *   **1.3.7 Sentiment Analysis:**  Analyzing the sentiment expressed by a target on social media.

### 1.4 Data Brokers

*   **Purpose:** Purchasing information from third-party data brokers.
    *   **1.4.1 Stolen Credentials:** Obtaining compromised usernames and passwords.
    *   **1.4.2 Personal Information Purchase:** Buying contact details, addresses, and other personal data.
    *   **1.4.3 Targeted Advertising Exploitation:** Using purchased data for targeted advertising campaigns.
    *   **1.4.4 Data Aggregation and Correlation:** Combining multiple datasets to create a more complete profile of a target.
    *   **1.4.5 Profile Enrichment:** Adding additional information to existing profiles.
    *   **1.4.6 Background Check:** Purchasing background check reports.

### 1.5 Antique Donation Stores

*   **Purpose:** Searching for discarded electronics and personal items.
    *   **1.5.1 Discarded Electronics Exploitation:** Retrieving data from old computers, phones, etc.
    *   **1.5.2 Personal Item Analysis:** Examining donated items for clues about the donor's identity or activities.
    *   **1.5.3 Document Discovery:** Finding documents in donation bins.
    *   **1.5.4 Data Storage Device Acquisition:** Obtaining storage devices (USB drives, SD cards) from donations.
    *   **1.5.5 Information from Donated Materials:** Extracting information from donated items.
    *   **1.5.6 Physical Item Reconnaissance:**  Examining physical objects for clues.
    *   **1.5.7 Unsecured Data Discovery:** Finding unsecured data on donated devices.

### 1.6 Physical Surveillance

*   **Purpose:** Observing targets in their natural environment.
    *   **1.7.1 Observation of Routines:** Tracking a target's daily activities.
    *   **1.7.2 Building Layout Mapping:** Creating maps of buildings and facilities.
    *   **1.7.3 Security Camera Identification/Access:** Identifying and potentially accessing security camera feeds.
    *   **1.7.4 Access Control System Analysis:** Analyzing access control systems to identify vulnerabilities.
    *   **1.7.5 Employee Behavior Monitoring:** Observing employee behavior for patterns or anomalies.
    *   **1.7.6 Entry and Exit Point Analysis:**  Mapping entry and exit points of a location.
    *   **1.7.7 Vehicle Tracking:** Monitoring vehicle movements.

## 2. Tactic: Pretexting

*   **Definition:** Impersonating someone else to gain access or information.

### 2.1 Impersonation

 * **2.1.1 Authority Figure Impersonation:**  Pretending to be a manager, executive, or government official.
 * **2.1.2 Colleague Impersonation:**  Disguising oneself as a coworker.
 * **2.1.3 Vendor Impersonation:**  Assuming the identity of a supplier or service provider.
 * **2.1.4 IT Support Impersonation:**  Posing as an IT technician.
 * **2.1.5 New Employee Impersonation:**  Presenting oneself as a recently hired employee.
 * **2.1.6 Customer Service Impersonation:**  Acting as a customer service representative.
 * **2.1.7 Law Enforcement Impersonation:**  Pretending to be a police officer or other law enforcement official.

### 2.2 Authority Figure

 * **2.2.1 CEO Fraud:**  Impersonating the company's CEO.
 * **2.2.2 HR Director Impersonation:**  Posing as the Human Resources Director.
 * **2.2.3 Legal Counsel Impersonation:**  Pretending to be a lawyer.
 * **2.2.4 Government Official Impersonation:**  Disguising oneself as a government employee.
 * **2.2.5 Senior Management Impersonation:**  Acting as a high-level manager.
 * **2.2.6 Board Member Impersonation:**  Pretending to be a member of the board of directors.
 * **2.2.7 Auditor Impersonation:**  Posing as an auditor.

### 2.3 Technical Support

 * **2.3.1 Password Reset Scam:** Requesting password resets under false pretenses.
 * **2.3.2 Software Installation Scam:** Tricking users into installing malicious software.
 * **2.3.3 Remote Access Scam:** Gaining remote access to systems through deception.
 * **2.3.4 System Update Scam:**  Promising system updates that install malware.
 * **2.3.5 Malware Removal Scam:** Offering fake malware removal services.
 * **2.3.6 Account Lockout Scam:** Locking accounts and demanding payment for unlocking them.
 * **2.3.7 Network Troubleshooting Scam:**  Using fabricated network issues to gain access.

### 2.4 Customer Service

 * **2.4.1 Account Verification Scam:** Requesting account verification information.
 * **2.4.2 Refund Scam:**  Offering fake refunds.
 * **2.4.3 Order Confirmation Scam:**  Requesting order confirmation details.
 * **2.4.4 Billing Inquiry Scam:**  Initiating fraudulent billing inquiries.
 * **2.4.5 Loyalty Program Scam:**  Exploiting loyalty programs for personal gain.
 * **2.4.6 Shipping Notification Scam:**  Sending fake shipping notifications.
 * **2.4.7 Product Recall Scam:**  Using product recalls to collect information or install malware.

### 2.5 Vendor/Supplier

 * **2.5.1 Invoice Fraud:** Creating and sending fraudulent invoices.
 * **2.5.2 Payment Method Change:**  Requesting changes to payment methods.
 * **2.5.3 Supply Chain Disruption:** Disrupting the supply chain for financial gain.
 * **2.5.4 Delivery Schedule Change:** Altering delivery schedules.
 * **2.5.5 Product Recall Notification:** Sending false product recall notifications.
 * **2.5.6 Contract Renewal Scam:**  Scamming contract renewals.
 * **2.5.7 Discount Offer Scam:** Offering fake discounts.

### 2.6 Urgency

* **2.6.1 Immediate Action Required:** Creating a sense of urgency to bypass scrutiny.
* **2.6.2 Limited Time Offer:**  Using limited-time offers to pressure targets.
* **2.6.3 Account Suspension Warning:** Threatening account suspension.
* **2.6.4 Impending Deadline:**  Creating an artificial deadline.
* **2.6.5 Crisis Situation Exploitation:** Leveraging a crisis for manipulation.
* **2.6.6 Financial Penalty Threat:**  Threatening financial penalties.
* **2.6.7 Security Breach Notification:** Falsely claiming a security breach to elicit information.

### 2.7 Sympathy/Empathy Ploy

* **2.7.1 Personal Hardship Story:** Sharing fabricated stories of hardship.
* **2.7.2 Request for Help:**  Soliciting assistance under false pretenses.
* **2.7.3 Emotional Manipulation:** Using emotional appeals to influence behavior.
* **2.7.4 Exploiting Kindness:** Taking advantage of people's compassion.
* **2.7.5 Creating a Sense of Guilt:**  Making targets feel guilty.
* **2.7.6 Appealing to Conscience:**  Using moral arguments.
* **2.7.7 Sharing a Vulnerability:** Revealing personal information to gain trust.

## 3. Tactic: Initial Contact & Engagement

### 3.1 Spear Phishing

*   **Definition:** Targeted phishing attacks designed to exploit specific individuals or groups.

    * **3.1.1 Targeted Email Attacks**
    * **3.1.2 Personalized Content**
    * **3.1.3 Knowledge of Victim’s Role**
    * **3.1.4 Exploiting Trust Relationships**
    * **3.1.5 Custom Malicious Attachments**
    * **3.1.6 Specific Project References**
    * *3.1.7 Impersonating Known Contacts*

### 3.2 Social Engineering Requests

*   **3.2.1 Pretexting:** Creating a false scenario to elicit information.
*   **3.2.2 Baiting:** Offering something enticing (e.g., a free download) to lure victims.
*   **3.2.3 Quid Pro Quo:**  Offering something in exchange for information or access.
*   **3.2.4 Tailgating:** Following someone into a restricted area without authorization.
*   **3.2.5 Impersonation:** Pretending to be someone else.
*   **3.2.6 Diversion:** Creating distractions to divert attention away from security measures.
*   **3.2.7 Influence:** Attempting to persuade targets to take actions they wouldn’t otherwise.

### 3.3 Direct Approach

* **3.3.1 Cold Calling:** Unsolicited phone calls.
* **3.3.2 Unsolicited Email:** Sending unsolicited emails.
* **3.3.3 Direct Mail:**  Sending physical mail.
* **3.3.4 In-Person Contact:**  Directly approaching individuals.
* **3.3.5 Networking Events:** Engaging with targets at professional events.
* **3.3.6 Referrals:** Obtaining referrals from trusted sources.
* **3.3.7 Online Advertisements:** Using online advertising to reach targets.

### 3.4 Indirect Approach

* **3.4.1 Building Rapport:** Establishing a friendly relationship with the target.
* **3.4.2 Information Gathering:** Collecting information about the target’s interests and needs.
* **3.4.3 Establishing Common Ground:** Finding shared interests or experiences.
* **3.4.4 Observing Behavior:**  Watching how the target interacts with others.
* **3.4.5 Passive Listening:** Paying attention to what the target says without interrupting.
* **3.4.6 Creating a Sense of Familiarity:** Making the target feel comfortable and at ease.
* **3.4.7 Leveraging Existing Relationships:** Using connections to gain access.

### 3.5 Exploiting Vulnerabilities

* **3.5.1 Human Vulnerabilities:**  Exploiting psychological weaknesses (e.g., trust, fear).
* **3.5.2 Process Vulnerabilities:** Targeting flaws in business processes.
* **3.5.3 System Vulnerabilities:** Leveraging security holes in systems and applications.
* **3.5.4 System Misconfigurations:** Exploiting improperly configured systems.
* **3.5.5 Weak Passwords:**  Using easily guessable passwords.
* **3.5.6 Lack of Security Awareness:** Targeting individuals who are unaware of security risks.
* **3.5.7 Outdated Software:** Exploiting vulnerabilities in outdated software.

## 4. Tactic: Manipulating Trust

### 4.1 Scarcity & Urgency

*   **4.1.1 Timeliness:**  Creating a sense that something must be done immediately.
*   **4.1.2 Limited Availability:** Suggesting that an opportunity is rare or will soon disappear.
*   **4.1.3 Exclusive Offers:** Offering special deals only to select individuals.
*   **4.1.4 Deadline Pressure:**  Setting artificial deadlines.
*   **4.1.5 One-Time Opportunity:** Claiming that something can only be done once.
*   **4.1.6 Impending Loss:** Suggesting a potential loss if action isn’t taken.
*   **4.1.7 Financial Penalty Threat:**  Threatening financial consequences.

### 4.2 Authority

* **4.2.1 Expert Endorsement:** Using endorsements from recognized experts.
* **4.2.2 Credentials Display:** Showcasing qualifications and certifications.
* **4.2.3 Uniform/Title:** Utilizing uniforms or titles to convey authority.
* **4.2.4 Celebrity Influence:** Leveraging the popularity of celebrities.
* **4.2.5 Official Communication:**  Presenting information as official.
* **4.2.6 Perceived Status:**  Creating an impression of high status.

### 4.3 Social Proof

* **4.3.1 Testimonials/Reviews:** Using positive customer feedback.
* **4.3.2 Popularity Indicators:** Highlighting the number of users or followers.
* **4.3.3 Group Consensus:**  Presenting a majority opinion as fact.
* **4.3.4 Endorsements:** Obtaining endorsements from trusted sources.
* **4.3.5 Community Engagement:** Demonstrating active participation in a community.

### 4.4 Reciprocity

* **4.4.1 Mirroring:**  Mimicking the target’s behavior or language.
* **4.4.2 Similarity/Common Ground:** Finding shared interests or values.
* **4.4.3 Compliments:** Offering sincere praise.
* **4.4.4 Cooperation:** Working collaboratively with the target.
* **4.4.6 Indebtedness Creation:**  Providing favors to create a sense of obligation.

### 4.5 Commitment & Consistency

* **4.5.1 Small Initial Requests:** Starting with small, easy-to-agree-to requests.
* **4.5.2 Suspiciously Agreeable:**  Agreeing to everything the target says.
* **4.5.3 Public Commitments:** Making public statements of support.
* **4.5.4 Written Statements:** Obtaining written agreements.
* **4.5.5 Foot-in-the-Door Technique:** Using a small request to lead to a larger one.
* **4.5.6 Cognitive Dissonance Exploitation:**  Creating psychological discomfort that leads to compliance.

### 4.6 Reciprocity

* **4.6.1 Unsolicited Gifts/Favors:** Offering unexpected gifts or services.
* **4.6.2 Concessions:** Making concessions to build goodwill.
* **4.6.3 “Free Samples”:** Providing free samples to encourage purchases.
* **4.6.4 Indebtedness Creation:**  Creating a sense of obligation for future favors.

## 5. Tactic: Exploit Trust

### 5.1 Insider Threat

* **5.1.1 Disgruntled Employee:** Targeting employees with grievances.
* **5.1.2 Unintentional Insider:** Employees who inadvertently expose information.
* **5.1.3 Malicious Insider:**  Employees intentionally leaking or stealing data.
* **5.1.4 Espionage:**  Gathering intelligence through insider access.
* **5.1.5 Sabotage:** Disrupting operations by insiders.
* **5.1.6 Data Exfiltration:** Stealing sensitive data from the organization.
* **5.1.7 Policy Violations:**  Circumventing security policies.

### 5.2 Compromised Accounts

* **5.2.1 Stolen Credentials:** Using stolen usernames and passwords.
* **5.2.2 Session Hijacking:** Taking control of an active user session.
* **5.2.3 Adversary-in-the-Middle Attacks:** Intercepting communication between the user and the server.
* **5.2.4 Phishing (Credential Harvesting):**  Obtaining credentials through phishing attacks.

### 5.3 Supply Chain Attacks

* **5.3.1 Compromised Software Updates:** Using malicious software updates to infiltrate systems.
* **5.3.2 Malicious Hardware:** Introducing compromised hardware into the supply chain.
* **5.3.3 Tampered Components:** Altering components during manufacturing or distribution.
* **5.3.4 Vulnerable Libraries:** Exploiting vulnerabilities in third-party libraries.
* **5.3.5 Third-Party Risk:**  Assessing and mitigating risks associated with vendors.
* **5.3.6 Manufacturer Exploitation:** Targeting manufacturers to compromise their products.
* **5.3.7 Code Injection:** Injecting malicious code into software or systems.

### 5.4 Unsecured Systems

* **5.5.1 Default Open Systems/DBs:** Using default credentials and settings.
* **5.5.2 Unpatched Systems/Lack of Software Updates:** Failing to apply security patches.
* **5.5.3 Misconfigurations:**  Improperly configured systems.
* **5.5.5 Lack of Encryption:** Not encrypting sensitive data.
* **5.5.6 Weak Authentication:** Using weak passwords or authentication methods.
* **5.5.7 Outdated Software:** Utilizing outdated software with known vulnerabilities.

## 6. Tactic: Weaponize Trust

### 6.1 GenAI, VibeCoding, Deep Fakes, Chatbots, Synthetic Videos

*   **6.1.1 AI Lookalike:** Using AI to mimic individuals or organizations.
*   **6.1.2 Deepfake Audio/Video:** Creating realistic but fabricated audio and video content.
*   **6.1.3 AI-Generated Chatbot Conversations:** Utilizing chatbots for social engineering attacks.
*   **6.1.4 AI-Assisted Phishing:** Leveraging AI to improve phishing campaigns.

### 6.2 Disinformation Campaigns

* **6.2.1 Fake News:** Spreading false information to mislead the public.
* **6.2.2 Propaganda:**  Using biased or misleading information to influence opinions.
* **6.2.3 Smear Campaigns:** Damaging the reputation of individuals or organizations.
* **6.2.4 Conspiracy Theories:** Promoting unfounded theories and narratives.
* **6.2.5 Astroturfing:** Creating fake online reviews or comments.
* **6.2.6 Inauthentic Profiles:** Using fake social media accounts to spread disinformation.

### 6.3 Exploiting Cognitive Biases

* **6.3.1 Confirmation Bias:** Targeting individuals who are likely to accept information that confirms their existing beliefs.
* **6.3.2 Anchoring Bias:**  Using initial figures to influence subsequent judgments.
* **6.3.3 Availability Bias:** Exploiting readily available information.
* **6.3.4 Framing Effect:** Presenting information in a way that influences perception.
* **6.3.5 Sunk Cost Bias:** Leveraging past investments to justify continued action.
* **6.3.6 Bandwagon Effect:**  Appealing to the desire to conform to group behavior.
* **6.3.7 Authority Bias:** Exploiting deference to authority figures.

### 6.4 Psychological Manipulation

* **6.4.1 Gaslighting:** Making someone question their own sanity or perception of reality.
* **6.4.2 Love Bombing:** Overwhelming someone with affection and attention early in a relationship.
* **6.4.3 Guilt Tripping:**  Making someone feel guilty to manipulate their behavior.
* **6.4.6 Creating Dependency:** Making someone reliant on another person or system.
* **6.4.7 Coercion:** Using threats or pressure to force compliance.

### 6.6 Trust as a Vulnerability

* **6.6.1 Exploiting Kindness**
* **6.6.2 Creating a Sense of Obligation**
   * **6.6.4 Using Personal Relationships**
    * **6.6.5 Taking Advantage of Politeness**
