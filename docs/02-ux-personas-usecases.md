# 02 – UX Personas & Use Cases

---

## Personas

### Persona 1: "Strength Sam" – Intermediate Lifter
- **Profile:** 25-year-old gym-goer, trains 4–5 times per week.
- **Goals:** Improve major lifts, avoid plateaus, track supplements for recovery.
- **Frustrations:** Spreadsheets are clunky, existing apps don’t handle exercise variations well.
- **Needs from Progress Note:** Easy set logging, progress analytics, predictive insights (PR probability, plateau alerts).

---

### Persona 2: "Coach Casey" – Personal Trainer
- **Profile:** 34-year-old coach managing 10+ athletes.
- **Goals:** Monitor client progress, detect under/over-training, recommend dietary adjustments.
- **Frustrations:** Hard to track multiple clients in one system.
- **Needs from Progress Note:** Centralized dashboards, exportable data, ability to create/share templates. *(Roadmap feature)*

---

### Persona 3: "Nutrition Nina" – Health Enthusiast
- **Profile:** 29-year-old professional balancing work and fitness.
- **Goals:** Ensure consistent dietary intake, track supplement effectiveness, stay accountable.
- **Frustrations:** Logging macros manually is tedious, and apps often lack supplement tracking.
- **Needs from Progress Note:** Flexible dietary logging, supplement units (mg/g/ml/capsule), nutrition insights.

---

## Core Use Cases

### Use Case 1: Log a Workout Set
- **Actors:** Strength Sam  
- **Precondition:** User is signed in and has an active training session.  
- **Steps:**
  1. User selects activity and variation.  
  2. User enters reps and weight (lb/kg) or machine level.  
  3. System validates and saves the set.  
  4. System updates session and analytics cache.  
- **Outcome:** The set is stored and visible in the session log.  

---

### Use Case 2: View Weekly Progress Trends
- **Actors:** Strength Sam  
- **Precondition:** User has logged workouts.  
- **Steps:**
  1. User navigates to the analytics dashboard.  
  2. System aggregates weekly data by activity/variation.  
  3. Charts display volume, intensity, and PRs.  
- **Outcome:** User understands training progress and areas of plateau.  

---

### Use Case 3: Log Nutrition & Supplements
- **Actors:** Nutrition Nina  
- **Precondition:** User has an account.  
- **Steps:**
  1. User selects “Add Intake.”  
  2. User enters calories/macros and supplement data with units.  
  3. System saves intake and updates daily totals.  
- **Outcome:** User sees accurate daily nutrition + supplement breakdown.  

---

### Use Case 4: Predict Personal Records (PRs)
- **Actors:** Strength Sam  
- **Precondition:** User has ≥4 weeks of training history.  
- **Steps:**
  1. User navigates to “PR Predictions.”  
  2. System applies forecasting models (regression, ARIMA, classification).  
  3. System displays expected PRs, probability, and confidence intervals.  
- **Outcome:** User sees estimated performance trajectory and training risks.  

---

### Use Case 5: Export Training Data
- **Actors:** Coach Casey  
- **Precondition:** User has logged workouts and nutrition.  
- **Steps:**
  1. User selects “Export Data.”  
  2. System generates secure CSV files.  
  3. User downloads or receives a link.  
- **Outcome:** User obtains structured data for external analysis or sharing.  

---

## UX Principles Reflected
- **Clarity:** Simple workflows for common tasks (log → view → export).  
- **Consistency:** Unified design across workout, nutrition, and supplement logging.  
- **Predictive Value:** Data science methods (forecasts, plateau detection) provide *actionable insights* rather than raw data.  
- **Scalability:** Supports single users now, coach/multi-user dashboards later.  

---
