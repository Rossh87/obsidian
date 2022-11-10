By convention, router is configured as its own module, `app-routing`.  Routes are set up in an array, and the module re-exports the angular router.  Other modules can then import it and use the `router-outlet` selector to display components associated with the current application URL.

`AppRoutingModule` must be imported in the root component, not lazy-loaded.