# Prototype · Juno

**Public Share URL:** https://rocketship-prd-wizard.lovable.app

## What it demonstrates

The prototype shows the core shape of Juno as an AI associate PM: a three-step flow, **Source → Distilled → Directive**, that takes messy raw input (interview transcripts, support tickets, executive emails) and turns it into structured, prioritized insights and a draft PRD-style output ("Opportunity Brief"). It's aimed at the same friction this whole project was built around: insights getting re-typed into Jira, going stale, and PMs having to manually consolidate signals scattered across Slack, Notion, and support tools before they can even start triaging.

Conceptually, the three steps map onto the harness pipeline this project specified: Source is the retrieval step (the six named sources in our spec), Distilled is the cross-reference-and-score step, and Directive is the drafted output that's meant to go to a human. The prototype proves that shape is buildable as an interactive tool, not just a diagram.

## Debrief

### What worked

- The Source → Distilled → Directive flow is legible at a glance. A PM opening this for the first time can tell what stage they're at without instructions, which matches the intent behind the badge-to-canvas hybrid placement we specified.
- Consolidating multiple raw inputs into a single console genuinely addresses the real pain point named in the tool's own framing, that insights are "out of date by Thursday" because they live scattered across tools. That's a legitimate problem this prototype's UI shape solves.
- The "Structured Insights" step, with priority and sentiment labeling, shows the triage function, turning noise into something ranked, is achievable as an interactive step, not just a backend concept.

### What broke, or felt like a toy

- **The input isn't scoped.** The live tool accepts arbitrary pasted transcripts, tickets, and emails all at once, not the strict six-named-source, single-artifact-type boundary this harness was built around. That's a meaningful gap from what we specified: without that scoping, there's no way to confirm the tool is actually cross-referencing a real Strategy doc, Capacity Note, and Roadmap rather than pattern-matching on whatever text gets pasted in.
- **No visible citation structure.** The output is described as "evidence-backed," but nothing in the UI shows a claim-to-source link the way our `citations: [{claim, source_id}]` schema requires. "Evidence-backed" as a label isn't the same as a checkable citation, and that distinction was the entire point of the pre-ship gate's zero-tolerance rule.
- **No confidence meter or freshness header.** Nothing surfaces how current the underlying sources are, or how confident the tool is in its own output, both central pieces of the InsightCard refactor and the Confidence Calibration dimension from the rubric.
- **No visible human-in-the-loop gate.** The flow appears to go straight from input to a generated draft with no Approve/Edit/Reject checkpoint in between. That's the single most important control this whole project specified, and its absence here is the biggest gap between the prototype and the harness.
- **It reads more like a UI shell than a wired pipeline.** The page shows placeholder sections and status indicators "awaiting content processing," which suggests the generation step may not be fully connected end-to-end yet, more a demonstration of the intended shape than a working instance of the retrieve → cross-reference → score → gate pipeline.

### What I'd change next pass

- Constrain the Source step to the six named sources for one signal type, rather than accepting arbitrary multi-source paste-ins, so the prototype is actually testing the scoped harness instead of a general-purpose summarizer.
- Add a visible citation on every claim in the Directive output, not just an aggregate "evidence-backed" label, matching the Strategic Traceability section built in the InsightCard refactor.
- Surface a confidence meter and a per-source freshness indicator before the draft is shown as finished.
- Insert an explicit Approve / Edit / Reject decision point before any output is treated as final, this is the one change that would close the biggest gap between what's live and what was specified.
- Replace the placeholder/status-indicator shell with the real pipeline steps, so a reviewer can see retrieval, cross-referencing, and scoring happen, not just a loading state between input and output.
