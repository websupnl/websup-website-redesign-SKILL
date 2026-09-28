# Quality and completion checks

Mark each item PASS, FAIL, or NOT TESTED in the handover. A written checklist is not evidence that its tests ran.

## Story and authenticity

- Exact opening/reply/return/CTA copy matches the supplied brief.
- The old website matches the chosen reference; it has not been intentionally degraded.
- The finished desktop and mobile designs match the approved references.
- Real website facts, client statements and results have not been invented.
- The client site's branding and WebsUp's end-card branding remain distinct.
- The viewer gets the scheduled old-site reference window and finished-design holds.

## Continuity

- The expansion begins at the clicked link, and the return lands on that link.
- Mapped logo/headline/image/CTA transitions are visible; the rebuild is not only a whole-image crossfade.
- Text handovers have no overlapping words or stretched glyphs.
- Scroll and camera motion do not create unexplained jumps back to the hero.
- Desktop-to-mobile shows real layout changes, not desktop scaled down.
- The mobile menu opens, is legible, and closes within its beat.
- The comparison endpoints have identical viewport, camera, hero position and clipping.
- The cursor/touch target is correct after camera transformations.

## Visual and temporal checks

Inspect stills around 0.8, 3.5, 5.2, 6.5, 8.5, 10.5, 12.5, 14.5, 15.6, 17.5, 20.8, 23.0, 24.5, 25.7, 26.7, 27.4, 28.5, 29.6, 30.8, 31.7, 32.5 and 34.8 seconds. Adjust/add samples to match actual event timings.

- Inspect both settled states and mid-transition frames.
- Review the continuous video at its intended viewing size; messages, major content and CTA remain readable.
- Check crops, clipping, borders, image resolution and responsive line breaks.
- Check arbitrary-time determinism by seeking in non-chronological order and comparing repeated timestamps.
- Check frame samples directly before/after overlay and native-content handovers.
- End card remains stable through the last output frame.

## Technical and audio checks

- All required resources load without live-network dependencies in the final render.
- There are no browser errors or failed image/font/background assets.
- FFmpeg exits successfully and the output file exists and is playable.
- Encoded dimensions and frame rate match the chosen specification.
- Duration is 35 seconds within the selected frame/container timing tolerance.
- Audio is present when a finished audiovisual version is claimed; cues align, no obvious clipping, music resolves cleanly.
- Audio sources and any illustrative interactions are documented.

## Delivery status

Choose one accurate label: specification only; unrendered implementation; silent draft; audiovisual draft; verified final film.

Do not mark work complete solely because source code was written, a render command was issued, or a file name was planned.
