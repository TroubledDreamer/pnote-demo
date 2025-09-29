# 03 – System Architecture

---

## High-Level Architecture

Progress Note is designed as a **cross-platform fitness and nutrition tracking system** with a modular backend and scalable cloud infrastructure.  

```mermaid
flowchart TD
    subgraph MobileApp[Mobile App (React Native + TypeScript)]
        UI[Workout & Nutrition UI]
        AnalyticsUI[Analytics Dashboard]
        AuthUI[Login & Registration]
    end

    subgraph API[Backend API (Flask, Docker)]
        AuthService[Authentication Service (JWT)]
        WorkoutService[Workout Logging Service]
        NutritionService[Nutrition & Supplements Service]
        AnalyticsService[Analytics & Predictions]
    end

    subgraph DB[Database Layer (MySQL on Azure)]
        UserTable[(User)]
        WorkoutTable[(Workout & Sets)]
        NutritionTable[(Intake & Supplements)]
        DirectoryTable[(Activities & Templates)]
    end

    subgraph Cloud[☁️ Azure Infrastructure]
        AppService[App Services]
        SQL[Azure Database for MySQL]
        Blob[Azure Blob Storage (exports/media)]
    end

    MobileApp -->|HTTPS/REST| API
    API --> DB
    API --> Cloud
