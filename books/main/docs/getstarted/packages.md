# Loading Packages and Modules

There are more ways to load packages and modules than the tow listed on the
previous page. These will be introduced and described from an end-user's
perspective on this page, while all the details are documented with the
[oll-core](../oll-core/index.html) package, which also gives guidance for
package authors.

## Loading Packages

### Direct Loading of Packages

As seen on the previous page there is a command to load a package:

```lilypond
\loadPackage edition-engraver
```

This tries to load the [edition-engraver](../../edition-engraver/index.html)
package, if it is not already loaded. If the requested package is not installed
(or the package name is misspelled) a warning is printed to the console, and of
course follow-up errors should be expected. A LilyPond compilation failing with
the error message `unknown escaped string` may be the consequence of trying to
access a command from an *openLilyLib* package that could not be loaded.

### Package Dependencies

Packages can depend on other packages (for example,
[page-layout](../../page-layout/index.html) depends on the
[breaks](../../breaks/index.html) package.) If a package with dependencies is
loaded these are looked up first. Dependency loading is handled just like
explicit loading, so a depended-upon package is not loaded twice, and a missing
dependency triggers a warning with the risk of follow-up errors.

### Loading Packages With Options

*openLilyLib* packages are usually configurable with options and properties (see
the following pages for an introduction). Packages may understand these options
already upon loading and can be set with the following invocation:

```lilypond
\loadPackage \with {
  option1 = value
  option2 = value
} package-name
```

This is something that has to be explicitly implemented in a package[^opts].
To what extent this is available should be explained in the respective
package's documentation.

## Loading Modules

Packages can be organized with multiple (also nested) *modules*, sometimes only
for a better organization of the code, but usually also to make it possible to
only load functionality that is actually needed in a document. In that case
modules have to be loaded explicitly.

### Simple Loading of Modules

Modules can be loaded directly:

```lilypond
\loadModule analysis.harmony.functional
```

This will try to load the `functional` submodule of the `harmony` module of the package `analysis`. Loading is skipped if it is already loaded, and if either `harmony` or `analysis` isn't loaded yet they will implicitly be loaded first. Of course this will also lead to any declared dependencies (not in this case) being loaded too.

### Loading Modules With Options

Like packages modules may support options to be set at loading time:

```lilypond
\loadModule \with {
  use-colors = ##f
} scholarly.annotate
```

### Loading Modules as Package Options

If a package includes many modules (such as e.g.
[oll-misc](../../oll-misc/index.html) does) it may be cumbersome to load each
desired module individually. Therefore `\loadPackage` can be used to load
multiple modules at once. This is achieved by passing a symbol-list with module
names the the package option `modules`:

```lilypond
\loadPackage \with {
  modules = choice.annotate
} scholarly
```

This will load the [scholarLY](../scholarly/index.html) package with the two
modules `choice` and `annotate`. Note that while this is convenient in many
cases there are two caveats:

1. Modules loaded this way can *not* be passed any load-time options. Usually
   this should not be a problem as options can be set afterwards, but it has to
   be considered what is more appropriate for a given document or project.
2. Each entry in the symbol-list is considered an independent module, therefore
   this syntax doesn't support loading submodules (which are referenced by
   symblo-lists themselves)


## Package Metadata

*openLilyLib* packages are to some extent documented by a set of metadata stored
in the file `package.cnf` in the package's root directory. This includes a
description of the purpose, references to a repository, maintainers, version
information and other items. For debugging purposes it's not only possible to
directly locate and open this file but to insert the command
`\describePackage <package-name>` somewhere in a document after loading the
package. For the [page-layout](../../page-layout/index.html) package this
produces the following output in the terminal:


```

openLilyLib: Metadata of package 'page-layout':
=====
((repository
   .
   "https://github.com/openlilylib/page-layout.git")
  (website
   .
   "https://github.com/openlilylib/page-layout")
  (license . "GPL3")
  (version . "0.0.1")
  (maintainers "Urs Liska <ul@openlilylib.org>")
  (oll-core . "0.5.0")
  (dependencies "edition-engraver" "breaks")
  (description
   .
   "The page-layout package provides tools to easily define and apply
sets of line breaks.")
  (short-description
   .
   "Managing page layout in LilyPond scores")
  (display-name . "Page Layout")
  (name . "page-layout"))
```

[^opts]:

    The package has to take care that options are first registered, then updated
    with values passed during package loading before being processe further.
