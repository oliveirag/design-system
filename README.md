# design-system

An achromatic, dark-first design system for web, React Native and iOS.

- Neutrals only, built on `#171717` and `#FFFFFF`. The primary action is the inverse of the page.
- Geist for everything you read or tap. JetBrains Mono for labels, numbers and code.
- Dark and light themes. Desktop and mobile sizes.
- Rules drawn from Apple's Human Interface Guidelines and Emil Kowalski's interface and motion principles.

## What's inside

- `tokens/tokens.json`: every color, type, spacing, radius and motion value, in the W3C Design Tokens format.
- `PRINCIPLES.md`: the rules for color, type, layout, motion and accessibility.
- `COMPONENTS.md`: the components, with their variants, states and behavior.

## How to use it

1. Copy `tokens/tokens.json` into your project, or convert it to CSS variables or a theme with a tool like [Style Dictionary](https://styledictionary.com).
2. In components, use the `mapped` and `responsive` tokens, like `mapped.text.primary`, `mapped.surface.default` or `responsive.space.md`. Never raw hex values or `brand` tokens.
3. Read `PRINCIPLES.md` before designing a new screen or component.

Fonts: load [Geist](https://fonts.google.com/specimen/Geist) and [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) from Google Fonts on the web, or bundle them in a native app. Both are free under the SIL Open Font License.

## Also in

- [Figma](https://www.figma.com/design/UCRpBaSIdmQaDTVWPm8v4F)
- [Claude Design](https://claude.ai/artifact/JXMM6qazE1pxYkXXHxCbuF)

## License

MIT. Use it, fork it, ship it.
