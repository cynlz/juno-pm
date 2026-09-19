# Prototype · Juno

## Prototype link

* **Public Share URL:** `https://lovable.dev/projects/juno-pm-p0-triage-prototype` *(Replace with your live prototype share link)*

---

## What it demonstrates

This prototype proves the end-to-end **Signal-to-PRD Synthesis Flow**: taking unstructured customer feedback (interview transcripts, support tickets, executive emails) from raw text, processing it into structured insights with priority and sentiment tags, and instantly generating an evidence-backed PRD Opportunity Brief with BDD acceptance criteria—all in a single dark-mode workspace.

---

## Debrief

- **What worked:** The persistent three-column layout made the line of sight between raw customer evidence, structured insights, and the final PRD spec completely transparent. The 1.5s simulated processing state provided immediate feedback without breaking context.
- **What broke / felt like a toy:** Mocked static responses meant the transition from raw input to generated insights didn't dynamically adapt if non-standard transcript formats were pasted in.
- **What I'd change next pass:** Wire the middle and right columns directly to live API model calls with streaming text output so the PRD preview renders progressively as insights are extracted.