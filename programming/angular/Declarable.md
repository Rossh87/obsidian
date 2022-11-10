There are three classes in Angular that are considered declarables: components, directives, and pipes.

**Components** generally handle data bindings and state for a single unit of UI.  They are associated with an HTML template that describes the rendered UI itself.

**Directives** add additional behavior to elements in the app.  Components are actually a kind of directive, but usually we mean either **attribute** or **structural** directives.

**Attribute** directives include many built-in directives like `NgFor` and `NgClass` that add special behaviors to DOM elements.  Importing modules like `FormsModule` makes attribute directives associated with the imported module available in components declared by the importing module.