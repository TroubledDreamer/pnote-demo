# 04 – Data Model & ERD

This document describes the core relational model for **Progress Note**.  
The goal is a clean, normalized schema that supports fast logging, reliable analytics, and future features (coach views, templates).

---

## Entity–Relationship Diagram (ERD)

```mermaid
erDiagram
  user ||--o{ user_information : has
  user ||--o{ weight : has
  user ||--o{ height : has
  user ||--o{ training_session : has
  user ||--o{ macronutrient : logs
  user ||--o{ intake : logs
  user ||--o{ directory : owns
  user ||--o{ directory_cache : owns
  user ||--o{ supplement : takes

  training_type_list ||--o{ activity_list : categorizes
  activity_list ||--o{ activity_allowed_variation : allows
  variation_list ||--o{ activity_allowed_variation : is_allowed

  activity_list ||--o{ activity_config : has
  activity_config ||--o{ activity_config_variation : composed_of
  variation_list ||--o{ activity_config_variation : member

  training_session ||--o{ anaerobic_set : has
  anaerobic_set ||--o{ anaerobic_rep : has

  training_session ||--o{ aerobic_set : has

  intake ||--o{ supplement : includes
  supplement_list ||--o{ supplement : referenced_by

  directory ||--o{ directory : contains
  directory ||--o{ directory_dietary : links
  dietary_template ||--o{ directory_dietary : linked

  directory ||--o{ directory_activity : links
  activity_config ||--o{ directory_activity : linked

  directory ||--o{ directory_intake : links
  intake ||--o{ directory_intake : linked

  user {
    int id PK
    string name
    string email
    string password
    datetime created_at
  }

  user_information {
    int id PK
    int user_id FK
    string sex
    float height_cm
    date date_of_birth
  }

  weight {
    int id PK
    int user_id FK
    float weight_kg
    datetime date
  }

  height {
    int id PK
    int user_id FK
    float height_cm
    datetime date
  }

  training_type_list {
    int id PK
    string name
    string description
  }

  activity_list {
    int id PK
    string name
    string description
    int training_type_list_id FK
  }

  variation_list {
    int id PK
    string name
    string description
  }

  activity_allowed_variation {
    int activity_list_id PK, FK
    int variation_list_id PK, FK
  }

  activity_config {
    int id PK
    string name
    int activity_list_id FK
    string variation_set_hash
  }

  activity_config_variation {
    int activity_config_id PK, FK
    int variation_list_id PK, FK
  }

  training_session {
    int id PK
    int user_id FK
    int activity_config_id FK
    int training_type_list_id FK
    datetime date
  }

  anaerobic_set {
    int id PK
    int training_session_id FK
    datetime date
  }

  anaerobic_rep {
    int id PK
    int anaerobic_set_id FK
    int rep_order
    int repetition
    float weight_kg
  }

  aerobic_set {
    int id PK
    int training_session_id FK
    float duration
    float distance
    float added_weight_kg
    datetime date
  }

  macronutrient {
    int id PK
    int user_id FK
    float calories
    float protein_g
    float carbohydrate_g
    float fat_g
    datetime date
  }

  intake {
    int id PK
    int user_id FK
    string name
    boolean template
    datetime date
  }

  supplement_list {
    int id PK
    string name
    string description
  }

  supplement {
    int id PK
    int user_id FK
    int supplement_id FK
    int intake_id FK
    float weight
    string unit
    datetime date
  }

  directory {
    int id PK
    int user_id FK
    boolean is_public
    boolean is_main
    string category
    string name
    int parent_id FK
  }

  dietary_template {
    int id PK
    int user_id FK
    string name
    boolean is_public
    string structure
  }

  directory_dietary {
    int directory_id PK, FK
    int template_id PK, FK
  }

  directory_activity {
    int directory_id PK, FK
    int activity_config_id PK, FK
  }

  directory_intake {
    int directory_id PK, FK
    int intake_id PK, FK
  }

  directory_cache {
    int id PK
    int user_id FK
    string category
    string structure
    datetime last_updated
  }

  blob_storage {
    int id PK
    string uri
  }

