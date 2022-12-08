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
- Useful when markup contains multiple namespaces.  Usually this means svg (which defaults to the `svg` namespace), or math elements (which defaults to the `math` namespace).
- There are some shenanigans with `attribute` selectors b/c they don't automatically inherit a namespace.

## Grouping
- a comma-separated list will apply the rules to elements matching each specified selector, e.g.
```css
a, li {
	text-decoration: none;
}
```
will apply the `text-decoration` rule to all `li` elements and all `a` elements.

## Combinators
- a sequence of simple selectors with separating space or combinator represents a set of conditions that must **all** apply to an element in order for it to be selected.  E.g. the selector `a.selected` applies to all `a` elements whose classes include "selected".
- `" "` (space) selects all elements matching the selector that follows the space that are also descendants of the selector preceding the space.  e.g.
```css
main article {

}
```
selects all `article`s that are inside a `main` elements.
- `>` selects *direct* children, i.e. exactly one level below the leading selector
- `~` selects all all elements matching the second selector that are siblings of the first  element **and** occur **after** the first  element.  NB rule will **not** be applied to the first selected element itself.  The second element need not immediately follow the first element in the document flow to be selected.
- `+` is similar to `~`, except that it selects the second element only if it **immediately** follows the first element.

## Functional
- functional selectors accept a forgiving list of selectors, which can help prevent a single invalid selector from blocking application to multiple elements
- `:where()` can help with narrowing a selector *without* increasing its specificity
- `:has()` can be used to select parent elements, but browser support isn't great
- `not()` matches any element that is **not** matched by any selector passed as a parameter.