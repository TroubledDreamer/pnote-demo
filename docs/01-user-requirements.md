# 01 – User Requirements

## Use Case: Log a Workout Set
**Rationale:** Users need to accurately record workouts (sets, reps, weight, and variations) to track progress over time.  

**User Requirement:**  
U1.0 The user shall be able to log a workout set with activity, variation, reps, and weight (lb/kg) or machine level.  

**System Requirements:**  
R1.1 The system shall store workout data (date, time, activity, variation, reps, weight, unit).  
R1.2 The system shall validate input (e.g., reps > 0, weight ≥ 0).  
R1.3 The system shall associate sets with a training session.  

**Acceptance Criteria:**  
- A user can create a new workout set.  
- The saved set is displayed in the session view.  
- Invalid data is rejected with an error.  

**Relates to/Dependencies:** Training Session entity, Activity & Variation directory.  
**Priority:** High  


## Use Case: View Weekly Workout Analytics
**Rationale:** Users need to understand trends in performance to adjust training plans.  

**User Requirement:**  
U2.0 The user shall be able to view weekly workout trends (volume, intensity, and PRs).  

**System Requirements:**  
R2.1 The system shall aggregate workout data weekly by activity and variation.  
R2.2 The system shall display charts (progression, % change, PRs).  
R2.3 The system shall highlight plateaus or regressions.  

**Acceptance Criteria:**  
- Weekly progression charts load within 2 seconds.  
- PRs are correctly flagged per activity/variation.  
- Plateau detection is visible when slope < threshold.  

**Relates to/Dependencies:** Logged workout sets, analytics pipeline.  
**Priority:** High  


## Use Case: Log Nutrition and Supplements
**Rationale:** Users want to track food and supplement intake for better diet management.  

**User Requirement:**  
U3.0 The user shall be able to log dietary intake (macronutrients) and supplements (amount + unit).  

**System Requirements:**  
R3.1 The system shall support units (g, mg, ml, capsule).  
R3.2 The system shall allow creation of reusable dietary templates.  
R3.3 The system shall store supplement usage linked to an intake entry.  

**Acceptance Criteria:**  
- User can add a meal with calories, protein, carbs, fat.  
- User can add supplements with units.  
- Daily nutrition totals update correctly.  

**Relates to/Dependencies:** Dietary & Supplement directories.  
**Priority:** Medium  


## Use Case: Predict Personal Records (PRs)
**Rationale:** Users benefit from predictive insights that estimate future PRs and progression rates.  

**User Requirement:**  
U4.0 The user shall be able to view predictions for PRs and training outcomes.  

**System Requirements:**  
R4.1 The system shall analyze historical data with regression and time-series forecasting.  
R4.2 The system shall display forecasts with confidence intervals.  
R4.3 The system shall compute PR probability per activity/variation.  

**Acceptance Criteria:**  
- Forecast charts are generated for selected exercises.  
- PR probability is displayed as a percentage.  
- Predictions update when new data is logged.  

**Relates to/Dependencies:** Workout analytics pipeline.  
**Priority:** Medium 


## Use Case: Export Data
**Rationale:** Users should be able to control and back up their personal workout/nutrition data.  

**User Requirement:**  
U5.0 The user shall be able to export workout, dietary, and supplement data in CSV format.  

**System Requirements:**  
R5.1 The system shall generate CSV files for workouts, intakes, and supplements.  
R5.2 The system shall provide a secure download link or email delivery.  
R5.3 The system shall respect user privacy (exports only their own data).  

**Acceptance Criteria:**  
- A CSV export button is available.  
- CSV files contain clean, normalized data with headers.  
- Export completes within 60 seconds.  

**Relates to/Dependencies:** Database schema, user authentication.  
**Priority:** Medium  



## Non-Functional Requirements

### Performance Requirements
- **API latency:** p50 < **300 ms**, p95 < **800 ms** for standard endpoints under normal load (≤50 concurrent users).
- **Write operations:** create/update of sets, intakes, supplements complete in **< 500 ms** end-to-end.
- **Analytics dashboards:** first meaningful render in **< 2 s** on a mid-tier mobile device over 4G; subsequent navigations **< 1 s** with caching.
- **Batch analytics:** weekly aggregates generate in **< 10 s**; per-exercise PR forecast in **< 2 s** on demand.
- **Payloads & pagination:** default page size 25–50; response payloads **< 1 MB**; compression enabled (gzip/br).
- **Capacity (MVP target):** supports **500 DAU** with **≥50** concurrent sessions without degradation; vertically/horizontally scalable.

### Safety and Security Requirements
- **Transport security:** HTTPS only (TLS 1.2+); HSTS enabled on public endpoints.
- **AuthN/AuthZ:** JWT bearer tokens (access **≤15 min**, refresh **≤7 days**); server-side revocation; roles planned for coach/admin.
- **Data protection:** encryption at rest (e.g., Azure MySQL AES-256); keys/secrets managed via Azure Key Vault or equivalent; no secrets in code or repo.
- **App hardening:** input validation & output encoding; CSRF (where applicable), rate limiting, account lockout, secure password hashing (bcrypt/argon2); OWASP Top 10 mitigations.
- **Privacy & compliance:** PII minimization; user self-service **export** and **delete**; GDPR-friendly data flows and logs.
- **Backups & recovery:** automated daily backups; retention **≥30 days**; **RPO ≤24 h**, **RTO ≤4 h**.
- **Environment separation:** production, staging, and demo data isolated; demo accounts auto-purged after **≤30 days**.

### Software Quality Attributes
- **Availability/Reliability:** API uptime **≥99.5%** monthly; error budget tracked; graceful degradation for analytics if upstream is slow.
- **Maintainability:** type-safe code (TypeScript/Python typing); linting & formatting enforced; backend unit/integration test coverage **≥70%** for core logic; API contract tests for critical endpoints.
- **Scalability:** stateless API processes; horizontal scale on Azure App Service; DB read-replicas/caching planned for growth.
- **Usability & Accessibility:** mobile UI adheres to WCAG 2.1 AA contrast; minimum tap target **≥44×44 pt**; clear error states and loading cues.
- **Observability:** structured logging (correlation IDs), metrics (latency, error rate, throughput), and tracing; alerts on p95 latency, 5xx rate, queue depth, and DB connections.
- **Portability/Compatibility:** Android **10+** and iOS **15+**; supports common screen sizes; tolerant of intermittent connectivity with retries and queued writes.
- **Data Quality (Analytics):** model validation tracked; PR probability classifier holds **≥0.70** cross-validated accuracy with drift monitoring and periodic retraining.
- **Security of exports:** generated CSV links are signed, time-limited, and scoped to the requesting user.

