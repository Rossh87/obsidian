Modules are the mechanism for grouping views, services and other pieces into a single code unit.  An `Ng Module` is a single compilation context and should encompass code pieces that are related to each other: a single workflow, domain, or set of capabilities.

Modules have a tree structure: every application has a single root module, conventinally called `AppModule`, that serves as the entrypoint to the application.  

Modules can share functionality via the `imports` and `exports` fields, declared in the metadata passed to the `@NgModule` decorator.  Things like client-side routing, http, forms, and other functionality 'bundles' are made available to components by importing those modules in the module that declares those components.  Specifically, importing `ModuleB` into `ModuleA` makes any directives (e.g. `*NgFor` from `CommonModule`, or `([NgModel])` from `FormModule`) exported from `ModuleB` available to components in `ModuleA`.  A module can export another module *even if it does not import it*.  This useful in modules that bundle common functionality that will be used throughout the application, but whose own components do not themselves require these shared directives.

Module import/export also controls component availability.  A [[Declarable]] class can be declared **exactly once**, no matter what. Different modules cannot declare the same component.

Only the root module should provide a component in its `bootstrap` metadata.  This is the entrypoint for the module.  Submodules should be accessed by `import`ing them.

Modules are the basic unit of code for lazy-loading.  Note that lazy-loaded modules have some unique behaviors with regards to any [[Providers]] they provide.