---
title: Design tokens
---

Edit all your preferences (colors, fluid text sizes etc.) in `src/_data/designTokens/*.json`.

Additional colors, variants and gradients for custom properties are automatically created in `src/assets/css/global/base/variables.css` based on the colors set in `colors.json`.

In the [style guide](/styleguide/) you can see how everything turns out.

**Special case: colors**

As of version 4.0, you can create colors dynamically. Run `npm run colors` after setting your color values in `src/_data/designTokens/colorsBase.json`. This will create / overwrite the required `colors.json` file in the same directory. These colors become custom properties (e.g. `--color-gray-100`) and utility classes similar to the Tailwind CSS syntax (for example `bg-gray-100`, `text-gray-900`).

If you want to adjust how the colors turn out, edit `src/_config/setup/create-colors.js`.

Placed under `neutral` or `vibrant`, colors are converted into scalable palettes. `neutral` is better for grayish / monochromatic colors, while `vibrant` is better for colorful palettes. Colors listed under `fixed` remain as standalone values without generating shades. Each color placed here also generates a "subdued" version for the dark theme.

```js
// this creates a palette with shades of green, 100 to 900
  "vibrant": [
    {
      "name": "green",
      "value": "#008000"
    }
  ],
```

<strong class="text-pink">Important:</strong> If you change the color names, you must edit `src/assets/css/global/base/variables.css` with your color names. The rest of the CSS files should only reference custom properties set in `variables.css`.