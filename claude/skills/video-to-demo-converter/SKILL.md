---
name: video-to-demo-converter
description: Builds a Supademo demo from uploaded video or prepared screenshots, then adds copy and structure. Use for a recording-based demo; explain when a requested screenshot sequence needs separate capture or extraction.
---

# Video to Demo Converter

Turn a recording or prepared media sequence into a demo using the media handles Supademo actually supports.

## Workflow

1. **Choose the output.** One uploaded video becomes one video step. A screenshot walkthrough needs separate image assets, one per step. The MCP tools do not automatically split a recording into screenshot steps. If the user needs that output, prepare the capture/extraction plan and use a separately available, authorized capture workflow, or ask for the screenshots.
2. **Get trusted media handles.** Use conversation handles if present. For local files, call `create_upload_job`, provide its upload URL, and call `get_upload_job` after upload until processing completes. Use returned `videoId` for a completed video, or image URL, width, and height for each image. For explicitly requested library reuse, call `list_media_library_items`: a video's `itemId` is its `videoId`; image items provide `url`, `width`, and `height`. If an image lacks positive dimensions, request a completed upload with those values rather than inventing them.
3. **Build.** For a new demo, call `create_demo_from_uploaded_media` with the ordered media array. Map selected library videos to `{ type: "video", videoId: itemId }` and images to `{ type: "image", imageUrl: url, width, height }`. Each item becomes one regular step in that order. Preserve the returned demo and step IDs. To add library items to an existing demo instead, resolve the target with `get_demo`, then call `create_step_from_media_library_item` with that `demoId`, the selected `itemId`, and its `type`. That tool adds a step; it does not create a demo or return a media handle.
4. **Edit the result.** Read `get_demo`. Add clear step copy with `update_steps` and appropriate hotspots with `create_hotspots`. Create new task-based chapter steps with `create_steps` using `type: "chapter"`, `chapterType: "Link"`, the title in `chapter.heading`, and the planned 1-based `position`; use `update_chapters` to edit existing chapter step IDs. Use `reorder_steps` or `delete_steps` only for changes included in the user's request. There is no generic step-merge tool. Removing a step does not trim dead air inside a video.
5. **Handle audio explicitly.** Do not claim the source narration was removed or restored by conversion. Inspect the resulting video/audio. If new narration is requested, use `voiceover-producer`; adding generated voiceover is separate from editing or muting source video audio.
6. **Verify.** Use `get_demo` and `demo-qa-checklist`. Check the actual media, step order, copy, links, and playback when browser access is available. Publish only when publication is part of the authorized task.

## Source review

Inspect for private data, notifications, and unreadable captures before sharing. Explain any required recapture or redaction, and distinguish completed edits from work the available tools cannot perform.

## Supademo tool conventions

Read [the tool conventions](../supademo-onboarding/references/tool-use.md) before calling Supademo tools for this workflow.
