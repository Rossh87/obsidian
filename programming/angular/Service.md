Services are for encapsulating data and related logic, and sharing that data with 1 or more view components.  They enforce separation of concerns between logic and presentation.

A service is just a class decorated with the `@Injectable` decorator.  For the service to be available for injection into a component, it must be registered with a provider.  By default, `ng cli` generates services that are registered to the `root` provider.  Services in the `root` provider are available for injection into any class that has the lookup token.  `root` is the correct place to register an injectable unless you want to limit consumption of the service to importers of a particular `ngModule`.  No specific import/provider declarations are needed for services provided by `root`.

If a service is to be provided by a non-root module, it is best to to declare this relationship in the **service** definition (via `@Injectable` metadata) rather than the **module** definition (via `@ngModule` metadata).  This enables tree-shaking if no other class actually consumes the injected service.

It's important to remember that by default an injected service is a singleton: every consumer is accessing the data.