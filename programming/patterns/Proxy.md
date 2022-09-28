Essentially, proxying is a less-coupled form of composition/decorating/whatever else we want to call it.  Proxy methods intercept calls to their target, redirecting, changing, or adding effects to the original argument.

ES6 `Proxy` is maybe not good for performance-intensive applications.

Potential use-cases:
- two-way data binding
- logging
- deprecating APIs that are transitioning to breaking changes (proxy calls to old methods to the appropriate method(s) of the new API, and log a deprecation message, e.g.)
- caching
- preserving object identity (the proxy identity) while swapping underlying data