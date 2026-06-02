# ACMS — AI Context Memory Schema

**Compress any project into a single string. Paste it into a fresh AI chat to resume instantly — no context lost.**

🔗 **[Live Demo → ciaran11221.github.io/ACMS](https://ciaran11221.github.io/ACMS/)**

---

## The Problem

AI chat windows have a context limit. On long projects you hit it fast — the AI forgets earlier decisions, loses track of what's done, and you waste tokens re-explaining things you already covered.

The naive fix is to dump a summary file into a new chat. It's slow, lossy, and still uses hundreds of tokens.

## The Solution

ACMS compresses your entire project state — stack, tasks, decisions, blockers, next steps — into a single compact string using a structured encoding schema. A fresh AI chat decodes it instantly and resumes exactly where you left off.

```
ACMS▸[P=project,G=goal,S=stack,T=id:task,D=done,C=current,K=decision,N=next]|v1|P:ResearchOps|G:Multi-agent-research-pipeline|S:python,anthropic-sdk,tkinter|T:A1=setup,A2=orchestrator,B1=researcher,B2=analyst|D:A1-2,B1|C:B2|K:api=raw-anthropic,agents=sequential|N:C1,C2|TS:20260602
```

That's ~150 tokens. A prose equivalent is 2,000+. **~15x compression with zero information loss.**

---

## How It Works

1. **Paste a GitHub URL** or **upload any project file** (README, notes, spec)
2. **Describe what you want to do next** (optional)
3. Click **Generate** — Claude reads the project and encodes it into an ACMS string
4. **Copy and paste** the string into any fresh Claude chat
5. The new chat decodes it and resumes your project immediately

---

## The Schema

| Field | Meaning |
|-------|---------|
| `P`   | Project name |
| `G`   | One-sentence goal |
| `S`   | Tech stack |
| `T`   | Task legend (phased IDs: A=setup, B=core, C=polish, D=deploy) |
| `D`   | Done task IDs (compressed: A1,A2,A3 → A1-3) |
| `C`   | Current task in progress |
| `X`   | Blockers (`!unresolved`, `→resolved-by`) |
| `K`   | Key decisions a fresh AI can't infer from the stack |
| `N`   | Next tasks |
| `TS`  | Date encoded |

---

## Why This Matters

- **No backend** — runs entirely in the browser
- **No install** — open the URL and use it
- **Works on any project** — code, research, writing, business plans
- **Any AI** — the string is plain text, paste it anywhere
- **Your key, your data** — API key stored locally in your browser only

---

## Tech

- Pure HTML/CSS/JS — single file, no dependencies
- Anthropic API (claude-haiku) for encoding
- GitHub raw content for README fetching
- Hosted free on GitHub Pages

---

## Concepts Demonstrated

| Concept | Where |
|---------|-------|
| Context compression via structured encoding | ACMS schema design |
| Direct browser → Anthropic API calls | `callClaude()` in index.html |
| GitHub raw content fetching (no auth) | `fetchGitHubRepo()` in index.html |
| Graceful degradation (no README fallback) | URL-only encoding path |
| localStorage for stateless key management | `saveKey()` in index.html |

---

## Author

**Ciaran Brennan** — Galway, Ireland  
Building agentic AI systems on the Anthropic API.

[GitHub](https://github.com/Ciaran11221) · [ResearchOps](https://github.com/Ciaran11221/ResearchOps)

---

## License

MIT
