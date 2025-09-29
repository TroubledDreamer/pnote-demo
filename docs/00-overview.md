# Progress Note – Executive Overview

## Problem
Fitness enthusiasts and athletes often struggle with fragmented tracking solutions:  
    Spreadsheets or paper logs lack consistency and insights.
    Generic fitness apps fail to adapt to variations in exercises, supplements, or nutrition plans.
    Data is siloed, making it hard to analyze trends, predict plateaus, or personalize progression.
  
## Solution
**Progress Note** is a cross-platform fitness and nutrition tracking application designed to unify workout, dietary, and supplement logging.  
The system provides **data science–driven analytics** that go beyond logging — delivering insights, predictions, and personalized recommendations to help users achieve consistent progress.     

## Target Users
    **Individual lifters** who want structured workout and nutrition insights.
    **Serious athletes** aiming to optimize performance through advanced analytics.
    **Personal trainers & coaches** (future roadmap) managing multiple clients’ performance data.

## Key Features
    **Workout Tracking** 
        Log sets, reps, weights, and machine levels with variation support.
        Track weekly progression, personal records (PRs), and volume/intensity trends.
    
    **Nutrition & Supplement Logging** 
        Record daily meals, macronutrients, and supplements with flexible units (mg, g, ml, capsule).
        Build reusable dietary templates for consistency. 
    
    **Analytics Dashboard** 
        Weekly and long-term progress trends.
        PR forecasting (time-series analysis, ARIMA).
        Plateau detection and recovery gap analysis.
        PR probability classification (72% CV accuracy).

    **Infrastructure**
        Modular SlideSheet UI for streamlined input.
        Directory-style templates for workouts and dietary intake.
        Dockerized backend with scalable deployment on Azure.

## Tech Stack
    **Frontend**: React Native (TypeScript, Expo)
    **Backend**: Flask (Python), REST API, JWT authentication
    **Database**: MySQL (normalized schema for workouts, nutrition, supplements)
    **Cloud**: Microsoft Azure (App Services + Database)
    **DevOps**: Docker, Postman, GitHub Actions (planned)
    **Analytics**: Python (pandas, scikit-learn, statsmodels, matplotlib)

## Current Status
    Core features implemented and actively tested.
    Applied data science workflows for workout forecasting, plateau detection, and PR probability. 
    **Piloting with demo users** to validate user experience and predictive accuracy. 
    **Source code is private** to protect intellectual property; demo builds and documentation are available on request.





