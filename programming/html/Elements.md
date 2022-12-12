## <article/>
- https://html.spec.whatwg.org/dev/sections.html#the-article-element
- Rule of thumb: Use article if content can stand alone, e.g. a comment, a single blog post, a single article in a magazine archive page
- Often appropriate for `article` to have its own header/footer/heading/w/e
- Can be nested

## <aside/>
- https://html.spec.whatwg.org/dev/sections.html#the-aside-element
- Rule of thumb: <aside/> content is tangentially related to surrounding content but can be considered separate.  e.g. pull quote, a sidebar.

## <h*/>
- Headings form the outline of the document.  
- It is acceptable to have multiple `h1` elements at the top level, giving an outline like this:
1. Section 1
2. Section 2
3. Section 3
-  Not that neither `title` nor `header` impact the document outline
- It can be helpful to place compound headings inside the <hgroup/> tag

## <section/>
-  https://html.spec.whatwg.org/dev/sections.html#the-section-element
- Rule of thumb: if the grouped content would appear as an entry in an outline of the document, <section/> is likely appropriate.
- **NOT** a generic container element--use div if grouping is for scripting/styling purposes.
- A <section/> has the [[ARIA]] role of `region` by default, *as long as it has an accessible name*.  Assign an accessible name using the `aria-labelledby` attribute.
- Can be nested
