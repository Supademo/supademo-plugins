---
name: voiceover-producer
description: Writes a per-step voiceover script for a Supademo demo and generates AI voiceovers in a chosen voice, optionally with background music. Use when turning a silent click-through demo into a narrated product tour.
---

# Voiceover Producer

Turn a silent demo into a narrated tour: script it, pick a voice, generate, review.

## Prerequisites

- Supademo MCP connected
- The demo to narrate

## Workflow

1. **Read the demo.** `get_demo` — understand what each step shows and what the annotation already says.
2. **Draft the script.** Write one short voiceover line per step:
   - Spoken register, not written — contractions, short sentences, no bullet-speak
   - Don't read the annotation aloud verbatim; the voiceover adds context, the annotation labels the action
   - 8–15 words per step; the viewer should never wait for narration to finish
   - Open with the outcome ("Here's how you cut onboarding time in half"), not the feature name
3. **Prepare the script** as a table (Step | On screen | Voiceover line). For a drafting request, return it for review. For an authorized generation request, use the supplied or requested script within that scope; do not repeat an existing approval.
4. **Pick the voice.** Use an already selected voice, or `list_voices` to resolve the requested voice. Offer 2–3 options only when a meaningful preference remains missing.
5. **Generate.** `generate_voiceovers` with the approved script and chosen voice.
6. **Optional music.** If requested, use `list_background_music` and apply the selected track through supported `update_demo_settings` fields. Listing a track alone does not apply it.
7. **Review pass.** Re-read `get_demo` and verify generated audio is ready for each intended step; generation may be asynchronous. Listen when playback is available, and mark pronunciation/timing unverified otherwise. Flag steps where the line runs longer than the step naturally displays.

## Guardrails

- If steps already have voiceovers (human-recorded or previous AI), overwrite only when replacement of that existing audio is included in the user’s authorization — removing audio is `delete_voiceover` and it's destructive.
- Keep one voice per demo. Mixing voices mid-demo reads as broken.
- If the demo has translations, note that each language needs its own voiceover pass after `generate_demo_translation`.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
