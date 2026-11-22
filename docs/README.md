# 📚 Docs index

```
docs/
├── plan/        🗺️  What we're building, in which order, and why
├── api/         🔌  Exact requests/responses between the app and the API
├── decisions/   ⚖️  Short records of important decisions
└── learning/    🎓  Visual 80/20 learning pages (one per topic)
```

| Folder | Contents | Updated when |
|---|---|---|
| [plan/](plan/mobile-app-plan.md) | Phases, scope, milestones, risks | Scope or milestones change |
| [api/](api/pilot-api-contract.md) | Pilot API contract (draft → agreed in P0) | Any endpoint changes |
| [decisions/](decisions/README.md) | Decision log + template | A choice is made that's costly to reverse |
| [learning/](learning/README.md) | L1–L8 learning pages | With the milestone that introduces the topic |

**Rule of thumb:** if you had to ask "why is it like this?", the answer belongs in `decisions/`. If you had to ask "how does this work?", it belongs in `learning/`.
