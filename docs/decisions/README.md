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
| 0011 | 2026-11-24 | **Start/stop only as IoT Hub direct methods**, never via device-twin desired properties or cloud-to-device messages | ✅ Accepted | — |
| 0012 | 2026-11-24 | **Engineering review adopted in three tiers**: pilot now / pre-MVP / pre-prod (see plan §14) | ✅ Accepted | Each gate |
| 0013 | 2026-11-24 | **Second review adopted on the same rule**: command ID + "updated X ago" that can't freeze now; **real-hardware test gate is a pre-MVP blocker** | ✅ Accepted | MVP gate |

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
- **0011** — Direct methods fail within 15 s if the device is offline, so a start can never arrive late. Twin properties and cloud-to-device messages wait and are delivered on reconnect, possibly much later, which is unsafe for a generator.
- **0013** — A command ID costs ~2 hours and makes pilot debugging traceable; a display that looks live while the API hangs would hide exactly the failures the pilot exists to find. The simulator can't reproduce real cellular drops, crank timing or push delays, so outside users wait until a real unit passes.
- **0012** — The pilot is internal with a simulated device. Only changes that make it unsafe, unreliable or misleading to test without are done now; the rest are gate items for MVP or Prod batch 1.
