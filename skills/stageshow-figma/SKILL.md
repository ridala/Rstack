---
name: stageshow-figma
description: Create editable product illustrations and short UI demonstrations in Figma. Use for marketing product shots, homepage heroes, feature cards, bento illustrations, device compositions, and prototyped product walkthroughs. Covers native layers, component reuse, prototype states, and visual verification.
---

# StageShow for Figma

Turn a product capability into a visual story built from editable Figma layers. Decide what the viewer should understand, then make that understanding immediate.

## 1. Establish the brief

Identify the product, capability, destination, final display dimensions, and supplied references. Determine whether the output is static, interactive, or an autoplay demonstration.

Use supplied dimensions and design-system assets. When a detail is missing, choose a reasonable default and state it briefly. Ask only when the missing information changes the work materially.

Write one sentence describing the intended outcome, such as: “A teammate assigns a conversation, and the new owner appears in the inbox.”

Completion: one outcome and a defined output format.

## 2. Inspect the environment

Read the connected Figma tool instructions. Inspect the target selection, surrounding design, components, styles, and variables before construction. Follow the host integration's mandatory workflows.

Confirm whether the tools can create native layers, edit instances, wire prototypes, render frames, and play animations. Choose an implementation supported by those capabilities.

If prototype authoring is unavailable, create editable state frames and a transition specification. Label them as unwired. A rendered frame proves appearance only.

Completion: a feasible construction and verification method.

## 3. Plan the composition

Choose the focal object and the intended viewing order. Make the result primary, explanatory context secondary, and peripheral detail quiet.

Define the visible output frame before building its contents. Keep the focal action and result inside it. Use deliberate overlap or cropping where it helps the composition.

Judge text at its actual display size. For a small destination, rebuild around fewer elements instead of shrinking everything uniformly.

For multiple feature tiles, vary the visual form while sharing spacing and typography. Give each tile a distinct job within the set.

Completion: the still composition communicates the capability before motion is added.

## 4. Construct native layers

Use editable text, frames, vectors, and component instances. Screenshots can serve as references or intentional image assets; newly authored controls should remain editable.

Use a fixed-size outer frame for the output boundary. Use Auto Layout for content that reflows and absolute positioning for intentional overlap. Apply clipping at the frame that defines the crop.

Reuse existing components. Introduce local components only where repetition or state management justifies them. Use available variables and styles without creating an unnecessary design system.

Use stable names such as `Conversation/Owner`, `AssignmentMenu`, and `Cursor/Pointer`. Keep the hierarchy readable.

When using the Plugin API, load fonts before editing text. Check wrapping and truncation after changes.

Completion: editable artwork with a clear layer structure and correctly fitted content.

## 5. Refine the image

Match the product's typography, iconography, palette, and control conventions. Direct contrast toward the focal action. Use spacing and surface differences to clarify depth.

Write meaningful content where understanding depends on it. Simplify peripheral content without replacing the focal information with placeholder shapes.

Inspect baselines, optical alignment, repeated insets, corner relationships, and text fit. Keep device and window proportions consistent with the supplied reference.

Completion: clear at display size and coherent under close inspection.

## 6. Build behavior when requested

Choose between an interactive prototype with real hotspots and an autoplay sequence with timed state changes.

A drawn cursor is artwork: moving it does not activate a prototype hotspot. Wire the scene's transitions explicitly.

Define states before wiring them: context, action, selection or change, result, and replay if needed. Duplicate the base frame to retain corresponding layers. Preserve matching layer names and parent structure for Smart Animate.

Use variants for local component states and separate frames for larger scene changes. Animate supported properties and verify the result; unsupported changes may dissolve.

For entrances and exits, retain corresponding layers and adjust position or opacity where appropriate. Keep text readable during resizing through container changes, reflow, or separate text states.

Timing starting points, to tune after playback:
- Press feedback: 80–120 ms.
- Local transition: 180–300 ms.
- Larger movement: 350–600 ms.
- Result hold: 1,200–2,000 ms.

Use overlays where interactive menu behavior calls for them. For coordinated autoplay, scene-internal menu layers may be easier to control. Check available timeline tools before assuming a state-frame prototype is the only option.

Account for component and variable state when replaying. Make reset behavior deliberate and understandable.

Completion: understandable cause and effect, a readable result, and a working replay path when required.

## 7. Verify and hand off

Render the output and inspect hierarchy, text fit, clipping, alignment, assets, and fonts. Check compact layouts at their intended dimensions when requested.

When playback is available, inspect the whole sequence, including intermediate transitions and repeated playback. For interactive work, activate every intended hotspot and check dismissal and replay behavior.

Fix the largest visible defect first. If playback cannot be tested, report that limitation explicitly rather than inferring success from static frames.

Return links to the relevant frames or prototype when available, a brief description of the story, what was verified, and any unwired behavior. Keep working notes outside export frames. Export extra formats only when requested.

Completion: verified appearance, verified behavior where accessible, and an honest account of remaining limitations.

## References

Inspired by [StageShow by Benji Taylor](https://benji.org/stageshow); this is an independent Figma adaptation, not the original React skill.

For uncertain prototype behavior, consult Figma's current documentation:
- [Smart Animate](https://help.figma.com/hc/en-us/articles/360039818874-Smart-animate-layers-between-frames)
- [Matching objects](https://help.figma.com/hc/en-us/articles/21523793229463-Identify-matching-objects)
- [Plugin reactions](https://developers.figma.com/docs/plugins/api/properties/nodes-reactions/)
