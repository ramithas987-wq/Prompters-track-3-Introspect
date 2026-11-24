# FILE: architecture.md
##################################################

# System Architecture

## 1. High-Level Overview

INTROSPECT is an edge-first Personal Intelligence System designed to bridge the chasm between physical health telemetry and digital behavior telemetry. The architecture emphasizes **local execution**, **zero-latency multi-variate correlation**, and **privacy by design**.

```mermaid
flowchart TD
    subgraph MobileDevice ["On-Device Edge Layer"]
        subgraph DataSources ["Passive Telemetry Sources"]
            S1["HealthKit / Health Connect<br/>(Sleep, Steps, Workouts, HR)"]
            S2["UsageStats / ScreenTime API<br/>(App Duration, Pickups, Notifications)"]
        end

        subgraph IngestionEngine ["Ingestion & Normalization Layer"]
            I1["Time-Series Resampler<br/>(15-min epoch alignment)"]
            I2["Feature Vectorizer<br/>(Lagged daily features)"]
        end

        subgraph StorageLayer ["Local Storage Layer"]
            DB[("Encrypted Local SQLite<br/>(Telemetry & Correlation Store)")]
        end

        subgraph AnalyticsEngine ["Introspect Intelligence Core"]
            E1["Multi-Variate Correlation Engine"]
            E2["Cross-Domain Insight Synthesizer"]
            E3["Micro-Habit Recommendation Matrix"]
        end

        subgraph PresentationLayer ["UI & Interaction Layer"]
            UI["Interactive React / Web Dashboard<br/>(Daily Summary, Metrics, Graphs)"]
            N1["Notification & Intervention Dispatcher"]
        end
    end

    subgraph CloudLayer ["Optional Privacy-Preserving Cloud Layer"]
        C1["Zero-Knowledge Encrypted Backup"]
        C2["Anonymized Population Benchmarks"]
    end

    S1 --> I1
    S2 --> I1
    I1 --> I2
    I2 --> DB
    DB --> E1
    E1 --> E2
    E2 --> E3
    E3 --> UI
    E3 --> N1
    E2 -.->|Opt-In Anonymized Hashes| C1
    C2 -.->|Cohort Baselines| E1
```

---

## 2. Component Breakdown

### A. Passive Telemetry Ingestion Pipeline
- **Frequency**: Background worker triggered every 30 minutes or on OS broadcast triggers (e.g. device charging, unlock).
- **Time Alignment**: Converts raw timestamped events into normalized 15-minute time epochs to allow direct cross-referencing between screen usage events and biometric signals.

### B. On-Device SQLite Store
- Holds 90 days of rolled-up personal telemetry.
- Encrypted via OS-level hardware-backed keystore (iOS Keychain / Android Keystore).
- Contains partitioned tables for raw events, daily aggregates, computed correlation coefficients, and scheduled interventions.

### C. Cross-Domain Intelligence Engine
- **Pearson & Spearman Rank Correlation Evaluators**: Computes bidirectional correlation coefficients across paired metric streams:
  - Screen Time $\leftrightarrow$ Sleep Duration
  - Workout Intensity $\leftrightarrow$ Deep Sleep Latency
  - Late-Night Screen Consumption $\leftrightarrow$ Next-Day Activity Drag
- **Anomaly & Threshold Detectors**: Identifies habit spikes (e.g. $>1\text{ hr}$ phone use after 11:00 PM).
- **Natural Language Insight Synthesizer**: Converts statistical outputs into plain-language, non-judgmental explanations paired with single-action recommendations.

### D. Presentation & Intervention Dispatcher
- Provides an ultra-responsive dark-mode user interface.
- Sends proactive scheduled interventions (e.g. triggering bedtime downtime reminders 30 minutes before habitual sleep latency drops).

