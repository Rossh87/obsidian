Pseudo elements are used to select a specific sub-part of an element.  Contrast with [[Pseudo-classes]], which select based on element *state*.

Double-colons `::` should be used to distinguish from pseudo-classes.

`::before` and `::after` pseudo-elements create a pseudo-element that is the first/last child of the selected element.  The created element is `inline` by default.  Often combined with the `content` property, which replaces the selected element with an anonymous [[Replaced Elements]] containing the markup specified in the CSS `content` rule.  The generated element can be styled by adding more rules in the same declaration block as the `content` rule.