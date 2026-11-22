# EMS-1000 Mobile App

📱 The Android app (Expo / React Native) for monitoring and controlling EMS-1000 generator units.
It talks to the EMS-1000 staging API, which relays commands to devices through Azure IoT Hub.

> **Status:** Pilot · P0 (docs + setup). No app code yet.
> **Pilot users:** internal team only (Okey, Paul, Emeka).

## What the pilot app does

| | Feature |
|---|---|
| 🔐 | Sign in with your Microsoft (Entra) work account |
| 📋 | See the generators linked to you |
| 📊 | Live state: voltage, current, frequency, fuel, oil, temperature, starter battery, signal |
| ▶️ ⏹️ | Start / Stop with a confirmation step; Reset fault |
| 🔔 | Push alerts for critical faults, with per-alert on/off |
| 📈 | 24-hour chart |
| 📶 | Last-known state + "offline" badge when data is stale |

## Where to start

| If you want to… | Read |
|---|---|
| Understand the plan, phases and milestones | [docs/plan/mobile-app-plan.md](docs/plan/mobile-app-plan.md) |
| See how the whole system fits together | [docs/learning/L1-how-the-system-fits.md](docs/learning/L1-how-the-system-fits.md) |
| Know what the app sends to and gets from the API | [docs/api/pilot-api-contract.md](docs/api/pilot-api-contract.md) |
| See why things were decided | [docs/decisions/README.md](docs/decisions/README.md) |
| Learn the Git workflow used here | [docs/learning/L7-git-workflow.md](docs/learning/L7-git-workflow.md) |

## Related repos

| Repo | Role |
|---|---|
| [`ems1000-staging`](https://github.com/okeyf16/ems1000-staging) | Azure infrastructure (Terraform) + API + Functions — backend changes for this app go here |
| [`ems1000-device-sim`](https://github.com/okeyf16/ems1000-device-sim) | Python virtual device (`ems-sim-01`) used to test the app |
| [`iotgenmobile`](https://github.com/okeyf16/iotgenmobile) | Old Kivy prototype — reference only, retired at pilot end |

## How we work (short version)

1. Work on a branch → open a pull request → automated checks pass → merge to `main`.
2. Every feature is built as a thin slice that works end to end (phone → API → simulator).
3. Docs are updated in the same pull request as the code they describe.

Details: [L7 — Git workflow](docs/learning/L7-git-workflow.md).
