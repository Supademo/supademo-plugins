---
name: persona-script-adapter
description: Adapts an existing Supademo demo's script to a specific buyer persona — same click path, different narrative. Use when one product flow needs to speak to admins, end users, and executives separately.
---

# Persona Script Adapter

The clicks stay the same; the story changes. One captured flow becomes three persona-specific demos.

## Prerequisites

- Supademo MCP connected
- The source demo and a persona brief: role, what they're measured on, what they fear, vocabulary they use

## Workflow

1. **Load the source.** `get_demo` — the full step sequence and current copy.
2. **Interrogate the persona.** If the brief is thin, ask: What does this person get fired for? What number are they trying to move? Who do they have to convince internally? Their answers drive every rewrite.
3. **Rewrite the narrative, step by step:**
   - **Same screens, different emphasis** — an admin sees "granular permissions"; an exec sees "nothing leaks, no tickets"
   - **Reframe outcomes in their metric** — support leader: deflection rate; RevOps: time-to-first-value
   - **Adjust vocabulary register** — practitioners get precision, executives get consequences
   - **Rewrite the CTA** — "Start free trial" for practitioners; "See the 2-min overview" for execs who won't sign up
4. **Prepare the adaptation** as Step | Original | {Persona} version. Return it for a drafting request, or apply it to the requested variant when those edits are already authorized.
5. **Create the variant.** `duplicate_demo` (never edit the source), then `update_steps` / `update_hotspots` on the copy. Name it clearly: "{Demo} — {Persona}". Resolve or create tag IDs with `list_tags`/`create_tags`, then use `add_demo_tags` for findability.
6. **Optional:** persona-matched voiceover via `generate_voiceovers`.

## Guardrails

- Never mutate the source demo — always duplicate first.
- Don't invent capabilities the screens don't show; adaptation changes framing, not facts.
- If the click path itself is wrong for the persona (execs don't want 25 steps), recommend a trimmed duplicate instead of a re-narrated full flow.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
