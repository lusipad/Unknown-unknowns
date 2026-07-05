# Pitch & Explainer Doc

Reviewers start with the same unknowns the user started with. A good pitch doc walks
them through faster, and shows experts that the failure points they'd probe were already
accounted for. Answer their first three questions before they ask.

## One document, in this order

1. **The demo** — GIF/screenshot/link, first thing visible. One caption line.
2. **What & why** — two paragraphs max: the problem, and why now.
3. **The decisions that matter** — the 2–4 choices a reviewer would push on, each with
   the reasoning and the rejected alternative. Pull from the plan's "most likely to
   tweak" section and the decision log.
4. **Unknowns we found and answered** — potholes discovered along the way (from the
   blindspot briefing and the notes' Deviations/Surprises) and how each was handled.
   This is the section that converts experts: their anticipated objections, already met.
5. **What we didn't do** — explicit non-goals and known limitations. Preempts the
   "but what about…" thread.
6. **How to try it** — exact commands or steps, copy-pasteable.
7. **Risks & rollback** — what could go wrong and how to undo it.

## Fit the channel

Default: a single Markdown document that drops cleanly into Slack or a PR description.
For a standalone page (design review, wider audience): one self-contained HTML file,
same structure, demo media embedded.

## Quality bar

- A reviewer who reads only the demo and section 3 should already lean yes.
- Every "it works" claim is backed by something visible: a test name, a screenshot, a
  command output.
- No section over ~150 words except the decisions section. Cut until it hurts, then stop.
