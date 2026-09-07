# AI Agent PRD Template

_PRD template for AI agent features and products — systems that reason, use tools, and act on a user's behalf. For non-agentic AI features (classification, autocomplete, a single generation step), use only the sections that apply; for fully deterministic features use [prd-template.md](prd-template.md)._

> **How to use:** Copy into `.productmap/00_company/product/<initiative>/prd-<agent>-YYYY-MM-DD.md`. Delete guidance in italics. Keep dates absolute (`YYYY-MM-DD`). Link a tech spec / [ADR](adr-template.md) for architecture decisions — this doc owns the **what/why**, not the **how**.

---

## 0. Document control

| Field | Value |
|---|---|
| Status | Draft / In review / Approved |
| Owner (PM) | |
| Eng / ML lead | |
| Design lead | |
| Last updated | YYYY-MM-DD |
| Linked docs | Tech spec, ADRs, eval plan, design file |

---

## 1. Summary

_2–4 sentences a busy executive can read: the problem, what the agent does, the target outcome, the biggest risk._

- **Problem:**
- **Agent in one sentence:** _"An agent that <does X> for <user> by <using tools Y> so that <outcome Z>."_
- **Primary success metric & target:**
- **Biggest risk:**

## 2. Problem & opportunity

- **Who is impacted** (segment, persona, internal role) and **why now**.
- **Evidence** — links to research, tickets, metrics (`.productmap/10_data/...`), not unattributed claims.
- **Why an agent?** _Agents add cost, latency, and failure modes. Justify why a workflow, a form, or a single LLM call is not enough — e.g. multi-step reasoning, tool orchestration, or handling long-tail variability._
- **Cost of doing nothing:**

## 3. Users, jobs & scenarios

- **Primary persona(s)** and their job-to-be-done in this flow.
- **Sample prompts / triggering events** — _5–10 realistic inputs the agent must handle, including messy ones. These seed the eval set later._

| # | Scenario / sample input | Expected agent behavior | Priority |
|---|---|---|---|
| 1 | | | P0 |

- **Out-of-scope inputs** the agent must gracefully refuse or route elsewhere.

## 4. Goals, non-goals & success metrics

### Goals
_Measurable or at least observable._

### Non-goals
_Critical for agents — an agent will happily attempt anything not explicitly excluded. State boundaries positively ("the agent does not issue refunds")._

### Success metrics

| Metric | Type | Baseline | Target | Guardrail (must not regress) |
|---|---|---|---|---|
| Task success rate (end-to-end) | Primary | | | |
| Containment / escalation rate | Secondary | | | |
| p95 latency per task | Guardrail | | | |
| Cost per completed task | Guardrail | | | |
| User trust (CSAT / thumbs / retention) | Secondary | | | |

## 5. Agent definition

### 5.1 Role & capabilities (MVP)

- **Role:** _What the agent is (e.g. "support triage agent"), its persona/tone, and what it presents itself as to users._
- **Capabilities in scope:** _checklist — Q&A over knowledge base, retrieval (RAG), API/tool calls, file handling, multi-turn conversation, structured output, handoff to human, etc._
- **Capabilities explicitly out of scope for this release:**

### 5.2 Autonomy level & decision boundaries

_Where does this agent sit on the spectrum, per action type? Start narrow; expand as reliability is proven._

| Action | Autonomy level | Rationale |
|---|---|---|
| e.g. Draft reply | Suggest only (human sends) | |
| e.g. Look up order status | Act autonomously | Read-only, reversible |
| e.g. Issue refund > $500 | Ask / escalate to human | Irreversible, financial |

- **Escalation & handoff rules:** _When must the agent stop and hand off (confidence threshold, sensitive topic, user request, N failed attempts)? What context travels with the handoff?_
- **What the agent may never do:** _hard prohibitions, regardless of user instruction._

### 5.3 Tools & integrations

_The permission surface is the primary safety control — minimum permissions, expanded deliberately._

| Tool / API | Action | Read/Write | Side effects & reversibility | Approval required? | Rate/budget limit |
|---|---|---|---|---|---|
| | | | | | |

### 5.4 Context, knowledge & memory

- **Knowledge sources** (docs, DBs, retrieval indexes) and their freshness/ownership.
- **Memory:** _what persists across turns/sessions, retention period, user visibility & deletion._
- **Data access boundaries:** _tenant isolation, PII the agent can see vs. must never see, redaction._

## 6. User experience

- **Entry points & invocation** (proactive vs. user-initiated).
- **Visibility of agent work:** _streaming, plan/step display, citations, "why did you do that" affordances._
- **User control:** _interrupt, undo, edit-before-send, feedback (👍/👎 + reason)._
- **Failure & fallback UX:** _what the user sees on low confidence, tool failure, refusal, timeout — degraded mode must be designed, not accidental._
- **Disclosure:** _how users know they're interacting with AI; disclaimers required by legal/policy._
- States to design: empty, loading/thinking, partial success, error, escalated-to-human.

## 7. Quality bar & evaluation

_Define "good" before building — if you can't measure success you can't ship responsibly._

### 7.1 Offline evals (pre-launch gate)

- **Golden set:** _N representative tasks from §3, incl. edge cases; where it lives; who owns updates._
- **Grading method:** _programmatic checks / LLM-judge rubric / human review — and the rubric itself (correctness, completeness, tone, safety)._
- **Agent-specific metrics:** _tool-choice correctness, argument validity, step count / looping, unnecessary-action rate, policy compliance._
- **Ship bar:** _e.g. ≥ X% task success on golden set, 0 critical safety failures._

### 7.2 Online evals (post-launch)

- Task success, escalation rate, user feedback signals, sampled human review cadence.
- **Regression protocol:** _evals re-run on every prompt/model/tool change; silent upstream model updates are detected how?_

### 7.3 Red teaming & abuse

- Prompt injection (direct + via retrieved content/tool results), jailbreaks, data exfiltration attempts, harmful-content elicitation.
- Who runs it, when, and the bar for launch.

## 8. Guardrails, safety & compliance

- **Input checks:** _injection screening, off-topic/abuse filtering, input validation._
- **Action checks (pre-execution):** _allowlisted tools, argument validation, spend/rate caps, approval gates from §5.2._
- **Output checks:** _grounding/citation requirements, PII redaction, moderation, refusal templates._
- **Runaway protection:** _max steps per task, max cost per task, loop detection, global kill switch._
- **Privacy & compliance:** _prompt/output logging policy vs. PII constraints, data retention & deletion, regional constraints, audit trail for actions taken; extra scrutiny for regulated domains (medical/financial/legal)._

## 9. Failure modes & degraded behavior

| Failure mode | Likelihood | Impact | Detection | Mitigation / fallback UX | Owner |
|---|---|---|---|---|---|
| Hallucinated fact / citation | | | | | |
| Wrong tool call (irreversible action) | | | | | |
| Prompt injection via retrieved content | | | | | |
| Tool/API outage mid-task | | | | | |
| Looping / runaway cost | | | | | |
| Confidently wrong answer | | | | | |

## 10. Non-functional requirements

- **Latency:** _p50/p95 per interaction and per full task; streaming expectations._
- **Cost envelope:** _token budget per task, monthly ceiling, caching/batching strategy, unit-economics link ([unit-economics](../08_frameworks/)) — cost per task vs. value per task._
- **Reliability:** _SLO, retries, idempotency for tool calls, dedup._
- **Scalability & rate limits** (yours and upstream model provider's).
- **Security:** _tool auth model (agent acts as user vs. service account), secrets handling, least privilege._

## 11. Model & architecture notes

_Summary only — details live in the tech spec / ADRs. Model choice follows from requirements, not the other way around._

- **Model(s) & selection criteria:** _quality on evals, latency, cost, context window, tool-use reliability; fallback model._
- **Orchestration shape:** _single agent vs. multi-agent, planner/executor, workflow-with-LLM-steps — link ADR._
- **Prompt management:** _prompts versioned like code; owner; review process; changelog in appendix._

## 12. Monitoring & incident response

- **Tracing:** _every task traceable end-to-end (inputs, steps, tool calls, outputs) within logging policy._
- **Dashboards & alerts:** _task success, escalation, cost, latency, safety-flag rate, drift on eval samples._
- **Kill switch & rollback:** _how to disable the agent or roll back to a prior prompt/model version; who can pull it; rollback triggers with thresholds._
- **Incident playbook:** _severity levels for agent misbehavior; user comms for wrong actions taken._

## 13. Rollout plan

_Progressive autonomy — earn trust in stages._

| Phase | Audience | Autonomy | Exit criteria | Date |
|---|---|---|---|---|
| 0. Shadow mode | Internal — agent runs, output not shown/executed | None | Eval bar met on live traffic | YYYY-MM-DD |
| 1. HITL beta | N% users / internal | Suggest-only, human approves actions | Success ≥ X%, escalation ≤ Y% | YYYY-MM-DD |
| 2. Limited GA | | Autonomous for low-risk actions | Guardrail metrics stable | YYYY-MM-DD |
| 3. GA | | Target autonomy from §5.2 | | YYYY-MM-DD |

- Feature flags, comms plan, support/success enablement (help docs, known sharp edges).

## 14. Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner | By (YYYY-MM-DD) |
|---|---|---|---|---|---|
| | | | | | |

## 15. Dependencies

_Teams, services, model providers, legal/trust reviews — with owners and dates._

## 16. Open questions & decision log

| Question / decision | Owner | Due / decided (YYYY-MM-DD) | Outcome |
|---|---|---|---|
| | | | |

---

## Appendix

- **A. System prompt (versioned):** _v0 draft + changelog: version, date, change, eval delta._
- **B. Eval set & rubric:** _link to golden set under `.productmap/10_data/<initiative>/`._
- **C. Glossary:** _5–12 terms max — "task", "session", "escalation", "containment", autonomy level names._
- **D. What changed:** _dated entries (`YYYY-MM-DD`) when scope shifts post-review._

---

### Review checklist (gate before "ready for eng")

1. Non-goals and hard prohibitions are explicit — nothing left to inference.
2. Every tool lists side effects, reversibility, and its approval gate.
3. Autonomy level is set per action, with escalation rules and handoff context.
4. Golden set + ship bar defined **before** build starts.
5. Failure-mode table covers injection, wrong irreversible action, and runaway cost.
6. Cost per task has a ceiling and a dashboard.
7. Kill switch and rollback path exist and are owned.
8. Rollout starts in shadow/HITL mode with measurable exit criteria.
9. Logging policy reconciled with PII constraints; audit trail for actions.
10. Open questions have owners and absolute due dates.
