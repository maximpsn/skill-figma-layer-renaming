---
name: figma-layer-naming
description: Rename Figma layers by their role in the UI — predictable names from a fixed vocabulary instead of Frame 12, Group 5, Rectangle 3. Use when the user asks to «переименуй слои», «наведи порядок в слоях», «сделай нормальные названия слоёв», «почисти имена фреймов», «переименуй по нашим правилам», asks to name a frame that was just built in Figma, or asks for "rename layers", "clean up layer names", "layer naming", "name these layers properly". Works through the Figma tools (use_figma) and changes only layer `name`. Do NOT use for renaming components, component sets, variants or instances, for restructuring, regrouping or deleting layers, or for visual polish — those are different jobs.
---

# Figma layer naming

Rename only layer `name`. Never touch: components/sets/variants, instances
(keep component name), text content, vectors and masks inside icons, order,
nesting, visibility, styles.

Format: English, lowercase, spaces (`card header`, `actions right`), max 3
words. No digits, versions, new/final/copy, no sizes. Notes and refs: `_note`.

Name = role in the UI, not look, not content. `list row`, not `grey strip`.

## How to apply

1. Take the frame or page the user pointed at; if none, the current selection.
2. Walk the tree top-down — parent before child — reading children with
   `use_figma`.
3. Skip any node of type `COMPONENT`, `COMPONENT_SET`, `INSTANCE`: do not
   rename it and do not descend into it.
4. For every other node pick a name from the vocabulary below by its role, and
   write only `node.name`.
5. No readable role → keep the existing name. Never invent a name to have
   something to write.
6. Re-runs: leave valid names untouched. Then report how many layers were
   renamed and list the ones you could not name.

Batch the renames into as few `use_figma` calls as possible; renaming is
idempotent, so a failed call can simply be repeated.

## Role by depth

- page: header nav hero main sidebar footer modal overlay
- block: section card list table form gallery slider tabs accordion banner promo
  toolbar breadcrumbs pagination filter search profile summary faq reviews steps
- part: head body row cell item media actions controls info meta
- primitive: title subtitle label value caption hint link button input icon image
  avatar badge chip tag tooltip close bg divider spacer

## Modifiers

Only to split siblings: top bottom left right center fixed sticky primary
secondary small large dark light active disabled empty error loading

## Rules

- Do not repeat the parent: `card > header`, not `card > card header`.
- Replace auto names: Frame 12, Group 5, Rectangle 3, Text, Ellipse 2.
- Generic words (container, wrapper, inner, box, group) are fine when no role is
  readable.
- Repeated items share one name; Figma adds the numbering.
- Icons: `icon close` names the function, not the picture.
- Text layers by role, never by content.
- 3-second test: the layer is findable by name without expanding the tree.
- Traverse top-down, parent before child; never enter components or instances.

## Examples

| What it is | Name |
| --- | --- |
| Frame wrapping the top bar of a card | `head` |
| Two buttons pushed to the right | `actions right` |
| Row inside a settings list | `row` |
| The × in a modal corner | `icon close` |
| Caption under an input | `hint` |
| Comment left on the canvas | `_note` |
| Auto-named gap in a stack | `spacer` |
