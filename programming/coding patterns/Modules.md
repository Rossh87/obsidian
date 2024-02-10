## Browser
Setting `type="module"` on a `<script>` element allows the downloaded script to import other files with standard `import` syntax (webpack, TypeScript), with a couple of modifications:
1. the file extension and relative path specifier are required: `import {thing} from 'mod'` will fail; instead, use `import {thing} from './things/thing.js'`
2. files loaded as `type="module"` are deferred automatically

Modules loaded this way will not be available in the global scope.  Even if they export something, the only way to access the export is by explicitly importing the module in another file.  The exception is if the module explicitly attaches something to the global scope.  Don't.

Bundling for the frontend is still a useful tool because it allows us to package code from `node_modules` or wherever else without needing to host and serve 3rd-party packages explicitly.

## Node
Node has supported ES modules since `v14`, thought (I think) it was behind a flag for much of that time.  Use ESM by either using the `.mjs` file extension, or by specifying `package.json` field `"type": "module"`.

Note that in plain node, the file extension **is** required when importing into an ES module, as the extension is needed to determine the module type.

ES modules in Node can seamlessly import commonJS modules: the `exports` object of the commonJS file simply becomes the default import.

Note that commonJS `require` is dynamic code, executed at run-time.  `import` is static and is executed at build/load time.

## Shared
- ES modules are singletons by default