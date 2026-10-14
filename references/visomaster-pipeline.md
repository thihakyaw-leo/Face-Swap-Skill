# Local Face-Swap Pipeline: Model, Tracking, Mask, and Restoration Guide

Read this reference when a compatible local editor such as VisoMaster Fusion is installed and the user asks for frame-based face swaps, multi-face tracking, or restoration. **Inspect the installed version and its current UI/manual before operating it.** The official manual is updated over time and interface names or model availability may change.

## Capability and consent gate

- Do not claim that the Manus video-generation tool can run these models. They are local-app capabilities; use them only through an installed, authorized interface.
- Confirm the source-video editing rights and consent to use each identifiable target likeness. For each real person in a multi-face clip, verify the relevant permission independently.
- Keep original media untouched and render to a new output path. Do not share raw face crops, embeddings, face cards, or outputs publicly without authorization.
- Model code and model weights can have different terms. Before downloading, redistributing, or using a weight commercially, check its specific license and provenance; an application/repository license does not automatically license every model file.
- A face-swap pipeline changes facial identity and can adjust facial expression/pose. It does **not** reliably change the actor's body build, full-body pose, clothing, or whole scene. Route those requests to a verified whole-character/motion-transfer tool instead.

## Production workflow

1. **Prepare a short test.** Duplicate or segment a representative clip containing the hardest pose, lighting, and occlusion. Preserve the original audio/video and test on a few seconds before a full render.
2. **Load authorized source identities.** Create one source face card for each approved identity, using a clean reference image. Saved embeddings may speed reuse, but treat them as biometric identifiers: use local-only storage by default, name them minimally, protect the folder, and do not keep/export them without a reason and permission.
3. **Detect and assign target faces.** Choose a detector suited to the footage, then assign each detected person to the correct face card. Use ByteTrack (or the available tracker) to keep IDs across frames. Set the similarity threshold so only the intended identity matches; the VisoMaster manual describes a 1–100 control with 60 as its documented default, but the best value depends on footage. If a wrong face is included, raise the threshold; if correct frames are missed, lower it cautiously and review every match.
4. **Verify identity tracks before rendering.** Check the assignment at clip start, after occlusions, when people cross, after scene cuts, and whenever faces leave/re-enter frame. Tracking IDs can be wrong even when motion appears continuous. Use the app's issue-scan/preview tools where available. Do not render a whole multi-face video unattended until the mapping is verified.
5. **Choose a swapper with a short A/B test.** Keep the same target frames, card, crop, and baseline settings when comparing models. Select based on identity likeness, pose/profile handling, skin-tone continuity, detail, speed, and license—not on the model name alone.
6. **Set geometry and expression.** Establish a neutral swap first. Add keypoint replacement only as much as needed for the target head geometry; inspect both frontal and profile frames. Preserve the target driver's blinks, gaze, and mouth motion with expression tools only when the swap looks frozen or out of sync. Keep facial pose/expression edits subtle. These are face/head controls, not body-pose retargeting.
7. **Fix the composite with masks.** Inspect the active mask preview before changing several controls. Add only the mask that addresses the visible defect; re-check eyes, lips, teeth, hairline, hands, glasses, microphones, and side-profile edges after each change.
8. **Restore only material defects.** Compare the raw swap with one restoration/denoising configuration. Prefer the mildest pass that improves visible damage. Check identity and expression after restoration because generative restoration can invent or alter facial details.
9. **Enhance the full frame last.** Use one appropriate upscaler or colorizer only if the whole frame needs it. Avoid stacking multiple sharpeners or repeated resize passes. Run one export with the intended compression settings and check temporal flicker and audio sync.
10. **Review and deliver.** Review synchronized frames and a normal-speed playback. Confirm every person's mapping, track continuity, masks, facial motion, identity, skin tone, edges, occlusion, temporal stability, output dimensions, and audio. Clearly disclose realistic synthetic edits when viewers could mistake them for unaltered footage.

## Swapper model selection

The current VisoMaster Fusion manual lists these choices. Availability can vary by build and installed weights.

| Model family | Use as a starting hypothesis | Check before choosing |
|---|---|---|
| **Inswapper128** | General-purpose, fast baseline | Higher internal crop sizes may add detail at a speed cost; more pixels do not guarantee better likeness. |
| **InStyleSwapper256 A/B/C** | Test when preserving target-scene skin tone, lighting, or style cues is important | Variants can differ; compare them on the same difficult frames. Some builds expose a 512-resolution option. |
| **SimSwap512** | Test when a higher-resolution face crop and fine detail matter | Review identity fidelity, artifacts, and runtime on profiles and small faces. |
| **GhostFace v1/v2/v3** | Lightweight alternative; v2/v3 are described by the manual as generally sharper/more identity-faithful than v1 | Test actual footage; labels do not ensure better results for every person or pose. |
| **CSCS** | Test for challenging angles where combining appearance and identity embeddings may help | Review identity and expression carefully; avoid overfitting from a single reference. |
| **DeepFaceLive DFM** | Use when an authorized, compatible pretrained DFM model for the intended target is available | This is not a generic one-photo swapper: provide compatible DFM weights from a trusted source, verify its license, and check the app's morph/color-transfer settings and GPU use. |

Treat the table as a shortlist, not a ranking. Run a small controlled A/B comparison on the same frames and keep a note of model, settings, and failure cases so later renders are reproducible.

## Multi-face cards, embeddings, and tracking

- Create a mapping such as `track/person → source face card → permitted operation`. Do not assign one card to all faces unless that is explicitly intended and authorized.
- Similarity thresholds are filters, not proof of identity. Use a stricter value to prevent swaps on lookalikes; if coverage requires a lower value, manually inspect every added match.
- Use ByteTrack IDs to maintain continuity, but check IDs around crossing people, long occlusions, quick cuts, low detector confidence, and re-entry. Reassign or split timeline segments when an ID switch occurs.
- Use face-card/timeline markers when settings need to change with lighting, angle, or cast. Save only the minimum required workspace information; if a job file includes media paths or embeddings, protect it accordingly.
- Prefer a staged process: detect/track → inspect assignments → test swap → inspect → full render. Never infer that a face card or embedding match is correct merely because the UI accepted it.

## Keypoints, pose, expression, and blend masks

- **Keypoint replacement:** Apply gently to fit facial landmark geometry to the target head pose. Too much can warp facial structure or make the face look pasted on.
- **Expression restoration:** Transfer blinks, gaze, and mouth movement from the driving/target face when needed. Normalize extreme eye or mouth opening; compare lip sync and expression at normal playback speed.
- **Face pose editor:** Use pitch/yaw/roll, position, eye/gaze, brow, and mouth controls only for small corrective changes requested by the user. It does not provide full-body pose transfer.
- **Border mask:** Hide stray pixels at face edges/hairline/chin; blur its boundary.
- **Profile-angle mask:** Fade the far-side face when the person turns, if profile edges distort.
- **Occlusion mask:** Preserve hands, glasses, microphones, and other objects crossing the face.
- **XSeg mask:** Use as an independent segmentation channel; protect lips/inner mouth when needed. Mouth-focused XSeg/parser controls should be enabled only when a mouth-region defect is visible.
- **Text mask:** Use for a specific named object (for example, glasses or a hat) only when it needs to remain from the original. Confirm the mask preview does not remove facial features.
- **Face-parser mask:** Adjust semantic regions (eyes, brows, nose, mouth, hair, neck, background) only when the composite requires finer boundaries.
- **Eye/mouth restoration masks:** Blend original target eyes or mouth into the swap only when the swap's region is visibly wrong; use small, feathered masks and verify identity/expression remain coherent.

When several masks are active, inspect the combined mask and composite result. More masks are not automatically better.

## Restoration, denoising, color, and frame enhancement

- **Face restoration:** The VisoMaster manual lists GFPGAN-v1.4 and GFPGAN-1024 along with other restorers. Compare restored output to the raw swap; choose conservative blend strength to avoid a waxy look, invented details, identity drift, or sharpened boundaries. GFPGAN is a restoration pass, not an identity-matching model.
- **ReF-LDM denoiser:** Use as a reference-guided face-crop restoration/texture pass, not as a generic video denoiser or swapper. Try **Single Step** for a faster, subtle pass first. Use **DDIM/Full Restore** only when the defect warrants iterative restoration and the extra compute; compare identity, texture, and frame-to-frame stability. A fixed seed can help reproduce tests, but does not guarantee temporal consistency.
- **Restore eyes/mouth:** Apply these region blends only to correct visible artifacts and inspect the whole expression afterward; restoring too much from the original face can weaken the requested target identity.
- **AutoColor/color transfer:** Match the swapped face to the target scene's light and color, then inspect skin and neck transitions. Avoid aggressive transfer that changes the target's natural complexion.
- **MPEG/JPEG artifact simulation:** Use only when a creative brief requires a compressed-media look or to match the actual delivery texture. Do not use artifact simulation to conceal manipulation or make synthetic footage appear authentic.
- **Frame enhancers:** Upscalers (such as RealESRGAN/BSRGAN/Upsharp variants) act on the full frame; choose one only when needed. For black-and-white/color work, select an appropriate colorizer; a video-aware mode may reduce flicker. Do not assume face restoration and full-frame upscaling are interchangeable.

## Troubleshooting map

| Symptom | First adjustment to test |
|---|---|
| Wrong people are swapped | Verify card assignment and track IDs; tighten similarity threshold or detector confidence. |
| Missed valid frames | Check face size, pose/lighting, detection threshold, and card similarity; relax one threshold at a time and manually review new matches. |
| Face drifts or jumps | Check tracking, keypoint smoothing, marker changes, and cut boundaries; split/reset track assignments as appropriate. |
| Face looks pasted on | Inspect composite masks, profile fade, occlusion, border feather, and color/texture match. |
| Mouth/eyes look wrong | Check expression transfer and eye/mouth masks separately; avoid stacking restoration passes. |
| Waxy or changed identity | Reduce restorer blend/denoising strength or disable restoration; compare raw swap. |
| Flickering detail or color | Disable repeated enhancers; use consistent settings and inspect temporal behavior; avoid frame-by-frame parameter jumps. |
| GPU memory or speed issues | Lower input/crop resolution, unload unused models, process a shorter test, and consult the installed app's requirements before changing hardware/backend settings. |

## Sources

- VisoMaster Fusion user manual: https://github.com/VisoMasterFusion/VisoMaster-Fusion/blob/main/docs/user_manual.md
- ReF-LDM official implementation (NeurIPS 2024): https://github.com/ChiWeiHsiao/ref-ldm
- GFPGAN official implementation: https://github.com/TencentARC/GFPGAN

Product/model details were checked on 2026-10-14. Verify current documentation, local installation, model files, and weight-specific licenses before execution.
