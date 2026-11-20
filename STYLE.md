# Cheap.com — STYLE.md

> Design system specification for Travel Pocket / Cheap.com. Updated 2026-11-20.
> This document defines the **target standard**. Existing `index.html` styles may not yet fully comply. Do not treat the presence of this file as proof that the app has been migrated.

## 1. Universal corner radius

- **11px is the sole standard corner radius for every button**, across all pages, modals, bottom navigation, settings, form actions, icon buttons, upload controls, confirmation buttons, and other interactive buttons.
- Remove page-specific 9px, 10px, 12px, 14px, 18px, pill/999px button radii when implementing the migration, unless a control is not a button (e.g. circular indicator).
- Canonical token: `--cheap-button-radius: 11px`.
- Keep inputs and cards consistent where practical, but this rule specifically mandates **all buttons** be 11px; it does not automatically force every non-button container to 11px.
- Button states (hover, pressed, disabled, focus) must preserve the 11px radius.

## 2. Delete buttons: icon-only, no fill, no border

- **All ordinary item-deletion buttons** must use an accessible trash icon, with **no background and no border**.
- Use consistent red danger icon color (`var(--cheap-danger, #a83f53)`), icon stroke, sizing, alignment, and tap target.
- No visible “刪除” text on these item-delete buttons. Preserve `aria-label` and `title` (e.g. `aria-label="刪除連結"`).
- Keep touch targets comfortably usable (recommended at least 40 × 40px), without visible background/border; use transparent padding as needed.
- Use a common class `.tp-delete-icon-btn` rather than repeating conflicting styles in page-specific CSS.
- Applies to link management, itinerary stops and days, checklist items and categories, tickets, receipts, and other ordinary delete-item actions wherever they appear.
- Preserve confirmation flows and existing deletion behavior. Do not change data handling as part of styling.

### Explicit exception: API removal / disconnection

- Buttons for **removing, disconnecting, or clearing an API integration / API key** (e.g. RapidAPI key removal) are **not** converted to icon-only.
- These exceptional API actions may retain text labels, background, and borders for clarity and safety, but **their button corner radius must still be 11px**.
- Destructive **confirmation dialog** buttons may also retain explicit text labels (“刪除”, “確認刪除”) for accessibility and clarity; the icon-only rule targets ordinary item actions, not confirmation decisions.

## 3. Shared visual language (existing tokens)

| Purpose | Current token / value |
| --- | --- |
| Main text | `--cheap-ink: #173e62` |
| Secondary text | `--cheap-muted: #526e86` |
| Date text | `--cheap-date-color: #6385a4` |
| Danger | `--cheap-danger: #a83f53` |
| Field border | `--cheap-field-border: #cbdfee` |
| Glass border | `--cheap-edge: #ffffffcf` |
| Body text | `--cheap-text-body: 14px` |
| Small text | `--cheap-text-small: 12px` |
| Heading text | `--cheap-text-heading: 15px` |
| Shared control height | `--cheap-control-height: 44px` |

- Keep the existing pale-blue / translucent-white liquid-glass visual system.
- Keep main, secondary, and destructive actions distinguishable.
- Avoid introducing new one-off button radii or inconsistent delete-button treatments.

## 4. Implementation and verification checklist

- [ ] Add the shared 11px button radius token and apply it to all button types (including `button`, `.btn`, custom action classes, and buttons in modals/navigation).
- [ ] Remove higher-specificity conflicting button-radius overrides.
- [ ] Convert all ordinary delete-item buttons to the shared transparent, borderless trash-icon style.
- [ ] Preserve textual API removal/disconnection actions and textual destructive confirmation actions.
- [ ] Confirm keyboard focus, screen-reader labels, tap target size, and disabled/pressed states.
- [ ] Visually check Home, Itinerary, Other, Settings, link editor, checklist, ticket, receipts, and all modal screens on mobile.
- [ ] Confirm no business logic or stored data has changed.

## 5. Change scope

This update records the **approved design rules** in `STYLE.md`. Updating this document alone does not modify `index.html`, deploy the UI, or migrate existing styles.
