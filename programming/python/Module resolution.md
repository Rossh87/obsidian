All of the 'import machinery' is directly exposed as normal Python modules/functions, e.g. `importlib` package, or the builtin `__import__()`. Usually we interact with the module system via the `import` statement. This statement:
1. Searches for the module by name
2. Creates a module object for the search result (if it is found), and
3. Binds the search result to an identifier in the local scope 

There is only 1 type of module object in Python, regardless of language (C, Python, etc.).

Modules and packages can be thought of as files and directories as an analogy, but in reality modules and packages can originate from places that are not filesystems. E.g. a module can be created directly in Python without any file representation. A package is a special kind of module: any module with a `__path__` attribute is considered a package.

The search for modules begins with `sys.path`, a list of strings (MUST be only strings) that specifies the search path(s) for modules. `sys.path` is a combination of the environment variable `PYTHONPATH` and an installation-dependent (OS installation? Python installation?) default. This is similar to Unix `$PATH`. When the Python interpreter is invoked, a potentially unsafe string is appended to `sys.modules`; depending on the invocation, the appended string changes:
1. `python -m module`: prepend the current working directory
2. `python script.py`: prepend the script directory (resolving if script is a symlink)
3. `python -c code` or REPL commands: prepend an empty string, which is the same as current working directory.

## Regular packages
A 'regular' package is generally any directory that contains an `__init__.py` file. The contents of the `init` file are executed the first time the package is imported. Packages defined this way can include subpackages that have their own `init` file. IMPORTANT: when a subpackage is imported, `init` files for its parent packages are also executed.

## Namespace packages
A namespace package is made up of various portions (a set of files in a single directory), where each portion contributes a subpackage to the parent package. A portion may live any number of places, e.g. on a network, in a zip file, etc. This allows code that is split across multiple directories (not necessarily subdirectories of the parent package) to be treated as part of a single package. This is useful if, e.g., multiple teams are responsible for different subpackages of the same package.

