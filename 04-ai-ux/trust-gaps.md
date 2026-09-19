# Trust-Gap Mitigations · Juno

## Trust Gaps

| Gap | Where it shows up | User cost | Mitigation |
| :--- | :--- | :--- | :--- |
| **Hallucination** | Generated PRD acceptance criteria and technical feasibility checks. | High — Engineering builds the wrong requirements or runs into technical dead-ends during sprint execution. | **Verifiability Badges & Citation Checks:** Tag every requirement with a status badge (`🟢 Verified` vs. `🟡 Unverified Assumption`). Block auto-publishing if key criteria lack backing citations. |
| **Opacity (no "why")** | Priority risk scoring and feature opportunity synthesis in Slack previews. | Medium — PMs distrust Juno's recommendations and ignore AI outputs, reverting to manual triage. | **Inline Source Citations & CoT:** Every insight includes interactive source tags (`[Source: Zendesk #1042]`) that reveal original feedback snippets and Chain-of-Thought reasoning on hover. |
| **No user control** | Multi-system state mutations (e.g., creating Jira tickets or publishing Notion docs). | High — Unvetted specs or premature issues corrupt team backlogs and trigger team panic. | **Permission-Gated Action Buttons:** Hard human-in-the-loop gate (Tier 3 permission). Juno presents action cards with explicit `[Push to Notion]` or `[Edit Criteria]` buttons; zero state changes occur without a human click. |

---

## Highest-Priority Fix

### The Single Gap to Close First: **Hallucination in Acceptance Criteria**

### Why This Takes Priority:
Product managers and engineering leads operate on high-trust relationships. If Juno generates plausible-sounding but technically impossible acceptance criteria (e.g., assuming a non-existent API endpoint or ignoring microservice security handshake constraints), engineering loses confidence in the entire product specification process. 

Fixing **Hallucination** through strict ground-truth verification badges (`🟢 Verified` vs. `🟡 Unverified`) protects product credibility first. A PM can easily accept an opaque summary or click a manual confirmation button, but a single hallucinated technical requirement reaching an active sprint backlog destroys trust across the entire engineering organization.