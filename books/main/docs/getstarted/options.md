# Options

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
