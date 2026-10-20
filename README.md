# design-system

Design tokens shared across my projects, so they all use one design language.

`tokens.mjs` is an unchanged copy of `src/styles/tokens.mjs` from [julianhilgemann.com](https://github.com/julianhilgemann/julianhilgemann.com) (commit `78eb63c`). Its comments still point at files in that site, which remains the reference implementation and still has its own copy for now.

## What's in it

- **Colour:** a dark background and surfaces, a four-step `ink` scale for text, orange `primary` (the number, every call to action) and blue `info` (system, structure), hairlines and washes at fixed opacities, a validated chart palette (`viz`) and the gradient-sheet palette.
- **Type:** system font stacks and fluid type steps that scale between a 375px phone and a 1280px desktop.
- **Space, layout, radius, shadow:** gutters, section rhythm, content width, corner radii.
- **Motion:** durations, easings, card lift, button press and the GSAP reveal values.
- **Helpers:** `channels`, `mixHex`, `rgba`, and `cssVariables()`, which returns every token as a CSS custom property on `:root`.

## Use as a submodule

```sh
git submodule add https://github.com/julianhilgemann/design-system.git design-system
```

```js
import { color, rgba } from "./design-system/tokens.mjs";
```

In a Tailwind project, add the custom properties as base styles with `plugin(({ addBase }) => addBase(cssVariables()))`. The `tailwind.config.mjs` in julianhilgemann.com shows how to point the utilities at them.

To pick up later changes in a project that uses it:

```sh
git submodule update --remote design-system
```
