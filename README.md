# loadly

Small, accessible CSS loading spinners. No JavaScript, no dependencies, no build step required.

Written from scratch by [adam123gale-byte](https://github.com/adam123gale-byte). Prior art credited in [CREDITS.md](CREDITS.md).

**Status:** early. Three spinners, more coming.

## Why another spinner library

Most spinner libraries predate two things that now matter: reduced motion and high-contrast mode. Loadly is built around them rather than retrofitted.

| | typical spinner lib | loadly |
|---|---|---|
| Respects `prefers-reduced-motion` | rarely | yes, slows rather than stops |
| Survives Windows High Contrast | no | yes, falls back to borders |
| Screen reader label | manual | built in |
| Ships only what you import | no | one file per spinner |
| Speed, weight, colour, gap as tokens | no | all four |
| Licence | often unclear | MIT |

## Install

Copy one file. There is no bundler to configure and no JS to load.

```
src/orbit.css   src/pulse.css   src/bars.css
```

Each spinner is self-contained apart from the shared tokens. Either:

**A. Import the tokens once**, anywhere in your CSS:

```css
@import "loadly/src/_shared.css";
@import "loadly/src/orbit.css";
```

**B. Or paste tokens and one spinner** into your own stylesheet, and delete what you don't use.

## Use

```html
<span class="ld-orbit" role="status">
  <span class="ld-label">Loading</span>
</span>
```

Tune it on the element or on `:root`:

```css
.ld-orbit {
  --ld-size: 24px;
  --ld-color: rebeccapurple;
  --ld-weight: 2px;
  --ld-speed: 0.9s;
}
```

Centre it with `ld-center`. Override `--ld-easing` to change the feel.

## Spinners

| class | shape |
|---|---|
| `ld-orbit` | gradient arc on a masked ring |
| `ld-pulse` | three staggered expanding rings, one element |
| `ld-bars` | four bars on a scaleY wave |

## Tokens

| token | default | |
|---|---|---|
| `--ld-size` | `40px` | box size |
| `--ld-color` | `currentColor` | inherits text colour |
| `--ld-weight` | `3px` | stroke thickness |
| `--ld-speed` | `1.2s` | one cycle |
| `--ld-easing` | ease | timing function |
| `--ld-gap` | `0.18em` | spacing in `ld-bars` |

## Accessibility

- `prefers-reduced-motion: reduce` halves the speed instead of freezing. A stopped spinner reads as a broken page.
- `forced-colors: active` swaps gradients for borders and pins colour to `CanvasText`.
- `.ld-label` is a visually hidden text node. Pair it with `role="status"` so the change is announced once.
- Animations use only `transform` and `opacity`, so they stay on the compositor.

## Browser support

Evergreen Chrome, Firefox, Safari and Edge. Needs custom properties and `conic-gradient`; both are baseline. No IE.

## Credits

See [CREDITS.md](CREDITS.md). Conceptual debt to SpinKit by Tobias Ahlin.

## Licence

MIT, Copyright (c) 2026 adam123gale-byte.
