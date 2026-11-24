# Tech Stack & Sponsor Integrations

## 1. Technology Architecture

```
┌────────────────────────────────────────────────────────┐
│                   FRONTEND / CLIENT                    │
│   React 18  •  Vite  •  Tailwind CSS  •  Recharts      │
│   Lucide React Icons  •  Responsive Mobile Shell       │
└───────────────────────────┬────────────────────────────┘
                            │
┌───────────────────────────▼────────────────────────────┐
│               ON-DEVICE ENGINE (EDGE)                  │
│   SQLite Embedded  •  Resampling / Vectorization       │
│   Statistical Pearson/Spearman Correlation Evaluators  │
└───────────────────────────┬────────────────────────────┘
                            │
┌───────────────────────────▼────────────────────────────┐
│              BACKEND SERVICES & SPONSORS               │
│   Node.js / Express  •  PostgreSQL (Supabase)          │
│   Vercel / Netlify Edge Deployment                     │
│   Gemini 1.5 Flash API (Insight Summarization)        │
└────────────────────────────────────────────────────────┘
```

---

## 2. Tool & Library Breakdown

### Client-Side (Prototype & Web Dashboard)
- **React 18 & Vite**: Fast development cycle, zero-latency Hot Module Replacement, and optimized bundle size.
- **Tailwind CSS v3**: Charcoal/obsidian dark aesthetic (`#09090E`), glowing borders, and accessible typography.
- **Recharts**: High-performance SVG dual-axis charts (`ComposedChart`, `BarChart`, `LineChart`) for multi-variable correlation plots.
- **Lucide React**: Clean, modern icons across biometric and digital categories.

### On-Device Telemetry & Mobile Integration
- **Capacitor / React Native Native Bridges**: Interfaces with iOS HealthKit and Android Health Connect.
- **Local SQLite / OP-SQLite**: Fast embedded SQL queries running locally on iOS and Android devices.

---

## 3. Hackathon / Sponsor Integrations

| Sponsor / Platform | Integration Area | How INTROSPECT Uses It |
| :--- | :--- | :--- |
| **Google Cloud / Gemini** | Natural Language Synthesis | Uses Gemini 1.5 Flash to convert raw statistical correlation pairs (e.g. $-0.74$) into conversational, empathetic habit recommendations. |
| **Supabase / PostgreSQL** | Storage & Auth | Provides zero-knowledge encrypted database sync and row-level security (RLS) for multi-device dashboard views. |
| **Vercel / Netlify** | Deployment & Edge Hosting | Instant global edge CDN distribution with preview branches for judges and team members. |
| **GitHub** | Version Control & CI/CD | Automated build verification and PR workflows for the ideathon proof-of-concept repository. |


