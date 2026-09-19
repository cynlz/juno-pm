# AI PRD · Juno

Module 3 · Harness / AI PRD. The AI product requirements doc specifying all six harness surfaces, built with the M3 · AI PRD Builder.

---

## Problem & user

### The user problem and who has it
Product Managers (PMs) and Product Leaders at RocketShip face severe **Signal Collapse**—the operational bottleneck where high-volume, fragmented customer signals (Zendesk support escalations, Gong sales calls, Slack triage threads) are disconnected from strategic goals and engineering constraints. 

**Who has it:**
* **Product Managers:** Spend 15+ hours per week manually triaging customer feedback, copying transcripts between systems, and writing acceptance criteria from scratch, risking missed delivery deadlines or missed high-ARR customer escalations.
* **Engineering Leads:** Receive vague, ungrounded feature requests containing unverified technical assumptions that break API rate limits or violate database schemas during sprint execution.

---

## The harness

| Surface | Specification |
| :--- | :--- |
| **01 Context** | Ingests active quarterly OKRs, RocketShip Strategy One-Pager, Engineering Architecture Constraints Document, and a rolling 90-day Zendesk/Gong/Slack feedback index. |
| **02 Tools** | `search_strategy_docs`, `read_customer_tickets`, `check_eng_constraints`, `draft_prd_spec`, `push_to_notion`, `create_jira_issue`. |
| **03 Loop** | Hard turn ceiling of **5 turns per request**. Escalates immediately on 3 consecutive tool errors or confidence < 70%. |
| **04 Memory** | Thread-scoped execution memory; user/team preference overrides persist in key-value store with a 90-day TTL. |
| **05 Permissions** | **Read:** `AUTO` · **Draft:** `AUTO` · **Write:** `CONFIRM` (Human Gate) · **Send:** `BLOCKED`. |
| **06 Verification** | Automated pre-output AST parser checks JSON schema, enforces BDD `Given-When-Then` formatting, and validates inline citation tags. |

---

## 01 Context · Data Requirements

* **Required sources:** 
  1. *RocketShip Q3 Strategy One-Pager & Active OKRs* (Notion/Confluence).
  2. *Engineering Architecture Constraints & API Limits Document* (GitHub Markdown / OpenAPI Specs).
  3. *Zendesk Customer Support Tickets & Gong Sales Call Transcripts* (90-day rolling vector index).
  4. *Active Slack Escalation Thread History* (`#product-escalations`).
* **Deliberate exclusions:** 
  * *Production Database PII / HR Salary Data:* Left out to prevent security/privacy leaks and strictly contain context scope to product delivery signals.
  * *Unfiltered Raw Code Repositories:* Excluded to prevent context window bloat; replaced by curated architecture summary specs.
* **SLA of truth:** Changes to strategy docs or engineering constraints re-index into vector storage (`pgvector`) within **< 15 minutes**.
* **When a source is unreachable:** Degrade gracefully with explicit warning banner on Slack output (e.g., `[Warning: Engineering Constraints DB Unreachable - Technical Feasibility Unverified]`). Never silently fail or invent data.

---

## 02 Tools · System Capabilities

* **The verb list:**
  * `search_strategy_docs(query)` — **Read**
  * `read_customer_tickets(filter_criteria)` — **Read**
  * `check_eng_constraints(topic)` — **Read**
  * `draft_prd_spec(payload)` — **Draft**
  * `push_to_notion(page_id, content)` — **Write**
  * `create_jira_issue(project_id, issue_data)` — **Write**
* **Deliberate omissions:**
  * `broadcast_customer_release_notes()` or `auto_reply_zendesk()` — **Send**. Omitted to prevent unvetted AI communications from reaching external customers without human review.

---

## 03 Loop · AI Costs & Latency

* **Turn ceiling:** Maximum **5 tool turns** per user execution request.
* **Escalation trigger:** Loop halts and hands back to a human PM if:
  1. Juno reaches 3 consecutive tool invocation errors.
  2. RAG context produces conflicting directives (e.g., Q3 OKRs directly contradict API rate limits).
  3. ReAct model output receives a self-assessed confidence score **< 70%**.
* **Latency and cost target:** 
  * **P95 Latency:** Under **8 seconds** per completed task.
  * **Per-Task Cost Ceiling:** Under **$0.12** per completion (~GPT-4o / Claude 3.5 Sonnet token budget).

---

## 04 Memory · Data Requirements

* **What persists, at what scope:**
  * **Turn Scope:** Intermediate tool execution outputs and RAG context chunks.
  * **Session Scope:** Active Slack thread state and current scratchpad PRD draft.
  * **User / Team Scope:** Preferred PRD template styles and team default Notion target folders.
* **Expiry:** Session memory expires **24 hours** post-task. User preference overrides persist with a **90-day TTL**.
* **Write rules:** **Human explicitly outranks the model.** If a human edits a generated BDD criterion or overrides a risk score, Juno locks the human edit permanently and updates session memory.

---

## 05 Permissions · AI Risks & Mitigations

| Side-effect class | Tier | Justification |
| :--- | :--- | :--- |
| **Read** | **Auto** | Zero blast radius. Querying strategy docs and customer tickets provides required RAG context without mutating external systems. |
| **Draft** | **Auto** | Low blast radius. Generating user stories in private Slack previews allows rapid PM iteration before committing. |
| **Write** | **Confirm** | High blast radius. Creating Jira issues or publishing Notion docs affects team backlogs. Requires explicit PM button click (`[Push to Notion Draft]`). |
| **Send** | **Blocked** | Critical blast radius. Permanently disabled in V1 to eliminate the risk of automated messaging to external enterprise clients. |

---

## 06 Verification · AI Testing & Measurement

* **The check before output ships:** AST parser and Regex validator verify that:
  1. Output matches standard JSON/Markdown PRD schema.
  2. All user stories feature BDD `Given-When-Then` formatting.
  3. Every technical requirement includes an inline source citation tag (`[Source: ID]`) or a `[Unverified Assumption]` badge.
* **Failure behaviour:** If verification fails, Juno halts the card render and posts a fallback notification in Slack: *"Draft generated but failed verification (missing citations). Click [Refine] to re-run verification."*

---

## Eval plan

* Stub. Module 6 fills this in: Golden set of 50 production escalation scenarios, 100% pass threshold on Layer 1 code checks, $\ge 0.85$ faithfulness threshold on Layer 2 LLM-as-a-judge evals, and a bi-weekly regression cadence.

---

## Out of scope

* Automated code generation or GitHub Pull Request creation.
* Direct external customer email or Zendesk ticket response dispatching.
* Automated employee compensation or financial revenue projection modeling.
* Any tool or action classified as **Blocked** under the Tier 3 permission model.