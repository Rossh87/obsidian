## Attribute Selectors
- `a[attr]`: select all `anchor` elements that have an attribute named `attr`
- `a[attr=value]`: select all `anchor` elements that have attribute named `attr` whose value is exactly `value`
- `a[attr~=value]`: select all `anchor` elements whose value is a whitespace-separated list of words, **one** of which is exactly equal to `value`
- `a[attr|=value]`: select all `anchor` elements whose value is either exactly `value`, or begins with exactly `value` followed by a hyphen (`-`).
- `a[attr^=value]`: (same as regex) has `value` as prefix
- `a[attr$=value]`: (same as regex) has `value` as suffix
- `a[attr*=value]`: contains string `value` anywhere in attribute value
- `[attr operator value i`: adding `I` or `i` before the closing bracket makes the match case-insensitive.

## Namespace Selectors
