# Data Quality Detective Challenge

## Task 1: Identify Quality Issues

| Dimension        | Example from dataset                                                          | Explanation                                                                                                               |
| ---------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Accuracy**     | `PatientID P003, AppointmentDate 10/16/2025`                                  | Date format is US-style (`MM/DD/YYYY`) while others are `YYYY-MM-DD`. Could cause misinterpretation by automated systems. |
| **Completeness** | `PatientID P004, PatientName blank`                                           | Missing patient name; SMS reminders cannot be sent and records are incomplete.                                            |
| **Consistency**  | `DoctorName: "Dr. Osei"` vs `"dr. osei"`; `PaymentStatus: "Paid"` vs `"paid"` | Inconsistent capitalization causes mismatches in reporting or filtering.                                                  |
| **Timeliness**   | `AppointmentDate 2025-10-15` for today's date in 2026                         | Past appointments may be treated as upcoming or generate unnecessary reminders.                                           |
| **Validity**     | `PhoneNumber 244789012` missing the leading zero; format not standard         | System may reject SMS or fail validation rules.                                                                           |
| **Uniqueness**   | `P001 Kwame Mensah` appears twice with overlapping appointments               | Duplicate records can inflate patient counts and cause double billing or reporting errors.                                |

---

## Task 2: Assess Business Impact

| Issue                     | Operational Problem                              | Affected Function     |
| ------------------------- | ------------------------------------------------ | --------------------- |
| Missing patient name      | SMS reminders fail to reach patients             | Operations / Clinical |
| Inconsistent doctor names | Reports incorrectly split appointments           | Operations / Clinical |
| Duplicate patient records | Double-counting in reports; billing errors       | Finance / Operations  |
| Invalid phone numbers     | SMS reminders fail                               | Operations / Clinical |
| Past appointment dates    | System may trigger wrong alerts or notifications | Operations            |
| Date format inconsistency | Automated systems misread dates                  | Operations / IT       |

---

## Task 3: Recommend Solutions

| Issue                     | Proposed Fix                                                                                    | Responsible Role              | Verification                                                 |
| ------------------------- | ----------------------------------------------------------------------------------------------- | ----------------------------- | ------------------------------------------------------------ |
| Missing patient names     | Implement mandatory field validation during data entry                                          | Data Steward / Developer      | Run query for blank fields; ensure zero missing names        |
| Inconsistent doctor names | Standardize names using scripts or dropdown selection; enforce capitalization rules             | Data Steward / Developer      | Audit database for variations; confirm standardized naming   |
| Duplicate patient records | Implement uniqueness constraints on `PatientID + AppointmentDate`; deduplicate existing records | Data Steward / Database Admin | Check count before/after deduplication; ensure no duplicates |

**Additional Practical Steps:**

* Use **data validation scripts** for phone numbers (e.g., regex for 10-digit local format).
* Normalize **date formats** to a single standard (`YYYY-MM-DD`) and enforce during entry.
* Schedule **periodic audits** to catch anomalies early.

---

### Task 4: Specialization Perspective – Biggest Risk of Poor Data Consistency

> For a developer, the biggest risk of poor data consistency is that **automated processes, reporting, and analytics become unreliable**. This can lead to incorrect decision-making, financial losses, compliance breaches, and erosion of patient trust in healthcare systems.
