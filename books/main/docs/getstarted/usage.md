# General Usage

Loading packages with *openLilyLib* provides more possibilities than shown on
the previous page. These will only be introduced generally on this page, while
all the details of the available functionality is documented with
[oll-core](../oll-core/index.html). The topics covered below include an
introduction to the package/module loading interface and option handling.

## Loading Packages and Modules

### Simple Loading of Packages

As seen on the previous page there is a command to load a package:

```lilypond
\loadPackage edition-engraver
```

This first checks whether the package is already loaded and only if this is not the case loads the package.

Loading a package also silently checks for package dependencies and implicitly loads packages that need to be loaded before. (If a depended-up package is not installed, an error is triggered).

### Simple Loading of Modules

Package may be organized with multiple (also nested) *modules*, which can be loaded explicitly:

```lilypond
\loadModule scholarly.choice
```

Again, it is checked whether the module needs to be loaded. Additionally, if the
package (or any element earlier in the loading path) is not loaded yet, this
will be implicitly loaded. The same holds true for dependencies, just as with
package loading.

### Loading with Options

The loading commands support the passing of package/module options. Of course these options are dependent on what the packages provide, so there can be no general example. Except for one thing which is generally available: Passing to-be-loaded modules as options:

```lilypond
\loadPackage \with {
  modules = choice.annotate
} scholarly
```

which would load the [scholarLY](../scholarly/index.html) package with the
modules `choice` and `annotate`.

## Options

Packages can define configuration options, which can be accessed through the commands `\getOption` and `\setOption`. Options are addressed using a symbol list as path, which typically starts with the package/module name:

```lilypond
\getOption scholarly.annotate.use-colors
\setOption analysis.frames.border-width 0.5
```

There are more commands with different kinds of fallback mechanisms or the
ability to iterate over child options, but these are not covered here.

Also, it is possible to make use of the option handling infrastructure in user
documents, defining options with
`\registerOption path.to.option <default-value>`, which can be a very useful
tool and also “abused” for storing data such as music or titles for reuse.