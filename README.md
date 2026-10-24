# design-system

Design tokens shared across my projects, so they all use one design language.

`tokens.mjs` started as a copy of `src/styles/tokens.mjs` from [julianhilgemann.com](https://github.com/julianhilgemann/julianhilgemann.com) (commit `78eb63c`). It is now the single source for that site too, which renders the whole system at [julianhilgemann.com/design-system](https://julianhilgemann.com/design-system).

## What's in it

- **Colour, in two themes:** a page colour and surfaces, a four-step `ink` scale for text, orange `primary` (the number, every call to action) and blue `info` (system, structure), hairlines and washes at fixed opacities, a validated chart palette (`viz`), the gradient-sheet palette, shadows and the dialog scrim. `dark` is the original; `light` keeps the same roles on a pale ground, with the accents stepped down to hold 4.5:1 as text.
- **Type:** system font stacks and fluid type steps that scale between a 375px phone and a 1280px desktop.
- **Space, layout, radius:** gutters, section rhythm, content width, corner radii.
- **Motion:** durations, easings, card lift, button press and the GSAP reveal values.
- **Helpers:** `channels`, `mixHex`, `rgba`, `theme(name)`, and `cssVariables(name)`, which returns every token as a CSS custom property on `:root`.

## Themes

| Site | Theme |
| --- | --- |
| [julianhilgemann.com](https://github.com/julianhilgemann/julianhilgemann.com) | light |
| [hyperadapted.com](https://github.com/julianhilgemann/hyperadapted.com) | dark |
| [ecosystem_graph_app](https://github.com/julianhilgemann/ecosystem_graph_app) | dark |

The top-level `color`, `alpha`, `viz`, `gradientSheet`, `shadow`, `scrim` and `focus` exports, and `cssVariables()` with no argument, are the dark theme: what this module exported before the light theme existed. A dark site imports them as they are.

A light site picks its theme in one place and re-exports it under the same names, so the rest of its code is theme-agnostic:

```js
// src/styles/tokens.mjs in the consuming site
import * as ds from "../../design-system/tokens.mjs";
export const { font, type, space, layout, radius, glass, motion, button, channels, mixHex, rgba } = ds;
export const { color, alpha, viz, gradientSheet, shadow, scrim, focus, cssVariables } = ds.theme("light");
```

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

Then commit the new submodule pointer in that project.
