# GovernanceReview

## QuickLoan Mobile Ethical Data Review Lab

---

## Deliverable 1: QuickLoan Governance Review Card

| Section                                        | Issue / Definition                                                          | Impact                                                                                            | Suggested Fix / Mitigation                                                                                                                                                                                                                                                                                            |
| ---------------------------------------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Data Quality Risk**                       | **Inconsistent phone numbers and missing loan application fields**          | Loan approvals may be delayed or denied incorrectly; SMS notifications fail; inaccurate reporting | Implement **input validation and standardized formatting rules** at data entry; add **mandatory fields enforcement** in the app                                                                                                                                                                                       |
| **2. Legal & Compliance Risk**                 | **Collection of entire contact lists without consent**                      | Violates Ghana DPA Act 843; potential fines and reputational damage                               | Classify contact list as **Sensitive PII**; collect only data necessary for loan decisions; implement **explicit opt-in consent workflow**                                                                                                                                                                            |
| **3. Bias & Fairness Risk**                    | **ML model may favor certain demographics due to historical training data** | Could result in unfair approvals/denials based on region, gender, or age                          | Introduce **bias monitoring dashboard**; track approval rates across demographic groups weekly; periodically **retrain model with balanced datasets**                                                                                                                                                                 |
| **4. Storytelling / Reporting Recommendation** | **Ethical Loan Approval Fairness Metric**                                   | Monitors fairness and transparency of automated decisions                                         | **Metric Name:** "Approval Rate by Demographic Group" - measures percentage of approvals across key demographic slices (gender, age group, region) <br> **Visualization Type:** Grouped Bar Chart <br> **Why it Matters:** Highlights disparities in loan approvals, ensuring accountability and ethical transparency |

---

## Deliverable 2: Corrected Data Flow Diagram (Annotations)

**Key Corrections (with Footnotes/Annotations):**

1. **User Mobile App - Excessive Collection**
   * **Correction:** Limit data collection to fields **necessary for loan approval** (income, employment status, bank account info).
   * **Annotation:** "Reduce PII collection to comply with Data Minimization principle under DPA."

2. **API Gateway → Raw Data DB - No Consent Capture**
   * **Correction:** Add **explicit consent capture step** before data storage.
   * **Annotation:** "Ensures lawful processing; users opt-in to data collection and loan scoring."

3. **Raw Data DB - No Classification / Retention Policy**
   * **Correction:** Apply **Data Classification** (Confidential / Sensitive) and define retention schedule.
   * **Annotation:** "Enables secure storage, lifecycle management, and compliance with retention rules."

4. **Preprocessing Service - No Handling Guidelines**
   * **Correction:** Mask or anonymize non-essential PII before preprocessing.
   * **Annotation:** "Reduces risk of exposure during feature engineering and ML training."

5. **Decision Service - No Transparency / Logging**
   * **Correction:** Implement **audit logging of automated decisions**.
   * **Annotation:** "Allows traceability and supports fairness reporting metrics."

---

## Deliverable 3: Summary of Review Process (Example 250 Words)

In conducting the QuickLoan Mobile ethical data review, I applied **Data Lifecycle and Classification principles** to identify high-risk points in the company's data pipeline. Starting from data collection at the user mobile app, I examined which data elements were necessary for loan scoring, highlighting excessive collection such as full contact lists. By classifying all personal data into categories (Public, Internal, Confidential, Sensitive), I was able to pinpoint **compliance risks** under Ghana's DPA, specifically the lack of explicit consent and unclear retention policies.

Next, I traced data through the preprocessing, model training, and decision services to identify potential sources of **algorithmic bias**, recognizing that historical patterns in loan approvals could unfairly favor certain demographics. To mitigate these risks, I proposed a **bias monitoring dashboard** and routine retraining with balanced datasets.

To ensure **ethical transparency**, I designed a single actionable metric: **Approval Rate by Demographic Group**, visualized as a grouped bar chart. This metric tracks loan approval rates across gender, age groups, and regions, providing stakeholders with clear insight into fairness in automated decision-making. By monitoring this metric, QuickLoan can quickly identify disparities, evaluate the impact of corrective actions, and demonstrate accountability to regulators and customers.

Finally, I recommended practical fixes at key points in the data pipeline, including data minimization, input validation, consent capture, masking/anonymization, and audit logging. These combined steps ensure that QuickLoan Mobile's automated loan decisions are not only efficient but also **ethically sound, legally compliant, and fair** across all user groups.
