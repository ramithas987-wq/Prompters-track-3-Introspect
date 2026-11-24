# API Design Specification

## Overview

INTROSPECT is architected to run primarily on-device. For cloud-connected features (backup sync, cross-device dashboard, anonymous population cohorts, and scheduled notifications), the platform defines a RESTful API with standard JSON payloads.

**Base URL**: `https://api.introspect.health/v1`  
**Authentication**: `Authorization: Bearer <JWT_USER_TOKEN>`

---

## Endpoints

### 1. Synchronize Encrypted Daily Summary
- **Endpoint**: `POST /sync/daily-summary`
- **Description**: Uploads end-of-day encrypted aggregated metrics and calculated scores.
- **Request Body**:
```json
{
  "date": "2026-11-24",
  "client_version": "1.0.0",
  "metrics": {
    "sleep_hours": 6.75,
    "deep_sleep_mins": 80,
    "step_count": 8432,
    "workout_count": 4,
    "resting_heart_rate": 64,
    "screen_time_hours": 6.53,
    "most_used_app": "Instagram",
    "pickup_count": 72,
    "notification_count": 146,
    "late_night_screen_hours": 1.25,
    "harmony_score": 74
  },
  "encrypted_telemetry_blob": "enc_aes256_gcm_..."
}
```
- **Response**: `200 OK`
```json
{
  "status": "success",
  "sync_timestamp": "2026-11-24T14:30:00Z",
  "next_sync_window": "2026-11-25T02:00:00Z"
}
```

---

### 2. Retrieve Behavioral Insights Feed
- **Endpoint**: `GET /insights/feed`
- **Query Params**: `?date=2026-11-24&limit=5`
- **Response**: `200 OK`
```json
{
  "date": "2026-11-24",
  "insights": [
    {
      "id": "insight-screen-sleep",
      "title": "Screen Time + Sleep Correlation",
      "badge": "Cross-Domain Impact",
      "summary": "Higher screen usage late at night is associated with shorter sleep duration.",
      "explanation": "On nights with more than 45 minutes of screen use after 11:00 PM, sleep dropped by 45 mins.",
      "recommendation": "Activate phone Downtime at 10:30 PM.",
      "stat": "-1.2 hrs sleep on high late-screen nights",
      "impact_severity": "High Impact",
      "is_adopted": false
    }
  ]
}
```

---

### 3. Adopt Micro-Intervention
- **Endpoint**: `POST /actions/{action_id}/adopt`
- **Description**: Registers that the user accepted a habit recommendation, scheduling appropriate OS-level downtime and notification hooks.
- **Request Body**:
```json
{
  "action_id": "insight-screen-sleep",
  "scheduled_downtime_start": "22:30:00",
  "notification_channel": "push"
}
```
- **Response**: `200 OK`
```json
{
  "status": "adopted",
  "action_id": "insight-screen-sleep",
  "next_evaluation": "2026-11-25T07:00:00Z"
}
```

---

### 4. Fetch Cross-Domain Correlation Vectors
- **Endpoint**: `GET /analytics/correlations`
- **Query Params**: `?range=7d`
- **Response**: `200 OK`
```json
{
  "range": "7d",
  "correlations": [
    {
      "factor_a": "late_night_screen",
      "factor_b": "sleep_duration",
      "coefficient": -0.74,
      "significance": "p < 0.01"
    },
    {
      "factor_a": "exercise_minutes",
      "factor_b": "deep_sleep_minutes",
      "coefficient": 0.68,
      "significance": "p < 0.05"
    }
  ]
}
```
