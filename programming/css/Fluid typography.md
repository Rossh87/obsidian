1. https://www.smashingmagazine.com/2022/01/modern-fluid-typography-css-clamp/
2. https://www.youtube.com/watch?v=RctP49SwyT0

## Approach one:
Use media query breakpoints to set a fixed size at or below certain widths, set a midrange within which the font size will scale incrementally based on current width by using a combination of `cacl` and `vw` units, then set a max width at which the font size becomes fixed again.

## Approach two:
Outcome is the same as above. Fluid behavior became so common that a new CSS property was introduced to streamline it: `clamp`. Note that the fluid midrange still has to be set using some kind of relative unit, `clamp` does not make anything fluid itself, it just streamlines the min/max behavior.

`clamp` can be used with any attribute that accepts a numeric value type. And browser support is good. Fallback on unsupported browsers by setting a fixed value *before* the `clamp` value, e.g.
```css
.fluid {
	font-size: 16px;
	font-size: clamp(12px, [scaling calculation], 20px);
}
```

## Principles
One good use is to make headings scale faster than regular text. E.g. on very wide screens, we generally want `H1` to be *very* large relative to body text, but much closer in size on mobile. To achieve this, use `clamp` with a more aggressive scaling factor than body text.