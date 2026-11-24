#Introspect
**Zero-input self-knowledge.** turns the data trail you already leave behind into warnings, forecasts and proof of what works for you.

| | |
|---|---|
| Team | prompters |
| College | Dayananda Sagar Academy of Technology and Management |
| Event | wHACKiest 2026 Online Ideathon |
| Track | 3 – Know Thyself: Your Data. Your Intelligence. |
| Pitch deck | [Google Drive link](https://docs.google.com/presentation/d/1mG_06KpK5gE41TG4mmy96CA90kKzHhhr/edit?usp=drive_link&ouid=105703660470407094081&rtpof=true&sd=true) |
| Video pitch | [YouTube link](PASTE_YOUTUBE_LINK) |

> **Blueprint phase.** Per wHACKiest rules, this repository currently holds the design and plans only. Code will be added here during the 24-hour hack day.

## The problem

We leave a data trail all day: phone logs, watch history, searches, payments. It is wasted, never turned into insight.

- Indians spend **~5 hours a day** on their phones, ~70% of it on social media, games and video (EY, 2025).
- **55%** of professional college students in south Karnataka had poor sleep quality (CEGH, 2024).
- **1 in 3** wearable owners stop using it within six months (Endeavour Partners).

| Existing option | Gap |
|---|---|
| Fitness apps (Google Fit, Samsung Health) | Need a watch or manual logging; ignore phone, spending, schedule |
| Screen-time tools (Digital Wellbeing) | Count minutes, but never show what they cost you |
| Mood and habit trackers | Need daily input; most people stop logging within weeks |
| Data exports (Google Takeout etc.) | Years of history in raw files nobody ever opens |

**Typical case:** Priya's phone already knows she slept 4½ hours, watched YouTube until 3 AM and ordered food at midnight twice this week. Nothing puts it together until she burns out.

## Our solution

You grant permissions once. After that you never type, log or answer anything.

### Data you already leave behind
- Phone logs: screen on/off, unlocks, app use
- Charging and alarm snoozes, to infer sleep without a watch
- Phone step counter; Health Connect if available
- Google Takeout: years of YouTube and search history
- Notifications: UPI alerts, food orders
- Calendar, Spotify history, Maps (optional)

### Six insight engines
1. **Sleep without a watch:** inferred from charging, screen and alarms
2. **Strain index:** habits drifting from your normal trigger an early warning
3. **Your levers:** what really moves your sleep and focus, ranked
4. **Natural experiments:** compares matching days in your own past
5. **Stress spending + body clock:** midnight orders, weekend jet lag
6. **Forecast + what-if:** tomorrow's energy, plus nudges that learn what works for you

More: [docs/insight-engines.md](docs/insight-engines.md)

## Architecture

![Architecture diagram](docs/architecture.png)

Parsing happens on the phone. The cloud and AI see only daily features, never messages, search text, payment amounts or GPS.

Details: [docs/architecture.md](docs/architecture.md) · Privacy: [docs/privacy.md](docs/privacy.md)

## Tech stack

| Layer | Choice | Job |
|---|---|---|
| App | React + vite + Tailwind CSS | Responsive laptop dashboard with interactive screens, insight cards and visualizations |
| Backend | Python FastAPI on AWS Lambda | Sync, insights, what-if and brief endpoints, as a container image |
| Data | Supabase(PostgreSQL) | Stores user profiles, daily health records and structured data with Row Level Security (RLS) |
| AI / ML | Pandas + NumPy + Gemini API | Statistical analysis, personalized baselines, pattern detection, trend identification and AI-powered insights |
| Data Collection |Health Connect + StatsManager (Kotlin) + WorkManager | Collects health and activity data through Android background services |
| Integration | Google calendar API | Integrates calendar data to identify schedule patterns and provide context-aware insights |

More: [docs/tech-stack.md](docs/tech-stack.md)

## What makes it different

- **Zero input:** no forms, check-ins or watch needed.
- **Insights on day one:** imports years of history, so there is no two-week wait.
- **Natural experiments:** finds matching days in your past to show what actually works.

## Documentation

| Doc | Contents |
|---|---|
| [architecture.md](docs/architecture.md) | Components and data flow |
| [data-sources.md](docs/data-sources.md) | Each data source, how it's collected and what it feeds |
| [insight-engines.md](docs/insight-engines.md) | How each of the six engines works |
| [data-model.md](docs/data-model.md) | On-phone tables and cloud storage |
| [api-design.md](docs/api-design.md) | Planned endpoints |
| [privacy.md](docs/privacy.md) | What stays on the phone, what syncs, user controls |
| [tech-stack.md](docs/tech-stack.md) | Each tool and the sponsor integrations |
| [hack-day-plan.md](docs/hack-day-plan.md) | Team roles and the 24-hour build plan |

## Team Nexora

| Member | Role on hack day |
|---|---|
| [Prathith h v] (Lead) | Backend: FastAPI on Lambda, sync, Supabase |
| [R Deepa Mahesh Babu] | Android: collectors, notification listener, Takeout importer |
| [Shashidhar] | Android UI: insight cards, body clock, what-if slider |
| [Ramitha S] | Data and AI: sleep inference, baselines, levers, LightGBM + SHAP, Bedrock |

*Introspect is a wellness tool, not a medical device. It suggests seeing a doctor when it spots warning signs.*
