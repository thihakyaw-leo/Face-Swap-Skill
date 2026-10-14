# Higgsfield Genjutsu: Mode Selection and Current Product Notes

Consult this reference when a user asks for a Genjutsu-like transformation or when the Higgsfield connector is available. **Re-check the live UI/tool schema before each run**; product limits and connector operations can change.

## Choose the mode by what should remain

- **Object Swap:** Target one performer, outfit, product, prop, location, or other element and preserve the rest of the original shot as much as the tool allows. Use when the user wants the original scene/background and camera context to stay recognizable while changing a person or clothing.
- **Motion Transfer:** Use the source clip primarily as a motion, camera, and timing guide, then rebuild the performer or scene from target references. Prefer it when the desired subject has substantially different body proportions/silhouette, or when the user wants a new character/world rather than a localized edit. Explain that this rebuild may alter fine details beyond the target.

Do not call a full-character transformation a face-only swap. Ask the user to separate **what should change** (identity/face, hair, body build, skin/fur/material, outfit, footwear, accessories, props, background) from **what should remain** (motion, camera, timing, cuts, background, audio). If a user asks to change the body substantially but preserve the original background, choose the closest current mode after checking the live UI; do not imply the tool can perfectly isolate both constraints.

## Reference pack for full-person and wardrobe change

Use a small, consistent set rather than maximizing the image count:

1. **Identity/face views:** clear front and 3/4 views, plus profile if useful; keep lighting/color reasonably consistent.
2. **Body/silhouette views:** full-body front and side or 3/4 views that communicate build, height impression, posture, and proportions.
3. **Wardrobe views:** head-to-toe view of the exact outfit and separate detail views only for important fabric, pattern, footwear, or accessories.

Remove contradictory images (different hair, physique, outfit, or age presentation) unless the user specifically wants variation. State whether the complete performer should be replaced. Never assume face references alone will reliably change body anatomy or clothes.

## Source video preparation and review

Choose a source with one clearly visible subject, useful head-to-toe framing for full-body changes, readable movement, modest motion blur, and adequate lighting. Avoid unnecessary occlusion or rapid cuts when the requested transformation must stay consistent. Before export, compare source and result at corresponding moments. Inspect face and body consistency, silhouette, clothing coverage and details, hands/feet, limb articulation, fabric folds, occlusion, flicker, source-person remnants, motion/camera alignment, and audio continuity. Exact frame-level preservation and exact identity/body matching are not guaranteed by a generative transformation.

## Vendor-reported product details (checked 2026-10-14)

Higgsfield describes Genjutsu as supporting two approaches: Motion Transfer rebuilds a scene around the source motion/camera/timing; Object Swap edits a selected character, outfit, product, location, or object while preserving the rest of the shot. The official product material currently describes reference clips of 4–30 seconds, up to 30 reference images, and output up to 1080p. These are vendor-reported limits, not guarantees; confirm the live UI/tool schema before using them.

Official sources:
- https://higgsfield.ai/genjutsu
- https://higgsfield.ai/blog/higgsfield-genjutsu

## Connector availability

At execution time, check whether the Higgsfield connector is enabled and which operations it exposes. If unavailable, tell the user that the skill workflow is ready but the platform connection must be authorized before operating it. Do not scrape, upload, or invoke a guessed endpoint to bypass a disabled connector. Never assume a tool can perform Genjutsu merely because a Higgsfield connector is listed; inspect its current tools and input schema first.
