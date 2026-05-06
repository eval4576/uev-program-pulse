# UEV Program Pulse

**4-Stage AI Program Intelligence Pipeline for Ford EVDC**

Built by [Motionova Labs](https://github.com/eval4576) · Powered by Anthropic Claude API

**[→ Live Demo](https://eval4576.github.io/uev-program-pulse)** · Opens instantly with pre-loaded program analysis · No API key required

---

## What It Does

UEV Program Pulse takes raw program inputs from across Ford's Electric Vehicle Development Center workstreams — Jira sprint summaries, standup notes, risk log updates, engineering change requests, supplier communications — and runs them through a four-stage linear agentic pipeline. Each stage receives the prior stage's structured JSON output as explicit context before generating its analysis. The chain compounds.

The output is a workstream RAG status view, a ranked action list with owners and deadlines, a program Drift Index, and a copy-ready leadership brief — generated in under two minutes from raw, unstructured inputs.

---

## Pipeline Architecture

```
Raw Inputs
    │
    ▼
Stage 01 — Signal Ingest & Classification
    │  Classifies every signal by type, workstream, confidence, and source
    │  Flags data gaps explicitly
    │  Output: structured JSON with workstream signal inventory
    │
    ▼
Stage 02 — Drift Detection Engine
    │  Reads Stage 01 JSON — does not re-process raw input
    │  Produces RAG status per workstream
    │  Detects schedule drift, missing owners, escalation gaps
    │  Surfaces cross-stream dependencies with cascade risk
    │  Output: structured JSON with drift analysis
    │
    ▼
Stage 03 — Action Intelligence
    │  Reads Stage 02 JSON
    │  Generates ranked action list: urgency, owner, deadline, consequence
    │  Computes Program Drift Index (0–100)
    │  Output: structured JSON with prioritized action set
    │
    ▼
Stage 04 — Executive Brief Generation
    │  Reads structured summary of Stages 01–03
    │  Generates copy-ready leadership brief
    │  Standard format or VP Summary (one-page) format
    │  Timestamped and attributed
    │  Output: formatted plain-text brief, downloadable as .txt
```

**Key architectural decision:** Each stage receives only the prior stage's structured output as context — not the raw data again. This forces the model to reason from what was found, not re-read the source. The analysis compounds rather than repeats.

---

## Why This Exists

Ford's Long Beach EVDC is running the UEV platform program across three locations — Long Beach, Dearborn, and Palo Alto — with 830+ engineers, a hard production date in Louisville, and parallel assembly streams that have hard convergence points. The coordination overhead is real. Status visibility across that distributed structure today lives in Jira tickets, Slack threads, and weekly decks that are stale before leadership reads them.

This tool was built to demonstrate what it looks like to treat program operations as an engineering problem: prototype and build AI agents to automate reporting, status visibility, dependency tracking, and routine documentation.

---

## Example Scenarios

Four Ford EVDC-specific scenarios are pre-loaded and runnable with one click:

**UEV Module Integration** — A realistic week of parallel module assembly signals across Software, Vehicle Integration, Risk and Supply Chain, and ECR workstreams. Includes the NACS port location decision risk, TXO connector supplier slip, and Dearborn NVH queue conflict.

**Software Milestone Review** — Jira sprint status across ZCU integration, OTA pipeline, V2I comms, Dearborn sync items, test infrastructure conflicts, and vendor delivery delays.

**LB / Dearborn Sync** — Interface coordination status between the Long Beach skunkworks and Dearborn. Six open items exceeding two-week SLA. Tests the cross-stream dependency detection.

**Supplier Risk Event** — Ad-hoc escalation scenario: TXO connector slip, TDK display vendor delay, NACS harness decision window closing. Demonstrates the pipeline under time pressure.

---

## Tech Stack

- Vanilla HTML, CSS, JavaScript — zero dependencies, zero build step
- Anthropic Claude API (`claude-sonnet-4-20250514`)
- GitHub Pages deployment
- Token budgets: Stages 01–03 at 1,400 tokens, Stage 04 at 1,600 tokens (brief is the deliverable)

No backend. No database. No framework. The entire tool is a single HTML file.

---

## Setup

**Option 1 — Live demo (no API key)**

Open the live tool: **[eval4576.github.io/uev-program-pulse](https://eval4576.github.io/uev-program-pulse)**

The tool opens instantly with the UEV Module Integration scenario pre-loaded and all four stages already rendered — RAG status, drift analysis, ranked action list, and executive brief. No API key, no setup, no friction. Explore the full pipeline output immediately.

**Option 2 — Live pipeline with your Anthropic API key**

1. Open `index.html` in a browser
2. Enter your Anthropic API key in the inline field above the Run button
3. Load a scenario or paste your own program inputs
4. Hit Run — all four stages execute sequentially

Your API key is used only in your browser session. It is never stored, logged, or transmitted beyond the Anthropic API call.

**Option 3 — Embed key for local demo use**

Open `index.html` in a text editor. Find:

```javascript
const CONFIG = {
  API_KEY: '',
```

Replace the empty string with your key. Save. Open locally. The tool launches directly with no key prompt.

Do not push a version with your embedded key to a public repository.

---

## Output Formats

**Standard Brief** — Full program pulse brief with executive summary, workstream RAG status, critical and important action lists, positive signals, and open decisions required.

**VP Summary** — One-page leadership format. Situation, required actions with owners and deadlines, decisions needed from leadership, what is on track, and recommended next review timing.

Both formats include a timestamp and "Generated by UEV Program Pulse · Motionova Labs" attribution. Both are downloadable as a .txt file.

---

## Related Projects

This tool is part of the Motionova Labs AI PM Toolkit:

- [APEX](https://github.com/eval4576/apex-agent) — 6-stage autonomous product reasoning agent
- [AI PRD Generator](https://github.com/eval4576/ai-prd-generator) — Structured PRD generation from problem descriptions
- [PSPS EOC Dashboard](https://github.com/eval4576/psps-eoc-dashboard) — Operational decision intelligence for grid operators
- [AI Metrics Dashboard](https://github.com/eval4576) — Program metrics and delivery health tracking

---

## Author

**Eddie Valdivia** — Technical Program Manager · AI Builder · Long Beach, CA

[linkedin.com/in/eddievaldivia](https://linkedin.com/in/eddievaldivia) · [github.com/eval4576](https://github.com/eval4576)

---

*Built as a demonstration of AI-native program operations tooling for complex, multi-disciplinary programs. The scenarios and program context are based on publicly available information about Ford's Electric Vehicle Development Center.*
