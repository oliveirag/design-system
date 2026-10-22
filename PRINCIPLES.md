# Principles

House rules for every screen, component, and animation in this system.
Sources: Emil Kowalski (emilkowal.ski, emilkowalski/skill), Apple HIG and UI Design Dos and Don'ts, UI Collective (Kirk) token structure.
Platforms: web, React Native, and native iOS (SwiftUI). Platform-specific rules are in section 9.

## 1. Identity

- Achromatic. Neutrals only, anchored on Almost Black `#171717` and White `#FFFFFF`.
- Mono accent: the primary action is the opposite of the page. White on dark, `#171717` on light.
- Two typefaces. Geist is primary: everything the user reads or taps. JetBrains Mono is secondary: small labels and data (badges, table headers and numbers, meta lines, section tags, code). Geist weights 400, 500, 600; JetBrains Mono 400, 500. Never Thin, ExtraLight, Light, or anything above 600.
- Dark-first. Design in dark mode, then verify light.
- Restraint over options. If a token or variant is not used by a real component, it does not exist.

## 2. Color

- Components only read `mapped.*` tokens. Never `brand.*`, never raw hex.
- One color means one thing. Red means error or destructive, nothing else. The only other hues are the two data colors in section 2a.
- Never rely on color alone. Status always gets an icon and words. Links are always underlined.
- There is no success, warning, or info color. Use the neutral surface plus an icon and a label.
- Four kinds of feedback, each answered: status (what is true now), completion (it worked), warning (it might not), error (it did not, and what to do). A screen that changes state without one of these is a bug.
- Every text pair meets WCAG AA 4.5:1 in dark and light. Large text (18px and up) may drop to 3:1.
- No exemptions: disabled, placeholder, and caption text also meet 4.5:1. Show disabled with a flat surface and no border, never with faded text.
- Never lower text opacity. Use a text token instead.
- Control edges (input borders, unchecked boxes, toggle tracks) meet 3:1 against what they sit on. Use `border.control`, not `border.default`.
- Light mode `text.tertiary` only sits on `surface.page` or `surface.default`.
- Dark mode shows depth with lighter surfaces and borders, not shadows. Shadows are light mode only.
- Glass (translucent blur) is for nav bars, tab bars, and toolbars only. Never on content. Never glass on glass.
- Support `prefers-reduced-transparency` (solid surfaces) and `prefers-contrast: more` (stronger borders).
- Cards keep their 1px `border.default` stroke in light mode. `surface.default` on `surface.page` is too close to read on its own.

## 2a. Financial data

Products that show money (Ollie) use two data colors. Nothing else may.

- `data.gain` and `data.loss` color a signed P&L figure and its direction triangle. Nothing else: not buy or sell, not a badge, not a surface, not a row background.
- Color is never the only cue. Gain is `+` and a filled up triangle; loss is a true minus `−` and a filled down triangle. It must read in grayscale.
- Zero is neutral: `text.secondary`, no sign, no triangle.
- Loss is never the same red as error (`red.300` dark, `red.700` light, against error's 400 and 600). A losing trade is a result, not a failure.
- Buy and sell are `plus.circle` and `minus.circle` in `icon.primary`, never arrows. A losing buy should not show two arrows pointing opposite ways.
- Money is a string end to end. Never round through a float for display. Pad to two decimals; sub-cent digits drop to caption size in `text.tertiary`, never below 12px.
- Prices, counts and timers use tabular figures: JetBrains Mono, or Geist with `font-variant-numeric: tabular-nums`.

## 2b. Charts

- One series: the line is `data.series` (same as `text.primary`), 2px, round caps and joins, monotone interpolation.
- Gridlines `data.grid`. Axis labels caption size in `data.axis-label`.
- The zero or break-even rule is `data.zero`, 1px, dashed 4 on 4 off. It is the most important line on a P&L chart.
- Missing data breaks the line. Never interpolate across a gap; say so in words below the chart.
- One point is not a chart. Below two points, show a sentence instead.
- Fixed height (180 on phones). No legends for a single series. No gradient fills.

## 3. Typography

- Body is 16px with 24px line height. Headings use 1.2x, body uses 1.5x, rounded to the 4px grid.
- Minimum text size is 12px (caption, label). Never smaller.
- Which font: a label, a number in a table, or code uses JetBrains Mono (`label` or `code` style). Everything else is Geist.
- Hierarchy comes from weight, size, and color together, not size alone.
- Tracking: 0 for body and for anything in JetBrains Mono. Headings tighten as they grow: -0.01em at 20 and 24px, -0.02em at 32px, -0.025em at 40px, -0.03em at 48px. No positive tracking.
- Turn off programming ligatures in JetBrains Mono UI text (`font-variant-ligatures: none`). Keep them in code blocks.
- Use tabular figures for anything that changes (timers, prices, counters).
- Respect the user's text size setting. Size layouts in rem on web and scale with font scale in React Native.
- Line length: 45 to 75 characters on desktop. Keep mobile paragraphs short.
- Why two fonts, against Apple's "use the system font unless you have a reason": Geist reads faster at body sizes, has a real SemiBold for headings, and matches One Tap. JetBrains Mono keeps the system's identity where it earns it: labels and numbers that line up. System chrome (iOS tab bars, back buttons) stays in SF. Do not fight it.
- Ship exactly five font files, each family from one release so metrics match: Geist Regular, Medium, SemiBold; JetBrains Mono Regular, Medium.

## 4. Layout and spacing

- Everything is a multiple of 4. The only exceptions are 1px and 2px borders.
- Spacing comes from `responsive.space.*`, which comes from `brand.scale.*`.
- Tap targets are at least 44x44. Smaller visuals get invisible hit padding.
- Put controls next to the content they change. Align things that are related.
- Order content by importance: most important at the top and leading edge.
- Show the common path first. Advanced options one level deeper.

## 5. Motion

Decide in this order.

1. Should it animate? Seen 100+ times a day or triggered by keyboard: no animation. Tens of times a day: barely. Occasional (modals, toasts, drawers): yes. Rare (onboarding, celebrations): can add delight.
2. What is it for? Feedback, spatial continuity, state change, or preventing a jarring jump. "Looks cool" is not a purpose.
3. Easing. Entering or exiting: `motion.easing.out`. Moving on screen: `in-out`. Sheets: `drawer`. Spinners: `linear`. Never ease-in.
4. Duration. Press 160ms, tooltip 150ms, dropdown 200ms, modal 250ms, drawer 350ms. UI motion stays under 300ms.

Rules:

- Press feedback: `scale(0.97)`, triggered on press down, not release.
- Never animate from `scale(0)`. Enter from `scale(0.95)` with opacity 0.
- Popovers and menus grow from their trigger. Modals stay centered.
- Things leave the way they came in, faster than they arrived (about 75% of the enter duration). Slow where the user decides, fast where the system answers.
- Lists that appear together stagger by `motion.duration.stagger` (50ms, range 30 to 80). Cap the total at 300ms; never block input while it runs.
- A crossfade between two states that differ in shape gets `motion.blur-transition` (2px) on the outgoing layer to hide the double image. Nowhere else.
- Only animate `transform` and `opacity`.
- Anything touchable uses springs: `motion.spring.default` (no bounce). Bounce only after a flick (`momentum`).
- Every animation can be interrupted and reversed mid-flight. Never lock input during a transition.
- Drag tracks the finger 1:1 from where it was grabbed. Release hands off the finger's velocity into the spring as its initial velocity.
- Decide where a throw lands by projecting it: `distance = velocity / 1000 * rate / (1 - rate)` with `rate = 0.998` (normal deceleration). Snap to the target nearest the projection, not to where the finger let go.
- Dismiss by velocity or distance: a flick faster than 0.11px/ms dismisses even if it travelled only a little.
- Ignore a second finger once a drag starts. Capture the pointer so the drag survives leaving the element.
- Hover effects only where hover exists: `@media (hover: hover) and (pointer: fine)`. Touch never sees a stuck hover state.
- Boundaries rubber-band instead of stopping hard: `offset = (1 - 1 / (overshoot * 0.55 / dimension + 1)) * dimension`.
- First tooltip waits. Tooltips after it open instantly.
- Reduced motion: replace movement with a 150ms opacity crossfade. Keep the feedback, drop the travel.

Implementation:

- Never `transition: all`. Name the properties.
- Interruptible UI uses CSS transitions, not keyframes. Under load, CSS or WAAPI over main-thread JS.
- Review motion at slow speed (10% in devtools, Slow Animations in the simulator), then again the next day with fresh eyes.

## 5a. Haptics and sound

- Causality: a haptic fires exactly when its cause happens (touch-down, the commit, the snap), never after a network wait the user cannot see.
- Harmony: the haptic matches what is seen and heard. A light tap for a selection, a firm one for a commit.
- Utility: use them for outcomes that matter, not for every tap. If everything buzzes, nothing does.
- Map them to the four feedback kinds: success on completion of a decision, warning before something irreversible, error when it failed. Selection ticks for pickers and snapping.
- Respect the system setting. Never a haptic without a visible change. No custom sounds.

## 6. Components

- Every component has a stroke, even when it matches the fill, so adding one later never breaks instances.
- States: default, hover, pressed, focus, disabled. Focus is a 2px `border.focus` ring with 2px offset.
- Avoid disabled buttons where possible. Keep them enabled and explain on press.
- One primary (`surface.action`) button per view. Everything else is secondary or ghost.
- Confirmation dialogs only for destructive, irreversible actions. Prefer undo.
- Required field asterisk goes before the label.
- Fields use `border.control` at rest (3:1 against the card). `border.strong` fails 3:1 and is for dividers only.
- Private sub-components are prefixed with `.` so Figma does not publish them.
- Text, icon, and layer visibility are component properties. Nested instances expose their properties.

## 7. Copy

- Sentence case everywhere. Verb-first buttons, 1 to 3 words.
- Errors say what happened, then what to do.
- No "please", no "successfully", no exclamation marks in system copy.

## 8. Taste

- Unseen details compound. Get the ones nobody will notice right.
- Simplicity is not minimalism. Remove what is unnecessary, keep what gives context.
- Before shipping, check: contrast, 44px targets, reduced motion, light mode, largest text size.
- Wayfinding: on every screen the user can tell where they are (title), how they got here (back), and where they can go (visible actions). Persistent modes (paper or live, a sandbox) are always on screen, not only on the screen that sets them.

## 9. Native iOS (SwiftUI)

- Tokens: `mapped`, `responsive` (mobile mode) and `motion` mirror into a Swift `DS` namespace. Views read names, never hex. Until a generator exists, change `tokens.json` first, then the Swift copy, in the same change.
- Dynamic Type: every style scales through `UIFontMetrics` from the text style below. Layouts must survive accessibility sizes (scroll, do not clip).
  - display: largeTitle. h1: title1. h2: title2. h3: title3. h4: headline.
  - body-large and body: body. body-small: subheadline. code: callout. caption and label: caption1.
- Icons: SF Symbols, not the 16px web set. Match the symbol to the adjacent text's size and weight; use `.medium` scale with body, never a symbol heavier than its label.
- Liquid Glass: tab bars, toolbars, navigation bars and scroll edge effects are system materials on iOS 26 and later. Use them as they ship; do not paint `effect.glass` on them. Never glass on content.
- Sheets: use the system sheet and its spring. Do not restyle the presentation or re-time it with the drawer curve. Pick detents (medium, large) by how much the sheet asks of the user.
- System chrome keeps the system font where iOS ignores appearance overrides (iOS 26 tab bar titles, back button). Do not hack around it.
- Haptics: `sensoryFeedback` with the kinds in 5a.

