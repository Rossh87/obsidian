Currently, `all`,  `screen`, and `print` are the only level-3 media types that are not deprecated.  Note that the media type in a query is optional. If none is specified, `all` is the default.

Queries permit basic logic:
- logical `and` for media rules is available with keyword `and`
- logical `or` is available with commas
- logical `not` is available by prefixing the rule with keyword `not`

There is a [long list](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#syntax) of media features with varying levels of browser support.  Media features are rules that match some state of the user-agent, device, or environment.  They can be used to adjust for user preferences as well as device characteristics, e.g. `prefers-color-scheme`, which detects a user-specified preference for a light or dark scheme, set in the operating system or the browser.