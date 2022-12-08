https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes

`Pseudo-classes` allow selecting elements based on some aspect of their state, including state that is intrinsic to other browser APIs, like mouse position or navigation history.

A quick list of some of the more useful ones:

## Input
- `:enabled/:disabled`: applies to interface element in one of these two states
- `:checked`: matches checkboxed and radio buttons that are currently selected
- `:valid/:invalid/:user-invalid`: matches element whose contents are in the matched state.  e.g. a text input of type `email` with a plain name typed into it

## Location
- `:visited`: match links that have been visited
- various `target` selectors: match elements in relation to intra-document navigation links

## Tree-Structural
- `:first-child/:last-child`: matches element that is the first/last of its siblings, i.e. that is the first or last child of its immediate parent.  All `child` selectors work this way: they select elements based on their position amongst their own siblings.
- `nth-child(specifier)`: select elements according to their position in an indexed list of all sibling elements.  For specifiers `even` and `odd`, the list is 1-indexed.  Functional notation can also be used, in the format `An + B`, where `A` can be considered the "jump", `B` the offset, and `n` is the list of nonnegative integers (beginning with 0).  E.g. `2n + 1` gives the sequence `1, 3, 5, ...`, which is the same as keyword `odd`.
- `:nth-of-type(specifier)/only-of-type`: similar to above, except when numbering siblings it skips elements that are not of the requisite type.

## User Action
- `hover`
- `:focus`
- `:focus-within`: matches element that has focus, or any element that has a descendant to which focus applies

