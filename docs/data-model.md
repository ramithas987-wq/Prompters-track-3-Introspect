# Data Model & Storage

INTROSPECT employs a hybrid storage strategy: a rich on-device SQLite database for privacy-centric computation, and an optional end-to-end encrypted cloud schema for backup and cross-device sync.

---

## 1. Entity-Relationship Diagram (On-Device SQLite)

```mermaid
erDiagram
    USER_PROFILE ||--o{ DAILY_AGGREGATES : generates
    DAILY_AGGREGATES ||--o{ COMPUTED_CORRELATIONS : produces
    COMPUTED_CORRELATIONS ||--o{ INSIGHT_ACTIONS : triggers
    DAILY_AGGREGATES ||--o{ APP_USAGE_BREAKDOWN : contains

    USER_PROFILE {
        string user_id PK
        string display_name
        int target_steps
        int target_sleep_mins
        int daily_screen_budget_mins
        timestamp created_at
    }

    DAILY_AGGREGATES {
        string date PK
        string user_id FK
        float sleep_hours
        int deep_sleep_mins
        int rem_sleep_mins
        int step_count
        int workout_count
        int resting_heart_rate
        float screen_time_hours
        string most_used_app
        int pickup_count
        int notification_count
        float late_night_screen_hours
        int harmony_score
    }

    COMPUTED_CORRELATIONS {
        string correlation_id PK
        string date FK
        string engine_type
        float correlation_coefficient
        float p_value
        string impact_severity
        string summary_text
    }

    INSIGHT_ACTIONS {
        string action_id PK
        string correlation_id FK
        string category
        string recommendation_text
        boolean is_adopted
        timestamp scheduled_for
    }

    APP_USAGE_BREAKDOWN {
        string id PK
        string date FK
        string app_name
        int minutes_used
        float percentage
        string category
    }
```

---

## 2. SQL Schema Definitions (SQLite)

```sql
-- Daily Aggregate Rollups
CREATE TABLE IF NOT EXISTS daily_aggregates (
    date TEXT PRIMARY KEY,
    user_id TEXT NOT NULL,
    sleep_hours REAL NOT NULL,
    deep_sleep_mins INTEGER DEFAULT 0,
    rem_sleep_mins INTEGER DEFAULT 0,
    step_count INTEGER NOT NULL,
    workout_count INTEGER DEFAULT 0,
    resting_heart_rate INTEGER,
    screen_time_hours REAL NOT NULL,
    most_used_app TEXT,
    pickup_count INTEGER DEFAULT 0,
    notification_count INTEGER DEFAULT 0,
    late_night_screen_hours REAL DEFAULT 0.0,
    harmony_score INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Computed Cross-Domain Correlations
CREATE TABLE IF NOT EXISTS computed_correlations (
    correlation_id TEXT PRIMARY KEY,
    date TEXT NOT NULL,
    engine_type TEXT NOT NULL,
    correlation_coefficient REAL,
    p_value REAL,
    impact_severity TEXT CHECK(impact_severity IN ('High Impact', 'Recovery Pattern', 'Actionable Routine', 'Milestone Achieved')),
    summary_text TEXT NOT NULL,
    explanation_text TEXT NOT NULL,
    FOREIGN KEY(date) REFERENCES daily_aggregates(date) ON DELETE CASCADE
);

-- Actionable Interventions
CREATE TABLE IF NOT EXISTS insight_actions (
    action_id TEXT PRIMARY KEY,
    correlation_id TEXT NOT NULL,
    category TEXT NOT NULL,
    recommendation_text TEXT NOT NULL,
    is_adopted INTEGER DEFAULT 0,
    scheduled_time TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY(correlation_id) REFERENCES computed_correlations(correlation_id)
);
```

---

## 3. Cloud Storage Layer (Optional Zero-Knowledge Sync)

When cloud sync is enabled by the user:
- Records are encrypted on-device with AES-256-GCM using a user-derived key before transmission.
- The cloud backend cannot inspect app names, biometric values, or timestamps.
- Only zero-knowledge cryptograms and aggregated non-identifiable telemetry vectors are persisted in PostgreSQL.

