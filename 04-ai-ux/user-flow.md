# AI-Native User Flow · Juno

## Entry Point

### Where and why the user reaches for Juno
* **Primary Surface:** Slack `#product-escalations` channel and direct message interface (`@Juno`).
* **Trigger Event:** A Product Manager at RocketShip is overwhelmed by "Signal Collapse"—a sudden influx of un-triaged customer feedback, P0 support ticket escalations, or sales call notes during sprint planning.
* **Core Need:** The PM needs to rapidly distill unstructured feedback into actionable user stories and technical acceptance criteria without spending hours manually parsing threads and cross-checking engineering constraints.

---

## The Flow

* **Step 1 — Signal Trigger (User)**
  * The PM tags `@Juno` in a Slack escalation thread or pastes a raw Zendesk/Gong transcript into a private scratch pad with the prompt: *"Synthesize this feedback thread into a PRD draft for sprint review."*
* **Step 2 — Context Retrieval & Strategy Mapping (Juno)**
  * Juno intercepts the request, executes `read_customer_tickets()`, and queries both the RocketShip Product Strategy One-Pager and Engineering Architecture Constraints using a RAG pipeline.
* **Step 3 — Interactive Draft Generation (Juno)**
  * Juno posts a structured Slack Card displaying a 3-bullet insight summary, a draft user story (*As a... I want... So that...*), 'Given-When-Then' acceptance criteria, and identified delivery risks.
* **Step 4 — Inline Review & Refinement (User)**
  * The PM inspects the generated card, verifies inline source citations (`[Source: Zendesk #1042]`), checks verifiability badges, and adjusts criteria or asks for refinements directly in the thread.
* **Step 5 — Controlled State Change (Juno & User)**
  * Upon explicit PM button click (`[Push to Notion Draft]`), Juno writes the spec into the team's shared Notion scratch space and generates a draft Jira issue link for final human sign-off.

---

## AI Moments

### Where the AI acts, what it shows, and how the user stays in control

#### 1. Signal Synthesis & Opportunity Framing
* **Where the AI Acts:** When processing raw customer transcripts or Slack escalation threads.
* **What it Shows:** A concise 3-bullet insight summary with interactive inline citations (`[Source: Gong Call #882]`) mapping directly back to original feedback excerpts.
* **User Control (Confirm/Edit):** Hovering over citations displays source snippets; the PM can click `[Refine Summary]` to tweak focus before drafting specs.

#### 2. Acceptance Criteria Generation
* **Where the AI Acts:** When drafting technical user stories and BDD criteria.
* **What it Shows:** 'Given-When-Then' scenarios tagged with a **Verifiability Badge** (🟢 *Verified against Eng Constraints* vs. 🟡 *Unverified Assumption*).
* **User Control (Edit/Undo):** The PM can click any text field inline to edit criteria before committing, or click `[Undo Draft]` to wipe generated criteria instantly.

#### 3. Permission-Gated Delivery Execution
* **Where the AI Acts:** When transferring drafts into external tools (Notion / Jira).
* **What it Shows:** An interactive Slack action card featuring explicit primary and secondary control buttons (`[Push to Notion Draft]`, `[Create Draft Jira Issue]`, `[Discard]`).
* **User Control (Confirm Gate):** Juno is strictly prohibited from auto-mutating shared team databases. No write operation executes without an explicit human button click.

---

## Fallbacks

### What happens when Juno is unsure, wrong, or offline

* **When Juno is Unsure (Low Confidence / Ambiguous Context):**
  * *Behavior:* Juno halts automatic drafting, presents verified facts from context, and explicitly asks the PM 1–2 clarifying questions (e.g., *"I found conflicting constraints between the Q3 strategy and current API rate limits. Should I prioritize microservice migration or legacy DB support?"*).
* **When Juno is Wrong (Uncited / Hallucinated Requirements):**
  * *Behavior:* Any requirement or criteria statement that cannot be traced to a strategy doc or ticket ID is automatically flagged with a prominent warning badge: `[Unverified - Requires PM Review]`.
* **When Juno is Offline (Tool Execution Error / API Failure):**
  * *Behavior:* If Notion/Jira APIs time out or tool calls hit 3 consecutive errors, Juno gracefully fails back to plain text, delivering the draft directly in Slack with the message: *"Juno could not connect to Notion workspace. Here is your raw Markdown draft to copy manually."*