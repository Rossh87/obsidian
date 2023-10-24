CSS vars are declared in a ruleset like any other property.  The ruleset's selector sets the scope within which specified custom properties are meaningful. It is a common best practice to define global vars in the `:root`  [[Pseudo-element]], but there may be cases where it is desirable to limit the scope of variable declarations.

Normal specificity/cascade rules apply.

One use-case for scoping variables is to use a single, semantically-named variable to accomplish something that should have different values based on the element the var is applied to. For example, we might want an wrapper class that adds `margin-top` to every child after the first, to create spacing between headings, paragraphs, etc. That might look like this:
```css
// Select every sibling of the first descendant of class 'flow'
.flow > * + * {
	// use 'em' so that spacing will adjust according to the element's font-size
	margin-top: 1em;	
}
```

For some elements, we may want more than 1em of top margin, others less. To vary the value of `margin-top` for elements selected by the `.flow` class, we can use a variable, and then set the value of the variable scoped to specific elements:
```css
h1 {
	--flow-space: 2em;
}
h2 {
	--flow-space: 1.4em;
}

.flow > * + * {
	// 1em becomes fallback
	margin-top: var(--flow-space, 1em);
}
```