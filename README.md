# customer-support-annotation-framework
A data curation projects that focuses on structuring raw support messages using a 3 part scheme (Intent, Sentiment and PII) and handling data privacy edge cases 

## Assessment Phase: Critical Edge Case Analysis

The final phase of the framework involved evaluating 5 complex user messages where intent boundaries overlap. Below is the behavioral analysis of the platform's evaluation key:

### 1. Contact Information vs. Context Location (Row 11)
* **Message:** *"I'd like to change the email linked to my billing info..."*
* **Taxonomy Rule:** Even though the keyword "billing" is present, the core entity being modified is a contact field (email address). The platform prioritizes the **underlying data type** over the functional area, classifying this as `Account`.

### 2. Functional Asset Class Priority (Row 12 & 15)
* **Row 12:** Reporting "weird charges" and a "missing refund" strictly maps to `Billing` because it involves clear financial transactions, overriding the procedural nature of the user's question ("Should I wait?").
* **Row 15:** An unexpected "subscription cancellation" was mapped to `Account` instead of Billing by the platform. This indicates a boundary rule where a total revocation of service access is treated as an account lifecycle status change rather than a standard billing event.

### 3. Interface Failure vs. Functional Intent (Row 13)
* **Message:** App freezing during an account settings update.
* **Taxonomy Rule:** Root-cause engineering takes precedence. If the application environment breaks or crashes (`app keeps freezing`), the classification defaults to `Technical` regardless of which page the user was trying to access.

## Phase 4: Data Quality Assurance (QA) & Peer Review Audit

To ensure the integrity of the training dataset, a comprehensive Quality Assurance (QA) audit was performed on 5 peer-labeled customer messages. The auditing framework utilized a three-tier action system (`Keep` / `Fix` / `Flag`) to enforce taxonomy standards and data privacy compliance.

### Multi-Message Audit Log & Case Studies

| Case Study Message | Original Peer Labels | Audit Action | Core Analytical Justification |
| :--- | :--- | :--- | :--- |
| **1.** *"Hi, I need to update my phone number. I got a new one after moving..."* | Intent: Account<br>Sentiment: Neutral<br>PII Flag: No | **FIX** | **PII Flag Correction:** While the explicit digits are missing, the explicit request to update a sensitive contact field counts as introducing personal info, requiring a `Yes` flag for privacy compliance. |
| **2.** *"Just a heads up! I switched banks last week and my auto payment failed..."* | Intent: Billing<br>Sentiment: Neutral<br>PII Flag: No | **KEEP** | **Perfect Alignment:** Intent is properly routed to `Billing` due to transaction failure. Sentiment is correctly `Neutral` given the collaborative tone, and no actual financial strings are shared to trigger PII. |
| **3.** *"I have emailed twice about this bug... My screen freezes every time I try to save..."* | Intent: Bug<br>Sentiment: Negative<br>PII Flag: No | **KEEP** | **Taxonomy Validation:** The platform expands the framework to accept `Bug` as a standalone intent for interface errors. Sentiment is accurately marked `Negative` due to explicit frustration. |
| **4.** *"Can you cancel my subscription?... My account is under j.ramos@fastmail.com."* | Intent: Billing<br>Sentiment: Negative<br>PII Flag: No | **FIX** | **Data Security Enforcement:** The peer missed a direct piece of Personally Identifiable Information. The explicit inclusion of a specific email string (`j.ramos@fastmail.com`) requires an immediate fix to `Yes`. |
| **5.** *"Why did you close my ticket?... Every time I log in, it says 'unauthorised'..."* | Intent: Bug<br>Sentiment: Negative<br>PII Flag: No | **KEEP** | **Error Persistence Mapping:** A recurring system authorization failure after a password reset is correctly labeled as a `Bug` intent with a `Negative` sentiment due to user irritation. |

## Phase 5: Taxonomy & Guideline Optimization

A key responsibility of a Data Quality Reviewer is identifying gaps in documentation to minimize future labeling variance. 

### Proposed Guideline Revision
* **Observation:** During the peer-review phase, the validation key accepted a fourth intent classification (`Bug`) which was missing from the initial core onboarding taxonomy (Billing, Account, Technical). This discrepancy caused initial alignment friction during technical error sorting.
* **Recommendation:** Update the *One-Page Guidelines* to explicitly define the boundaries between a standard infrastructure failure (`Technical`) and a persistent application software anomaly (`Bug`). Providing explicit code-path examples for both will significantly increase inter-annotator agreement (IAA) scores in future data pipelines.
