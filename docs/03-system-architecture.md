# 03 – System Architecture

---

## High-Level Architecture

Progress Note is designed as a **cross-platform fitness and nutrition tracking system** with a modular backend and scalable cloud infrastructure.  

```mermaid
flowchart TD
  subgraph MobileApp["Mobile App (React Native + TypeScript)"]
    UI["Workout and Nutrition UI"]
    AnalyticsUI["Analytics Dashboard"]
    AuthUI["Login and Registration"]
  end

  subgraph API["Backend API (Flask, Docker)"]
    AuthService["Authentication Service (JWT)"]
    WorkoutService["Workout Logging Service"]
    NutritionService["Nutrition and Supplements Service"]
    AnalyticsService["Analytics and Predictions"]
  end

  subgraph DB["Database Layer (Azure MySQL)"]
    UserTable[(User)]
    WorkoutTable[(Workout and Sets)]
    NutritionTable[(Intake and Supplements)]
    DirectoryTable[(Activities and Templates)]
  end

  subgraph Cloud["Azure Infrastructure"]
    AppService["App Service"]
    SQL["Azure Database for MySQL"]
    Blob["Azure Blob Storage (exports/media)"]
  end

  MobileApp -->|HTTPS/REST| API
  API --> DB
  API --> Cloud

