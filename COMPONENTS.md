# Components (v1)

All components read `mapped.*` and `responsive.*` tokens only. Every one exists in dark and light, desktop and mobile, by switching variable modes.

## Button
- Variant: Primary, Secondary, Ghost, Destructive. State: Default, Hover, Disabled. Size: Medium (40 desktop / 44 mobile), Small (32 / 36).
- Properties: Label, Icon left, Icon right (swappable), Focused.
- One Primary per view. Primary is the inverse of the page (mono accent). Red only for Destructive.
- Motion: scale 0.97 on pointer down, 160ms ease-out. No animation on keyboard activation.

## Input
- State: Default, Hover, Focused, Error, Disabled. Filled: No, Yes.
- Properties: Label, Show label, Required, Helper, Show helper, Leading icon (swappable), Value.
- Required asterisk before the label, neutral color. Error = icon + message that says what to do.
- Field 40 / 44. Edge uses `border.control` (3:1).

## Checkbox
- Value: Unchecked, Checked, Indeterminate. State: Default, Hover, Error, Disabled.
- Properties: Label, Show label, Description, Show description, Error message, Focused.
- 20px box, whole row is the hit target. Keyboard toggles instantly; pointer crossfades 150ms.

## Radio
- Value: Unselected, Selected. State: Default, Hover, Error, Disabled.
- Properties: Label, Description, Show description, Error message, Focused.
- Always in a labeled group of 2 to 5. Arrow keys move instantly. Dot enters from scale 0.95.

## Toggle
- Value: Off, On. State: Default, Hover, Disabled. No error state (takes effect immediately).
- Properties: Label, Description, Show description, Focused.
- Label leads, switch trails. Knob slides on spring (bounce 0), interruptible, draggable.

## Badge
- Variant: Neutral, Solid, Outline, Error. Size: Medium (24), Small (20).
- Properties: Label, Icon, Icon glyph.
- Not clickable. No green or yellow: status = icon + word.
- Text in the `label` style (JetBrains Mono Medium 12).

## Avatar
- Type: Image, Initials, Icon. Size: 24, 32, 40, 56.
- Properties: Initials.
- 1px inner border. Tappable avatars get a 44px hit target. Image fades in 150ms.

## Tabs
- Style: Underline (web navigation), Segmented (2 to 5 options, Apple pattern).
- Built from private `.Tab` (Default, Hover, Selected, Disabled).
- Indicator slides 200ms ease-in-out; content swaps instantly. Arrow keys instant.

## Table
- Built from private `.Cell` (Header, Header right, Text, Number, Checkbox, Badge, User, Action) and `.Row` (Header; Body Default, Hover, Selected).
- Properties: Title, Description, Show title.
- Rows 44, header 36. Header text in `label`, numbers in `code` (both JetBrains Mono), text cells in Geist. Numbers right-aligned. On phones switch to a list or pin the first column.

## Card
- Style/State: Static Default, Interactive Default, Interactive Hover.
- Properties: Title, Description, Meta, Show meta, Show media, Focused.
- Meta in `label` (JetBrains Mono); title and description in Geist.
- Interactive cards contain no buttons. Hover steps the border to strong, no lift.

## Modal
- Type: Dialog (440), Destructive (confirm), Sheet (mobile).
- Properties: Title, Description.
- Over `effect.scrim`. Focus trapped and returned. Dialog enters from 0.95 + fade 250ms; sheet slides 350ms on the drawer curve.

## Mode rail
- Mode: Paper (striped neutral), Live (solid `surface.error`, `text.on-error`). Sandbox products use Paper.
- Properties: Label (sentence case, wraps, 12px minimum), Icon.
- Pinned above all navigation, on every screen, including pushed ones. Never inside a scroll view, never under the nav bar.
- Live is the one place red describes state rather than an error, because every action there spends real money.

## List row and grouped section
- Row: Value (label leads, value trails), Navigation (chevron), Toggle, Custom. Section: Title (caption, sentence case), Footer.
- Rows 44 minimum, 1px `border.default` dividers inset to the text. Section is a Card with no padding between rows.
- Numbers trail and right-align.

## Notice
- Variant: Neutral, Error. Properties: Title, Message, Icon.
- Inline, on `surface.default` with a 1px border. Status is the icon plus the title; no color but red for Error.

## Countdown
- Urgency: Calm (`text.secondary`), Warning (`text.primary`, semibold, `border.control`), Critical, final minute (`text.error`, `border.error`).
- Badge-sized: ring plus `m:ss` in the `label` style. Critical pulses opacity only, and holds still under reduced motion.
- Says "expiring", never "expired": the server decides that.

## P&L value
- Sign, triangle and amount in `data.gain` or `data.loss`; zero in `text.secondary` with neither. Sub-cent digits in caption `text.tertiary`.
- Accessible label reads "Up 12.40" or "Down 3.10".

## Empty state
- Properties: Title, Message, Icon, Action (optional, Secondary).
- Says why it is empty and what fills it. Never a bare "No data".

## Code block
- `surface.default`, 1px border, radius md, body-small code style with ligatures on. Horizontal scroll, never wrap. Copy action trails.

## Sheet layout
- Title, content, then actions pinned to the bottom: Primary full width, Cancel as Ghost above or beside it. Destructive confirms use the Destructive button.
- On iOS it is the system sheet (see PRINCIPLES 9). Medium detent for a confirm, large when the sheet asks for typing or reading.

## Navigation and tab bars
- Platform chrome. On iOS, system bars with Liquid Glass; titles in Geist where iOS honours it. On web, a sticky bar on `effect.glass`.
- 2 to 5 tabs, icon plus short label, selected state from the platform.

## Icons
- Web and React Native: 16px, 1.5 stroke, round caps. Plus, Arrow right, Arrow left, Check, X, Chevron down, Chevron right, Alert, Info, Search, Minus, User.
- iOS: SF Symbols, sized and weighted to the adjacent text (PRINCIPLES 9).
- Color always from `icon.*` tokens.
