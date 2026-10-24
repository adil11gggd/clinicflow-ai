ClinicFlow AI — Predicting Missed Appointments and Improving Clinic Follow-Up
Final project proposal for the Building AI course, University of Helsinki / MinnaLearn

Project status: Concept and implementation plan. No trained model, patient dataset, or demonstrated performance is claimed.
Summary
ClinicFlow AI is a proposed decision-support tool that estimates the risk of missed appointments and helps clinics prioritize respectful, timely follow-up. It combines machine learning with existing appointment and CRM workflows, while leaving all patient-facing decisions to clinic staff.
Background
Missed appointments create gaps in clinicians' schedules, disrupt operational planning, and may delay patients' care. Clinics often send the same reminder to every patient or rely on staff to identify appointments that may need additional confirmation. A more tailored approach could help staff focus limited follow-up time where it is most useful.

My interest in healthcare operations, customer relationship management (CRM), and data-driven process improvement motivated this idea. The aim is not to automate medical judgment: it is to support the administrative work surrounding appointments.

The project explores three problems:
1. Clinic staff may not know which upcoming appointments need an additional confirmation call.
2. Manual follow-up can be inconsistent or difficult to prioritize when many appointments are scheduled.
3. Clinics need a way to assess whether personalized reminders actually improve attendance, rather than assuming that more messages are always better.
Research supports investigating this approach. A 2023 rapid systematic review reported evidence that some predictive-model-based reminder interventions reduce outpatient no-shows, while also identifying gaps in evidence about cost-effectiveness and equity. The results of any future ClinicFlow AI implementation would still require independent evaluation in its own setting.
How is it used?
Intended users: Reception teams, appointment coordinators, CRM managers, and clinic operations managers at dental and outpatient clinics.

Proposed workflow:
1. A clinic imports a permitted, minimal set of appointment records from its scheduling or CRM system.
2. Before the appointment, ClinicFlow AI estimates the probability that each appointment will be missed.
3. The dashboard shows risk estimates alongside understandable factors, such as long booking lead time or an unconfirmed appointment.
4. Staff can review suggested actions, for example sending an approved reminder or making a confirmation call. A high-risk score alone never cancels an appointment.
5. The clinic measures attendance, follow-up workload, patient experience, and whether interventions are beneficial.
Example: A receptionist sees tomorrow's schedule. Instead of calling everyone, the team reviews which appointments may need confirmation, checks the relevant circumstances, and decides whom to contact. Patients can still confirm, reschedule, or request help through normal clinic channels.

The interface should be simple, multilingual where appropriate, accessible to nontechnical staff, and designed not to stigmatize patients.
Data sources and AI methods
Potential data sources
With appropriate authorization and legal safeguards, training data could come from a clinic's historical appointment and CRM records. Possible fields include:
- Booking lead time, in days
- Appointment weekday and scheduled time
- Appointment category (administrative or operational grouping)
- Whether confirmation had been received before the prediction
- Historical counts of attended, canceled, and missed appointments, calculated only from earlier appointments
- Outcome label: attended or missed, determined after the appointment date
The first prototype could instead use synthetic records created for demonstration. No real patient records are included in this proposal or repository. Direct identifiers, diagnosis details, and sensitive health information would not be used in a public demonstration.
Proposed AI approach
This is a supervised binary classification problem: predict whether an upcoming appointment will be missed. The model should output an estimated probability rather than an absolute judgment.

I would begin with logistic regression, which provides an understandable benchmark for structured data. If a suitable dataset becomes available, I would compare it with a tree-based model such as gradient boosting, which can capture nonlinear relationships. Model simplicity and calibration would matter as much as raw predictive power.

A non-AI baseline would be routine reminders for all appointments or a simple rule-based follow-up policy.

To avoid misleading results, I would split training and evaluation data chronologically; create all historical features using information available at prediction time; and keep a held-out test period. Measures would include precision, recall, precision-recall AUC, calibration, and the number of useful contacts per staff hour. A small pilot or controlled trial would be needed to test whether model-informed reminders actually improve attendance and patient experience.
Challenges
- Privacy and confidentiality: Appointment records may constitute personal or health-related data. Data minimization, access controls, retention limits, a lawful basis for processing, and applicable regulatory requirements must be addressed before using real records.
- Bias and fairness: Predictive risk must never be treated as blame. Performance and consequences should be examined across relevant groups and clinic contexts, taking care not to use protected traits or unfair proxies for exclusion.
- False predictions: Someone flagged as high-risk may attend, and a lower-risk patient may miss an appointment. Predictions must not result in denial of care, extra fees, or automatic cancellation.
- Data quality and change: Inaccurate CRM histories, schedule changes, missing confirmations, or changes in staff practice could degrade performance.
- Model performance is not intervention effectiveness: A model may predict attendance reasonably well without improving outcomes. Reminder strategies need a separate impact evaluation.
ClinicFlow AI is an administrative decision-support concept, not a medical diagnosis, treatment recommendation, or autonomous scheduling system.
What next?
1. Build a small Python demonstration with synthetic data using pandas and scikit-learn.
2. Compare logistic regression with a simple non-AI baseline using a held-out dataset.
3. Create an example dashboard displaying risk estimates, uncertainty, and explanation summaries.
4. Interview clinic reception and operations staff to refine the workflow and assess whether the suggestions are useful.
5. If ethically and legally feasible, seek permission for a limited pilot using appropriately governed appointment data.
6. Evaluate both model quality and real-world outcomes before considering CRM integration.
The first milestone is a reproducible proof of concept; a real deployment would require technical collaboration, data governance, security review, and clinic stakeholder involvement.
Acknowledgments
- This proposal was prepared for the Building AI course by the University of Helsinki and MinnaLearn.
- Oikonomidi T, et al. Predictive model-based interventions to reduce outpatient no-shows: a rapid systematic review. Journal of the American Medical Informatics Association (2023). PubMed.
- Predicting Missed Appointments in Primary Care: A Personalized Machine Learning Approach (2025). PubMed.
- Collins GS, et al. TRIPOD+AI statement: updated guidance for reporting clinical prediction models that use regression or machine learning methods. BMJ (2024). Publication.
- ChatGPT was used to help draft and structure this conceptual proposal. No external code, protected patient records, or third-party images have been included.
