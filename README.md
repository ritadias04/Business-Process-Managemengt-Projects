# SafeDrive Insurance – Business Process Management & Process Mining

Two-part Business Process Management project developed at NOVA IMS (Master's in Data Science and Advanced Analytics, 2025/26). It analyses the motor insurance claims process of **SafeDrive Insurance**, first by modelling it in BPMN and then by analysing real event data with process mining.

| Assignment | Focus | Tool | Grade |
|---|---|---|---|
| **1 – AS-IS Process Modelling** | BPMN model of the claims handling process | Bizagi Modeler | **17.50 / 20** |
| **2 – Process Mining Analysis** | Dashboard and report on 23,275 real claims | Celonis | **17.30 / 20** |

## Business Context
SafeDrive Insurance is a mid-sized motor insurance company serving private and corporate customers across Portugal. Claim volumes have grown significantly, while customer satisfaction has declined. Customers report long processing times, unclear communication and payment delays. Management asked for an analysis of the current (AS-IS) claims process to find the causes.

---

## Assignment 1 – AS-IS Process Model (BPMN)

**Goal:** model the current claims handling process, from claim registration to payment confirmation, as a detailed BPMN diagram.

### Model Structure
The model uses a **two-level hierarchy**:
- **Level 1 – Main process:** end-to-end view with collapsed sub-processes and the key decision points (Is the claim validated? Does it require fraud verification? Is the fraud confirmed?).
- **Level 2 – Four detailed sub-processes:**
  1. **Claim Validation:** policy verification (does it exist? was it active?), with rejection and notification paths.
  2. **Damage Evaluation:** decision on physical inspection, inspector scheduling and report, photo evaluation, and repair cost estimation. Claims above 1,500€ are routed to fraud verification.
  3. **Fraud Verification:** claim history review, escalation of suspicious cases, requests for additional information, and fraud confirmation.
  4. **Claim Settlement:** payment approval, processing and transfer, and payment confirmation to the policyholder.

**Participants (pools and lanes):** Policyholder, Claim Handler, Company Inspector, Fraud Analyst Team, Finance Department and System.

---

## Assignment 2 – Process Mining with Celonis

**Goal:** use real event data to analyse the AS-IS process, find bottlenecks and deviations, understand what drives dissatisfaction, and give data-driven recommendations.

### Data
- **Case table:** 23,275 claims with vehicle type, district, claim reason, amount, refusal flag and customer satisfaction (1–5).
- **Event log:** 233,652 events across 13 activities, from January 2020 to October 2024.

### ETL
- Uploaded both tables to a Celonis Data Pool and profiled them with SQL transformations.
- Built a data model with a 1:N relationship between the case table and the event log.
- Data quality checks flagged minor anomalies, such as negative throughput times and very few Theft/Robbery claims.

### Dashboard (9 pages)
1. **Process Discovery:** process map by case and activity frequency and by throughput time (average, median and trimmed mean), with a vehicle type filter.
2. **Variant Explorer:** the ~5,450 process variants and their throughput times.
3. **Case Explorer:** claim-level drill-down to investigate outlier cases.
4. **Business Analysis:** claims volume and value by district, vehicle type and claim reason.
5. **Satisfaction Analysis:** satisfaction scores across segments.
6. **Conformance Checking:** deviations from the reference process and their time impact.
7. **Time & Efficiency Analysis** *(additional)*: intake vs. processing phases, and delays by district, vehicle and claim reason.
8. **Claims Refusal Analysis** *(additional)*: refusal rates and characteristics.
9. **Communication Analysis** *(additional)*: SMS, email and call patterns and regional inquiry rates.

### Key Findings
- **No standardisation:** about 5,450 distinct variants and 0% conformance to the reference model. The two main variants cover only 51% of claims.
- **Long, uneven processing times:** 32.8 days on average (median 15), reaching about 99 days in Braga and 67 days for Collision/Impact claims.
- **Costly deviations:** for example, missing "Assessment Closed" steps (13.6% of cases, +30 days) and out-of-sequence information calls (up to +42 days).
- **Communication failures:** 11.6% of customers had to call for information, rising to about 39–42% in Coimbra and Beja. Customers sent more emails than they received.
- **Moderate satisfaction:** 3.18 out of 5 on average, with almost 30% of claims rated 1 or 2.

### Recommendations
- Standardise the process into a small set of enforced paths.
- Investigate the slowest districts (Braga, Porto, Guarda).
- Create a dedicated fast-track for Collision/Impact claims.
- Send proactive automatic updates at each key milestone.
- Add system safeguards so critical steps, such as closing the assessment, can't be skipped.
- Train staff to reduce unexpected activities.

