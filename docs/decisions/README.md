# ⚖️ Decision log

Short records of choices that would be costly to reverse. New decisions: copy [`_template.md`](_template.md) to `NNNN-short-title.md` and add a row below.

| # | Date | Decision | Status | Revisit at |
|---|---|---|---|---|
| 0001 | 2026-11-22 | **Expo / React Native (TypeScript)** for the app; Kivy retired | ✅ Accepted | — |
| 0002 | 2026-11-22 | **Separate repo** `ems1000-mobile`; backend changes stay in `ems1000-staging` | ✅ Accepted | — |
| 0003 | 2026-11-22 | **Android first**; iOS at Prod batch 1 | ✅ Accepted | Prod batch 1 |
| 0004 | 2026-11-22 | **Pilot sign-in = existing Entra tenant accounts** (team-issued). MVP → Entra External ID with phone + SMS code; later + Google | ✅ Accepted | MVP |
| 0005 | 2026-11-22 | **Manual user↔device linking** (script, then admin web panel). Data model includes a `role` field from day one | ✅ Accepted | MVP |
| 0006 | 2026-11-22 | **Start safety (pilot):** confirm dialog; every command logged in the backend. Later: role limits, then PIN/biometric | ✅ Accepted | MVP |
| 0007 | 2026-11-22 | **Alerts:** push for critical faults via Expo Push (→ Firebase FCM), in-app alert list, per-alert toggles | ✅ Accepted | Prod batch 1 |
| 0008 | 2026-11-22 | **Connectivity:** last-known state + offline badge; commands disabled when offline; no queued commands (safety) | ✅ Accepted | — |
| 0009 | 2026-11-22 | **App = user features, web panel = admin** (fault injection, all-devices view, linking) | ✅ Accepted | — |
| 0010 | 2026-11-22 | **Engineer review approach** | ⏳ Open — decide before MVP | MVP gate |

## Why each was chosen (one line each)

- **0001** — Cloud builds (no Mac needed for iOS), built-in push, over-the-air fixes, large ecosystem. Kivy is weak at push and app-store releases.
- **0002** — App and backend release on different schedules; keeps CI and history clean.
- **0003** — Target market is Android-heavy; halves testing for the pilot.
- **0004** — Pilot is internal only; the API already moves to Entra tenant tokens. Building on Entra means the MVP switch is mostly configuration.
- **0005** — Fastest for 3 users; the `role` field avoids a data migration when invites/roles arrive.
- **0006** — Minimal friction for the internal pilot; the backend log is cheap and gives evidence if a generator starts unexpectedly.
- **0007** — Expo Push is free and needs no extra Azure service for the pilot; Azure Notification Hubs can replace it at scale.
- **0008** — A start command that fires late (after reconnecting) could start a generator when nobody expects it.
- **0009** — Keeps the customer app simple and lowers the risk of shipping admin powers to customers.
