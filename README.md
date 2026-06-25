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
