---
name: websup-website-redesign
description: Create a standalone website-redesign animation for WebsUp from a visual brief and authentic before/after website assets. Use for client-message-to-website stories, continuous UI transformations, desktop-to-mobile reveals, and before/after website advertisements. Reuse the motion-broll time-driven engine when available; do not require a talking-head video or transcript.
---

# WebsUp Website Redesign

Act as a motion designer and implementation engineer. The website is the product being advertised. The audience must understand the original site, see recognizable elements being redesigned, and have time to appreciate the result.

This is an adaptation specification, not a finished renderer. It depends on the separately installed `motion-broll` engine or an equivalent time-driven implementation. Do not claim that website extraction, element matching, responsive morphing, or sound mixing already exist in the upstream engine.

## Read first

1. Read `references/CASE-WEBSITE-REDESIGN.md` for the supplied 35-second case, exact messages, timings, and ending.
2. Read `references/ENGINE-ADAPTATION.md` before implementation. It identifies the relevant upstream APIs and the extensions needed for this use case.
3. Read `references/QA-CHECKLIST.md` before rendering or claiming completion.
4. Locate the existing `motion-broll` skill and read its `reference/engine-api.md` and engine code. Follow its engine contract, but replace its talking-head workflow with this one. If it is absent, report that dependency; do not pretend the engine is bundled here.

## Intended output

A standalone 35-second film, editable source, a seekable browser preview, and a short review report. This is not a set of B-roll clips to insert into a source video. The 13 shots are beats within one visual journey, not 13 separate hard-cut animations.

Default audio direction: instrumental music and selective sound effects, without narration. Do not add synthetic voiceover unless requested.

Keep final width, height and frame rate explicit. If the destination is not specified, propose 1080 × 1920 for a social cut and mark it as an assumption, not as a requirement in the supplied brief. Use an independently composed 1920 × 1080 version for landscape, rather than a mechanical crop. Frame rate is configurable; choose it before timing the final render.

## Intake: inspect what exists before asking

Use the current request, attached assets, and accessible project files. Do not ask the user to repeat this brief or its timeline. Collect only unresolved inputs:

- The old website: approved URL, archived page, supplied screenshots, or local source.
- The new website: approved live URL, local source, or approved desktop/mobile design.
- The client site's own branding and assets, separate from WebsUp's presentation/end-card branding.
- Destination/aspect ratio and any supplied audio or brand assets.

Do not ask for a video, transcript, SRT, talking-head density, or picture-in-picture coordinates.

If before/after references are missing, finish the specification and identify the missing references. A fictional demonstrator may be built only when that is requested or explicitly allowed. Label it as a concept; never pass it off as an actual customer redesign. A static design is not proof that its interactions already exist on a delivered website.

The conversation in the supplied brief is scripted advertising copy, not evidence of a real customer conversation. Do not attach it to an identifiable customer without appropriate user-provided context.

## 1. Freeze authentic website references

Inspect the old and new sites at comparable desktop viewports, and inspect the new site at a real mobile viewport. Record the capture dimensions and scroll positions.

Capture at least the hero, one or two relevant sections, and the mobile menu state when available. Preserve the old site's actual typography, colours, imagery, spacing and content. Do not add defects, artificial loading delays, darkening, blur, or broken controls to strengthen the comparison.

Use local assets in final rendering. A live iframe may help inspection, but the exported movie must not depend on a changing remote page, analytics, cookie banners, third-party timing, or a live network connection. Never enter credentials, submit forms, or change a production website merely to make the animation.

When a reference is a screenshot, state that it is a flattened reference. Separate or reconstruct only the visible elements needed for the transformation, and compare the reconstruction with that reference. Do not claim that arbitrary screenshot pixels are editable DOM elements.

## 2. Establish the finished design before animating

Prepare three reference frames first:

- Authentic old hero at the comparison framing.
- Finished new desktop hero.
- Finished new mobile layout.

Treat the after-design as a design task in its own right if the user has requested its creation. Do not improvise a generic landing page during the final reveal. Keep unsupported metrics, testimonials, awards, prices, and performance claims out of the design.

A real client website keeps its own identity. WebsUp branding belongs to the surrounding presentation and final card; it is not a reason to recolour the client's website.

If the user has already approved the visual direction or requested autonomous execution, inspect and improve these frames without inserting an unnecessary approval gate. Do not publish anything externally without authorization.

## 3. Build a continuity map

Plan one persistent interaction surface:

`link inside conversation → browser → redesigned browser → mobile browser → desktop comparison → link inside conversation → end card`

The surrounding conversation can be a separate layer. The expanding surface must originate from the clicked link, not from an unrelated rectangle at the frame centre. Store that original geometry so the return transition lands on the same link.

Inside the browser, use explicit element identities such as:

- `client-logo`
- `navigation`
- `hero-headline`
- `hero-image`
- `primary-cta`
- `featured-section`

Record each element's measured before/after rectangle, typography, crop, clipping, and parent coordinate space. Map the same subject to itself whenever possible. New elements can enter deliberately; removed elements can leave deliberately.

Use persistent elements or visually matched overlay elements during the rebuild. Do not hide a whole old screenshot and fade in a new screenshot while claiming a physical reconstruction. The outer browser morph alone is insufficient.

For changed text or line wrapping, use a controlled handover inside the mapped text region. Do not stretch glyphs or fake a perfect font morph. Preserve the heading's placement and visual role even when its copy changes.

## 4. Follow the supplied timeline

Implement the exact 13 beats in `references/CASE-WEBSITE-REDESIGN.md`. Do not repeat the entire brief back to the user instead of executing it.

Key constraints:

- Start immediately with the incoming message. No title or opening logo.
- Keep 00:06–00:10 available for understanding the old site.
- Limit the rebuild to 00:10–00:16; the build is anticipation, not the main attraction.
- Hold the finished hero clearly at 00:16–00:20.
- Show real or explicitly staged, design-faithful interactions, not arbitrary cursor motion.
- Preserve continuity through desktop → mobile → desktop.
- Match the old/new framing for the comparison.
- Keep the 00:32–00:35 end card stable and readable.

Do not silently jump back to the hero after scrolling. Either bring the hero back into view through a visible motion, or track the mapped elements into their new arrangement. Choose and document that handover.

## 5. Animation implementation

Reuse the existing time-driven motion engine when suitable. Construct one master scene with one 35-second clock. Organize code into modules if helpful, but avoid independent players whose timing can drift.

Every rendered frame must be computable from an arbitrary timestamp. Recompute positions, scroll, opacity, masks, menu state, hover state, cursor state, and camera focus from that timestamp. Do not rely on a previous frame, real user events, random unseeded values, CSS transitions, or timeout-driven changes.

The browser shell and its content have different jobs:

- The shell changes size, corner radius, location, and framing.
- The content contains independently controlled site elements.
- Scrolling changes content offset under a consistent clip.
- Mobile is a responsive arrangement of content, not a scaled-down desktop screenshot.

Use restrained, mostly critically damped or lightly overshooting motion. Do not impose a blanket bounce on every UI element. Let settled design frames remain still. Use motion blur selectively enough that the website and final text stay legible.

For mobile, calculate desktop and mobile layouts independently, then interpolate visible shared elements or use a locally controlled responsive layout. Resizing a div inside a fixed capture viewport must not be assumed to trigger viewport media queries. Read the implementation notes.

Keep cursor movement causally connected to the action. Test its position after camera transforms. During mobile interaction, use an intentional pointer or subtle touch indicator rather than an unexplained desktop cursor floating over a phone-shaped object.

## 6. Sound design

The upstream image renderer does not mix a soundtrack. Implement an explicit audio stage.

Use a cue sheet tied to the same master clock: incoming message, reply, link click, a few meaningful layout landings, final button, reveal, comparison, return message, music resolution. Avoid one sound effect per moving item.

Use user-supplied, properly licensed, or original sounds/music and record their origin. Do not silently add an audio service, paid generation, or voiceover. If suitable music is unavailable, deliver a clearly labelled silent review render and the missing-audio status rather than call it a finished audiovisual film.

Keep the transition into the 16-second reveal intentional: a brief reduction before the reveal, then a clear musical landing. Resolve the soundtrack by 35 seconds. Verify the muxed file, not only the browser preview.

## 7. Review and deliver truthfully

Inspect the quality checklist and fix visible failures. At minimum review the opening message, old hero, old scroll, start and middle of the rebuild, final hero, desktop detail, mobile menu, comparison, return message, and final card.

Also inspect intermediate transition frames and arbitrary-time seeks. An attractive contact sheet alone does not prove smooth motion.

Deliver only artifacts that actually exist:

- The final MP4 when a render has been completed and checked.
- The editable source and local assets, subject to asset-sharing restrictions.
- A seekable HTML preview or a local preview with precise launch instructions.
- The timeline/audio cue sheet and a concise QA/status note.

Distinguish clearly among specification, unrendered implementation, silent draft, and verified final film. Do not say a skill has been installed, a repository has been updated, a video has been rendered, or a site has been captured unless the action was performed and verified.
