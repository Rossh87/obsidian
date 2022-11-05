Modules are the mechanism for grouping views, services and other pieces into a single code unit.  An `Ng Module` is a single compilation context and should encompass code pieces that are related to each other: a single workflow, domain, or set of capabilities.

Modules have a tree structure: every application has a single root module, conventinally called `AppModule`, that serves as the entrypoint to the application.  

Modules can share functionality via the `imports` field in their metadata, declared in the `@NgModule` decorator.  Things like client-side routing, http, forms, and other functionality 'bundles' are made available to components by importing those modules in the module that declares those components.

There **must** be a one-to-one correspondence between a module and a component.  Different modules cannot declare the same component.