# Implementation notes: adapt the engine, replace the B-roll workflow

## Inspected upstream source

Repository: https://github.com/Barty-Bart/motion-graphics

Inspected commit: `e8d610adcf946367430c8b43a97aad8059befaad`.

Relevant paths:

- `skills/motion-broll/SKILL.md`
- `skills/motion-broll/reference/engine-api.md`
- `skills/motion-broll/engine/motion.js`
- `skills/motion-broll/engine/build.py`
- `skills/motion-broll/engine/render.js`

Read the currently installed version before implementing; reconcile differences rather than assuming its API has not changed.

No upstream engine code or font binaries are distributed in this package. The notes below describe what was inspected and what an implementing agent must add. This package is not an executable browser-to-video application.

## What already exists

The engine exposes `M.scene`, numeric and colour tracks, analytical spring helpers, layer visibility helpers, a cursor path, camera/shape geometry, and `window.seek(t)`. Scene duration is exposed as `window.DURATION`.

The clip builder combines HTML fragments with the engine and base styles. The inspected renderer opens the generated page with `?render`, reads the stage size and duration, calls `seek(t)`, captures four subframes per frame, and encodes the result with FFmpeg.

The engine is useful for continuous shell transformations. Its standard layer changes use opacity, blur, and scale. Those changes do not automatically map website elements, reconstruct a page, or implement responsive transitions.

## What to replace from the original skill

Replace the source-video interview, transcript extraction, speech-driven beat planning, B-roll density, speaker/PiP inspection, face gaps, and source-video compositing.

Use the supplied brief and exact timeline instead. Do not require a `plan.json` containing an existing source video solely to satisfy the old compositor. Build and render one standalone scene; mix audio separately.

The original warm-grey/black/orange palette is a default, not WebsUp's established identity. Preserve real client branding inside the website and use verified WebsUp presentation assets outside it.

## Recommended scene architecture

1. A stable output stage with explicit width, height, duration and fps configuration.
2. Surrounding chat elements, which are not the same thing as the morphing link surface.
3. One persistent link/browser surface whose position, dimensions, radius and framing vary with time.
4. One clipped content viewport under the browser chrome.
5. Independently controlled mapped website elements inside or over that viewport.
6. A cursor/touch layer and a final-card layer.

Use `M.scene` for the outer surface and master clock, and `geom`/`extra` or controlled element updates for the inner transformation. Use persistent browser-content layers during the rebuild, not a whole old/new layer swap.

The links, headlines, images and controls can be ordinary DOM/SVG elements or carefully extracted image layers. The requirement is controlled geometry and visual fidelity, not a specific frontend framework.

## Geometry and identity

Store before/after geometry in a common coordinate system. `getBoundingClientRect()` gives viewport geometry: record capture viewport and scroll position, and translate coordinates explicitly when comparing against document geometry.

Map semantic identities manually when selectors or DOM structures differ. Record at least rectangle, font/text treatment, background, radius, crop/object position, clipping parent, and visibility range. A mapping proposal must be visually checked; similar element names are not proof of equivalent content.

Include browser location, camera scale/focus, and content scroll when converting an element to screen coordinates. Use those same transforms for cursor targeting. Never aim the cursor at a pre-zoom coordinate.

At a handover between native page content and animated overlay elements, match both geometry and styling before changing visibility. Test the frames on either side of the handover. Keep readable text undistorted; a local typography handover is preferable to grotesquely scaling glyphs.

## Responsive transition

The video output frame remains fixed while the inner browser changes size. A viewport media query follows the document viewport, not an arbitrary resized parent div.

Suitable approaches include:

- Capture/measure the approved desktop and mobile layouts, then drive shared element positions and controlled text-layout handovers between those endpoints.
- Recreate the required site fragments using container-responsive layout, and explicitly interpolate breakpoint changes where continuous motion is needed.
- Use a same-origin, locally frozen iframe with a changing viewport, plus controlled element overlays to bridge discontinuous breakpoint changes.

Do not assume the third approach is automatically deterministic. Wait for assets and layout in the frame and compute all UI states from the master timestamp. Avoid live cross-origin pages in final capture.

Verify the actual mobile design and menu reference. A narrow screenshot and an invented hamburger icon do not establish an authentic mobile experience.

## Deterministic state

`seek(18)` must produce the same visible frame whether the previous call was `seek(0)`, `seek(34)`, or another `seek(18)`.

Derive scroll, hover, open/closed menu, wipe progress, content visibility and all transforms directly from time. Reset properties explicitly rather than leaving hidden state from a previous seek. Browser-preview playback may advance time, but render output must not depend on wall-clock timing.

All final-render assets should be local or embedded. Avoid network-triggered layout changes during capture. Static captured references are preferable to invoking a real site's uncontrolled scroll animation on every subframe.

## Renderer checks and extensions

The inspected `render.js` waits for document fonts, but does not explicitly decode every newly introduced website image or mix audio. Its FFmpeg input is the rendered PNG stream.

Before exporting a custom website scene:

- Wait for all required images and local embedded resources, including any controlled frames, not only fonts. Treat decode/load failures as errors. Expose and await a project-level readiness promise if useful.
- Verify CSS background images as well as `<img>` elements.
- Set the output viewport and allow layout to settle before measuring/capturing.
- Re-check readiness when responsive layouts select different images or fonts.
- Fail on page errors, missing stage/duration, failed FFmpeg exit status, or missing output. The inspected renderer collects page errors but does not by itself make all of these a successful-export gate.
- Probe the output dimensions, frame rate, duration and streams. Verify the actual encoded result visually.
- Use a local adapted renderer when changes are required; do not silently edit a globally installed skill.

`build.py` embeds its engine/base/font inputs; it does not automatically bundle arbitrary new website images or rewrite all custom asset URLs. Arrange portable asset paths or implement an explicit bundling step. Do not call a preview self-contained until it opens without missing dependencies.

Do not distribute font binaries to the user as part of this task. Refer the implementation environment to authorized local assets or the upstream installation as appropriate.

## Audio stage

Prepare a cue sheet with timestamps and asset origins. Mix effects and music against the 35-second visual master, then mux them into the final MP4. Check audible sync and the final end time.

Browser audio playback is not captured by the upstream screenshot renderer. A working `<audio>` element in the preview is not proof that the exported MP4 contains sound.

## Review artifacts

Generate reference stills and intermediate transition frames, then review continuous playback. A contact sheet is a diagnostic aid, not a substitute for the motion review. Retain a brief record of assumptions, staged interactions, missing assets, and verified tests.
