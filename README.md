
# loadly

Nine CSS loading spinners built for the two things most spinner libraries ignore: **reduced motion** and **high contrast mode**.

No JavaScript. No dependencies. No build step. ~1KB per spinner.

Written from scratch. Prior art credited in [CREDITS.md](CREDITS.md).

**[Live demo](index.html)** - open `index.html` in any browser.

## Why another spinner library

Most spinner libraries were written before accessibility became a procurement requirement. They animate regardless of the user's OS settings, disappear in Windows High Contrast, and ship a monolith so you pay for twenty spinners to use one.

Loadly is the opposite shape.

| | typical spinner lib | loadly |
|---|---|---|
| Respects `prefers-reduced-motion` | rarely | every spinner slows or swaps to a fade |
| Survives forced-colours mode | no | gradients become borders |
| Screen-reader label | manual | built in |
| Ships only what you import | no | one file per spinner |
| Size, weight, colour, speed, gap as tokens | no | all five |
| JavaScript | often | none |
| Licence | often unclear | MIT |

## Install

Copy one file. Nothing to configure.

```
src/ring.css   src/orbit.css   src/pulse.css   src/dots.css   src/bars.css
src/grid.css   src/square.css  src/sweep.css
```

Import the tokens once, then the spinner you want:

```css
@import "loadly/tokens.css";
@import "loadly/ring.css";
```

Or with a bundler:

```js
import "loadly/tokens.css";
import "loadly/ring.css";
```

Or paste the tokens and one spinner straight into your own stylesheet.

## Use

```html
<span class="ld-ring" role="status">
  <span class="ld-label">Loading</span>
</span>
```

Tune on the element or on `:root`:

```css
.ld-ring {
  --ld-size: 24px;
  --ld-color: rebeccapurple;
  --ld-weight: 2px;
  --ld-speed: 0.9s;
}
```

Centre with `ld-center`.

## Spinners

| class | shape | notes |
|---|---|---|
| `ld-ring` | bordered ring | simplest, widest support |
| `ld-orbit` | masked gradient arc | needs `conic-gradient` |
| `ld-pulse` | three expanding rings | one element |
| `ld-dots` | hop, three dots | one element |
| `ld-bars` | scaleY wave, four bars | inline |
| `ld-grid` | nine-cell fade wave | one element + `<i>` |
| `ld-square` | rolling square | mechanical, border-based |
| `ld-sweep` | travelling highlight | for inline and top-of-page |

## Tokens

| token | default | |
|---|---|---|
| `--ld-size` | `40px` | box size |
| `--ld-color` | `currentColor` | inherits text colour |
| `--ld-weight` | `3px` | stroke thickness |
| `--ld-speed` | `1.2s` | one cycle |
| `--ld-easing` | ease | timing function |
| `--ld-gap` | `0.18em` | spacing |
| `--ld-width` | `160px` | width, `ld-sweep` only |

## Accessibility

- `prefers-reduced-motion: reduce` slows every spinner and swaps movement for opacity where movement is the whole point. A frozen spinner reads as a broken page; a slow one still reads as alive.
- `forced-colors: active` replaces gradients with borders and pins colour to `CanvasText`.
- `.ld-label` is a visually hidden text node. Pair it with `role="status"` and the change is announced once.
- Animations use only `transform` and `opacity`, so they stay on the compositor and never trigger layout.

## Browser support

Evergreen Chrome, Firefox, Safari and Edge. Custom properties and `conic-gradient` are baseline. No IE. `color-mix` has a `@supports` fallback.

## Credits

See [CREDITS.md](CREDITS.md). Conceptual debt to SpinKit by Tobias Ahlin.

## Licence

MIT, Copyright (c) 2026 loadly.
