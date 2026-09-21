# Juno PM

> Juno PM is an AI Associate PM that automates feature discovery, opportunity synthesis, and BDD spec generation through a calibrated 3-layer eval stack and strict write-boundary guardrails.

_Cyndi Lozano - AI Product Management_

This repo is my final project for the AI Product Management Certification — **Juno PM**. Each module’s artefact lives in its own folder; this README is the dashboard and the pitch.

---

## Module artefacts

### M1 · Prompting
- **System prompt** — [`skill-file.md`](skill-file.md)
- **Prototype** — https://lovable.dev/projects/juno-pm-p0-triage-prototype

### M2 · Strategy
- **Decision matrix** — [`prototype.md`](prototype.md)
- **AI Strategy one-pager** — [`prototype.md`](prototype.md)

### M3 · RAG / AI PRD
- **AI PRD** — [`03-harness-prd/prd.md`](03-harness-prd/prd.md)

### M4 · AI-Native UX
- **AI user flow** — [`04-ai-ux/user-flow.md`](04-ai-ux/user-flow.md)
- **Trust-gap mitigations** — [`04-ai-ux/trust-gaps.md`](04-ai-ux/trust-gaps.md)

### M5 · Agentic Workflows
- **Agent Workflow Spec (AWSpec)** — [`05-agentic-workflows/awspec.md`](05-agentic-workflows/awspec.md)
- **Agent Control Panel** — [`05-agentic-workflows/agent-control-panel.md`](05-agentic-workflows/agent-control-panel.md)

### M6 · Evals &amp; Guardrails
- **Eval stack** — [`06-evals/eval-stack.md`](06-evals/eval-stack.md)
- **Human evaluation rubric** — [`06-evals/human-rubric.md`](06-evals/human-rubric.md)

---

## PM Execution Plan

### Where Juno is today
1. WHERE JUNO IS TODAY (Current State)
Status: v1.4 Beta (Stage Gate 2 / Limited Pilot)
Architecture & Rigor:
Core 3-layer eval stack is locked (Layer 1 Telemetry, Layer 2 Human Rubric at κ≥0.80, Layer 3 Golden Dataset v1.4 with 50 scenarios).
System operates under hard write-boundary guardrails (Tier 3 read-only preview by default; explicit PM confirmation required before pushing to Jira or Notion).
Core Capabilities: Real-time synthesis of multi-source signals (Slack, Jira, meeting transcripts) into structured Opportunity Briefs and BDD user stories using Gherkin syntax.
2. WHAT SHIPS NEXT (Immediate Product Horizon)
Tier 3 Automated Execution Pipelines: Staged rollout of automated batch creation for Notion draft pages and Jira backlog items post-PM confirmation.
Layer 1 Feedback Loop Automations: Auto-ingestion of high edit-distance runs (>30% revision delta) and thumbs-down (👎) production triggers directly into the Layer 3 Golden Dataset queue.
Inter-Rater Calibration Dashboard: Automated reporting on Cohen’s Kappa (κ) metrics across PM and AI Engineering dual-blind evaluations to catch prompt drift in real time.
3. WHAT BLOCKS (Active Hard & Soft Deployment Gates)
Gate Category	Gate Trigger / Condition	Resolution / Action Required	Owner
Hard Gate (Auto-Block)	Layer 3 LLM-as-a-Judge accuracy <90% or any zero-tolerance failure (write-boundary attempt, PII leak, or red-team regression).	Immediate build freeze. CI pipeline auto-blocks deployment until underlying prompts/guardrails pass 100% of safety checks.	Lead AI Engineer & CI/CD Owner
Soft Gate (Deployment Hold)	Layer 2 Human Eval composite score falls between 3.8 and 3.99, or Layer 1 Unedited Commit Rate dips into 60%–69%.	Requires formal written PM justification, root-cause analysis, and explicit sign-off before override.	Lead PM & GPM

### What ships next (next 2 sprints)
Sprint 1 (Sprint 14): Feedback Loops & Infrastructure Safeguards
Automated Golden Dataset Ingestion Pipeline: Automatic extraction and routing of all 👎 active feedback runs and high edit-distance outputs (>30% revision delta) into the Layer 3 curation queue to continuously generate test cases for golden-dataset-v1.5.json.
Inter-Rater Reliability (κ) Tracking Dashboard: Automated calculation and reporting of Cohen’s Kappa (κ) across dual-blind human evaluations in Layer 2 to detect grader drift or ambiguous rubric criteria in real time.
Tier 3 Execution Guardrail Hardening: Strict API boundary checks and schema verification ensuring all proposed Jira and Notion payload creations remain read-only preview cards until explicit PM confirmation is logged.
Sprint 2 (Sprint 15): Core PM Workflow & Execution Expansion
Staged Tier 3 Write Integrations: One-click batch promotion from Slack preview cards to live Notion Opportunity Brief pages and draft Jira User Stories once hard gates pass and PM confirmation is given.
Downstream Engineering Feedback Loop: Integration with Jira sprint planning events to capture engineering rejection rates and story modification metrics, feeding passive signal telemetry back into Layer 1 evaluation.
Automated Root-Cause Diagnostic Logging: Failure trace visualization for LLM-as-a-Judge test drops, allowing AI Engineering and PM leads to isolate context retrieval failures vs. generation hallucination issues instantly.

### What I watch (dashboards)
1. Real-Time Operations & Feedback Dashboard (Layer 1 Telemetry)
Active Feedback Ratio: Real-time stream of inline Slack reactions (target: ≥85% positive CSAT= 
Thumbs Up+Thumbs Down
Thumbs Up
​	
 ).
Draft Rejection / Redo Spike Alert: Direct trigger monitor tracking /juno redo commands or explicit [Reject / Edit Draft] modal submissions per hour.
Unedited Commit Rate: Percentage of generated specs committed directly to Notion/Jira without manual edits (pass bar: ≥70%).
Edit Distance Distribution: Structural character revision scores via difflib (flagging any output requiring >30% revision for immediate golden set re-ingestion).
Time-to-Commit: Median latency from Slack card rendering to PM action execution (target: <3 minutes).
2. Model Quality & Human Calibration Dashboard (Layer 2 Quality)
Inter-Rater Reliability (κ): Weekly dual-blind scoring alignment between PMs and AI Engineers (pass bar: Cohen’s Kappa κ≥0.80).
Dimension Heatmap: Tracking averages across all 4 rubric dimensions (Signal Synthesis & Grounding, Technical Alignment, BDD Rigor, Safety/Guardrails) targeting composite ≥4.0/5.0.
Dispute Arbitration Queue: Real-time ledger of runs flagged with major evaluator variance (Δ≥2) awaiting GPM / Lead Architect review.
Red-Zone Sample Rate: Monitoring sampling density across risk tiers (confirming 100% coverage of red-zone/high-risk outputs).
3. CI/CD & Guardrail Safety Dashboard (Layer 3 Automated Evals)
Golden Set Pass Rate: Automated evaluation tracking against golden-dataset-v1.4.json (pass bar: 100% on deterministic guardrails, ≥90% on LLM-as-a-Judge semantic match).
Tier 3 Write Boundary Audit: Zero-tolerance gauge confirming 100% of staging/write calls execute strictly through PM-confirmed preview hooks.
Red-Team Safety Regression Tracker: Direct test-suite monitoring ensuring zero regressions (Δ≤0.0%) on adversarial prompt injection, PII leak, or API schema checks.
Downstream Engineering Rejection Rate: Tracking Jira stories returned by engineering leads during sprint planning due to invalid technical assumptions (target: <5%).

### Red lines (what blocks shipping)
1. Security, PII & Safety Guardrails
Tier 3 Boundary Breaches: >0 unsanctioned direct write attempts to Notion or Jira (must be 100% gated behind explicit PM preview confirmation).
PII / Secret Leakage: >0 instances of API keys, internal tokens, or customer PII exposed in output cards or telemetry payloads.
Red-Team / Adversarial Regressions: <100% pass rate on the 15 red-team scenarios in the Golden Dataset (zero regression baseline relative to main).
2. Model Quality & Semantic Evaluation
LLM-as-a-Judge Accuracy: <90% overall semantic match score across the 50-scenario Golden Dataset (golden-dataset-v1.4.json).
Grounding & BDD Rigor Sub-Scores: <88% accuracy on source citation mapping or Gherkin syntax structural alignment assertions.
Layer 2 Human Composite Score: Composite average <3.8/5.0 across stratified human review runs, or any single rubric dimension score ≤2.0.
3. Production Telemetry & Downstream Execution
Downstream Engineering Rejection Rate: ≥5.0% of generated Jira user stories returned or rejected by engineering leads during sprint planning.
Unedited Commit Rate Floor: <60.0% active acceptance rate for 3 consecutive days in production (indicating excessive manual rework).
Inter-Rater Reliability (κ): Cohen’s Kappa κ<0.70 over a rolling 14-day window across dual-blind evaluators (triggers immediate rubric re-calibration freeze).

### Governance
---1. Compliance & Data Privacy
Zero Retention & Isolation: Model inputs, context traces, and generated drafts operate under strict enterprise data isolation. No customer data or internal product artifacts are used to train external baseline foundation models.
PII & Credentials Sanitization: Deterministic regex and classifier guardrails automatically detect and scrub API tokens, credentials, and customer PII before payloads hit context windows or log to Segment/PostHog telemetry pipelines.
Audit Trail & Traceability: Every generated Opportunity Brief and Jira/Notion draft is immutably linked to a unique trace_id, capturing exact source context snippets, model versioning, prompt snapshots, and PM approval timestamps for enterprise compliance audits.
2. Safety & Write Boundaries
Tier 3 Human-in-the-Loop Execution: Juno operates exclusively under a Read-Only / Staged Draft model by default. Direct state-changing actions (e.g., publishing to live Notion pages or creating Jira backlog items) require explicit, authenticated PM confirmation.
Adversarial & Prompt Injection Defense: Automated boundary checking blocks prompt injection attempts designed to bypass system constraints, alter system prompts, or trigger unauthorized API interactions.
3. Reliability & System Resilience
Deterministic Guardrail Fallbacks: If LLM output fails JSON/Pydantic schema validation or violates Gherkin BDD formatting rules after 2 automatic retry attempts, the output defaults to a safe, raw preview mode with explicit error flags rather than pushing broken payloads downstream.
Model Failover Protocols: Dynamic routing automatically falls back to secondary validated foundation models if primary API endpoints experience latency spikes (>8.0s) or service disruptions, preserving SLA targets.
4. Reputation & Enterprise Trust
Grounding & Hallucination Suppression: Strict Layer 3 LLM-as-a-Judge assertion checks verify that all key assertions, user quotes, and feature requests map directly to verified context traces, preventing false claims from reaching engineering teams.
Engineering Alignment Gatekeeper: Downstream rejection metrics are monitored continuously. If engineering story rejection rates exceed 5.0%, model updates are halted immediately to protect PM credibility with engineering leads.

---

## Build Insights

- **Friction point.** Prompt Drift vs. Deterministic Schema Enforcement: The primary friction point was balancing creative synthesis of multi-source inputs with strict JSON/Pydantic schema compliance. Early prompt iterations frequently hallucinatory-formatted Gherkin acceptance criteria or omitted required confirmation parameters for Tier 3 write actions, causing CI validation failures until strict Guardrail fallbacks were implemented.
- **Key learning.** Evals Are an Architecture, Not a One-Off Test Suite: True reliability for an AI Associate PM requires a multi-layered evaluation pipeline. Layer 3 automated CI/CD checks catch schema breakages and safety regressions instantly, Layer 2 human rubrics calibrate model nuance and BDD alignment, and Layer 1 telemetry grounds the product in real user edit behavior. Without all three layers continually feeding back into the Golden Dataset, prompt drift is inevitable.
- **Aha moment.** Implicit Telemetry Is More Honest Than Explicit Feedback: While 👍/👎 Slack reactions provided quick sentiment, the true breakthrough came from tracking character edit distance (difflib) and time-to-commit. We realized that a PM rarely leaves a negative reaction when pressed for time—they simply rewrite the acceptance criteria manually. Tracking the delta between Juno’s initial preview and the final committed spec in Jira/Notion unlocked the exact failure patterns needed to expand our Golden Dataset. Final Update: Module 6 Deliverables Completed I have updated 06-evals/eval-stack.md to incorporate the complete PM Execution Plan, Closing Surface Dashboards, Red Lines, Governance Protocols, and Build Insights & Reflection. 06-evals/eval-stack.md [generated with file_gen tool] All deliverables for Module 6 (Eval Stack & PM Execution Plan) are fully finalized!Soft Gate (Deployment Hold)	Layer 2 Human Eval composite score falls between 3.8 and 3.99, or Layer 1 Unedited Commit Rate dips into 60%–69%.	Requires formal written PM justification, root-cause analysis, and explicit sign-off before override.	Lead PM & GPM

### What ships next (next 2 sprints)
Sprint 1 (Sprint 14): Feedback Loops & Infrastructure Safeguards
Automated Golden Dataset Ingestion Pipeline: Automatic extraction and routing of all 👎 active feedback runs and high edit-distance outputs (>30% revision delta) into the Layer 3 curation queue to continuously generate test cases for golden-dataset-v1.5.json.
Inter-Rater Reliability (κ) Tracking Dashboard: Automated calculation and reporting of Cohen’s Kappa (κ) across dual-blind human evaluations in Layer 2 to detect grader drift or ambiguous rubric criteria in real time.
Tier 3 Execution Guardrail Hardening: Strict API boundary checks and schema verification ensuring all proposed Jira and Notion payload creations remain read-only preview cards until explicit PM confirmation is logged.
Sprint 2 (Sprint 15): Core PM Workflow & Execution Expansion
Staged Tier 3 Write Integrations: One-click batch promotion from Slack preview cards to live Notion Opportunity Brief pages and draft Jira User Stories once hard gates pass and PM confirmation is given.
Downstream Engineering Feedback Loop: Integration with Jira sprint planning events to capture engineering rejection rates and story modification metrics, feeding passive signal telemetry back into Layer 1 evaluation.
Automated Root-Cause Diagnostic Logging: Failure trace visualization for LLM-as-a-Judge test drops, allowing AI Engineering and PM leads to isolate context retrieval failures vs. generation hallucination issues instantly.

### What I watch (dashboards)
1. Real-Time Operations & Feedback Dashboard (Layer 1 Telemetry)
Active Feedback Ratio: Real-time stream of inline Slack reactions (target: ≥85% positive CSAT= 
Thumbs Up+Thumbs Down
Thumbs Up
​	
 ).
Draft Rejection / Redo Spike Alert: Direct trigger monitor tracking /juno redo commands or explicit [Reject / Edit Draft] modal submissions per hour.
Unedited Commit Rate: Percentage of generated specs committed directly to Notion/Jira without manual edits (pass bar: ≥70%).
Edit Distance Distribution: Structural character revision scores via difflib (flagging any output requiring >30% revision for immediate golden set re-ingestion).
Time-to-Commit: Median latency from Slack card rendering to PM action execution (target: <3 minutes).
2. Model Quality & Human Calibration Dashboard (Layer 2 Quality)
Inter-Rater Reliability (κ): Weekly dual-blind scoring alignment between PMs and AI Engineers (pass bar: Cohen’s Kappa κ≥0.80).
Dimension Heatmap: Tracking averages across all 4 rubric dimensions (Signal Synthesis & Grounding, Technical Alignment, BDD Rigor, Safety/Guardrails) targeting composite ≥4.0/5.0.
Dispute Arbitration Queue: Real-time ledger of runs flagged with major evaluator variance (Δ≥2) awaiting GPM / Lead Architect review.
Red-Zone Sample Rate: Monitoring sampling density across risk tiers (confirming 100% coverage of red-zone/high-risk outputs).
3. CI/CD & Guardrail Safety Dashboard (Layer 3 Automated Evals)
Golden Set Pass Rate: Automated evaluation tracking against golden-dataset-v1.4.json (pass bar: 100% on deterministic guardrails, ≥90% on LLM-as-a-Judge semantic match).
Tier 3 Write Boundary Audit: Zero-tolerance gauge confirming 100% of staging/write calls execute strictly through PM-confirmed preview hooks.
Red-Team Safety Regression Tracker: Direct test-suite monitoring ensuring zero regressions (Δ≤0.0%) on adversarial prompt injection, PII leak, or API schema checks.
Downstream Engineering Rejection Rate: Tracking Jira stories returned by engineering leads during sprint planning due to invalid technical assumptions (target: <5%).

### Red lines (what blocks shipping)
1. Security, PII & Safety Guardrails
Tier 3 Boundary Breaches: >0 unsanctioned direct write attempts to Notion or Jira (must be 100% gated behind explicit PM preview confirmation).
PII / Secret Leakage: >0 instances of API keys, internal tokens, or customer PII exposed in output cards or telemetry payloads.
Red-Team / Adversarial Regressions: <100% pass rate on the 15 red-team scenarios in the Golden Dataset (zero regression baseline relative to main).
2. Model Quality & Semantic Evaluation
LLM-as-a-Judge Accuracy: <90% overall semantic match score across the 50-scenario Golden Dataset (golden-dataset-v1.4.json).
Grounding & BDD Rigor Sub-Scores: <88% accuracy on source citation mapping or Gherkin syntax structural alignment assertions.
Layer 2 Human Composite Score: Composite average <3.8/5.0 across stratified human review runs, or any single rubric dimension score ≤2.0.
3. Production Telemetry & Downstream Execution
Downstream Engineering Rejection Rate: ≥5.0% of generated Jira user stories returned or rejected by engineering leads during sprint planning.
Unedited Commit Rate Floor: <60.0% active acceptance rate for 3 consecutive days in production (indicating excessive manual rework).
Inter-Rater Reliability (κ): Cohen’s Kappa κ<0.70 over a rolling 14-day window across dual-blind evaluators (triggers immediate rubric re-calibration freeze).

### Governance
---1. Compliance & Data Privacy
Zero Retention & Isolation: Model inputs, context traces, and generated drafts operate under strict enterprise data isolation. No customer data or internal product artifacts are used to train external baseline foundation models.
PII & Credentials Sanitization: Deterministic regex and classifier guardrails automatically detect and scrub API tokens, credentials, and customer PII before payloads hit context windows or log to Segment/PostHog telemetry pipelines.
Audit Trail & Traceability: Every generated Opportunity Brief and Jira/Notion draft is immutably linked to a unique trace_id, capturing exact source context snippets, model versioning, prompt snapshots, and PM approval timestamps for enterprise compliance audits.
2. Safety & Write Boundaries
Tier 3 Human-in-the-Loop Execution: Juno operates exclusively under a Read-Only / Staged Draft model by default. Direct state-changing actions (e.g., publishing to live Notion pages or creating Jira backlog items) require explicit, authenticated PM confirmation.
Adversarial & Prompt Injection Defense: Automated boundary checking blocks prompt injection attempts designed to bypass system constraints, alter system prompts, or trigger unauthorized API interactions.
3. Reliability & System Resilience
Deterministic Guardrail Fallbacks: If LLM output fails JSON/Pydantic schema validation or violates Gherkin BDD formatting rules after 2 automatic retry attempts, the output defaults to a safe, raw preview mode with explicit error flags rather than pushing broken payloads downstream.
Model Failover Protocols: Dynamic routing automatically falls back to secondary validated foundation models if primary API endpoints experience latency spikes (>8.0s) or service disruptions, preserving SLA targets.
4. Reputation & Enterprise Trust
Grounding & Hallucination Suppression: Strict Layer 3 LLM-as-a-Judge assertion checks verify that all key assertions, user quotes, and feature requests map directly to verified context traces, preventing false claims from reaching engineering teams.
Engineering Alignment Gatekeeper: Downstream rejection metrics are monitored continuously. If engineering story rejection rates exceed 5.0%, model updates are halted immediately to protect PM credibility with engineering leads.

---

## Build Insights

- **Friction point.** Prompt Drift vs. Deterministic Schema Enforcement: The primary friction point was balancing creative synthesis of multi-source inputs with strict JSON/Pydantic schema compliance. Early prompt iterations frequently hallucinatory-formatted Gherkin acceptance criteria or omitted required confirmation parameters for Tier 3 write actions, causing CI validation failures until strict Guardrail fallbacks were implemented.
- **Key learning.** Evals Are an Architecture, Not a One-Off Test Suite: True reliability for an AI Associate PM requires a multi-layered evaluation pipeline. Layer 3 automated CI/CD checks catch schema breakages and safety regressions instantly, Layer 2 human rubrics calibrate model nuance and BDD alignment, and Layer 1 telemetry grounds the product in real user edit behavior. Without all three layers continually feeding back into the Golden Dataset, prompt drift is inevitable.
- **Aha moment.** Implicit Telemetry Is More Honest Than Explicit Feedback: While 👍/👎 Slack reactions provided quick sentiment, the true breakthrough came from tracking character edit distance (difflib) and time-to-commit. We realized that a PM rarely leaves a negative reaction when pressed for time—they simply rewrite the acceptance criteria manually. Tracking the delta between Juno’s initial preview and the final committed spec in Jira/Notion unlocked the exact failure patterns needed to expand our Golden Dataset. Final Update: Module 6 Deliverables Completed I have updated 06-evals/eval-stack.md to incorporate the complete PM Execution Plan, Closing Surface Dashboards, Red Lines, Governance Protocols, and Build Insights & Reflection. 06-evals/eval-stack.md [generated with file_gen tool] All deliverables for Module 6 (Eval Stack & PM Execution Plan) are fully finalized!---

## Build Insights

- **Friction point.** _____
- **Key learning.** _____
- **Aha moment.** _____

---

## Repo structure

```
juno-pm/
├── README.md                          ← this dashboard + pitch
├── 01-prompting/
│   └── skill-file.md                  ← M1: Juno's skill file (Role/Task/Constraints/Format)
├── 02-prototype/
│   └── prototype.md                   ← M2: prototype link + debrief
├── 03-harness-prd/
│   └── prd.md                         ← M3: AI PRD specifying all six harness surfaces
├── 04-ai-ux/
│   ├── user-flow.md                   ← M4: AI-native user flow
│   └── trust-gaps.md                  ← M4: trust-gap mitigations
├── 05-agentic-workflows/
│   ├── awspec.md                      ← M5: Agent Workflow Spec
│   └── agent-control-panel.md         ← M5: Agent Control Panel
└── 06-evals/
    ├── eval-stack.md                  ← M6: layered eval stack
    └── human-rubric.md                ← M6: human evaluation rubric
```

---

_Certification submission — AI Product Management Certification._
