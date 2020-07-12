# Options

*openLilyLib* provides two major tools to manage package and project configuration: Options and Properties. Properties are a newer and potentially more powerful development, but there still are valid use cases for the older option system.

This and the following page only describe the highest-level user-facing
functionality for using options and properties provided by packages, but there
are much more powerful features usable by end-users in documents or project
infrastructures. These are discussed in detail in the documentation of
[oll-core](../../oll-core/index.html).

## Package/Module Options

Most packages and modules define configuration options which are set to
reasonable defaults. Here are a few existing package options with their default
values:

```lilypond
scholarly.annotate.use-colors => ##t
ji.state.fundamental => #(ly:make-pitch 0 0 0)
stylesheets.span.span-colors => #`((default . ,darkmagenta))
```

### Changing Package/Module Options

Options can be set to different values with the command
`\setOption <option-path> <value>`. Setting the value of the `export-targets`
option in `scholarly.annotate` to a different target list would be done with the following statement at any point in a LilyPond document:

```lilypond
\setOption scholarly.annotate.export-targets #'(plaintext latex)
% or
\setOption scholarly.annotate.export-targets plaintext.latex
```

Trying to set an option that hasn't been registered by a package or project
infrastructure will result in a warning.

### Changing Child Options

In some cases it is more convenient to set the value of a *child* option. While
this is mostly used programmatically it can also provide a more convenient
interface to set multiple options at once. For this it is necessary to provide
an association list with the child option names as the keys:

```lilypond
\setChildOptions scholarly.annotate.colors
#`((critical-remark . ,blue)
   (musical-issue . ,green))
```

This iterates over the keys `critical-remark` and sets the corresponding child
options to the respective values.

??? note "Association list syntax"

    Note the syntax used for the association list which uses the backtick and the commas for the color values. This form, also known as *quasiquoting*, is not necessary for the sake of `\setChildOptions` but rather to evaluate the variables `blue` and `green`. If all values are literals it is sufficient to use the regular list syntax

    ```lilypond
    #'((key-one . 1)
       (key-two . "foo"))
    ```

`\setChildOption <parent-path> <child-name> <value>` can be used to change a
single child option:

```lilypond
\setChildOption stylesheets.span.span-colors default #darkgreen
```

!!! warning

    Note that setting child options checks if the *parent* option is registered
    but not the child. This was deliberately chosen to make it possible to store
    the value of keys not originally known. But this “feature” poses the
    inherent risk of unexpected results in case of e.g. misspelled child names.


### Effect of Changing Options

Essentially an option is a variable that will at some point be retrieved,
typically during the execution of a function. Changing an option value will use
that new value when the option is retrieved again. It is important to understand
that depending on the implementation of these functions changing values over the
course of a document may have very different (or no) effects. This should be
documented with the packages that define the options.

#### Evaluation During Parsing

Some options are evaluated in music functions and for example result in a
`\once \override` to be set to the option value. In such cases options may be
changed at any time, even within a music expression, with the change taking
effect immediately.

#### Evaluation in a Callback Function

Some options are used in callback functions. These are functions which are
executed at various points in the engraving stage, when all the music has
already been parsed. An example for this situation is the option
`scholarly.annotate.use-colors` mentioned above.

If this is the case changes throughout the document will not have the expected
effect. Instead *all* instances will use the value of the *last* modification.
To make such options changeable the implementation has to find a way to store
the current value during the parsing stage and retrieve this within the
callback.

#### Evaluation During Instantiation

It is conceivable that the option value is evaluated while the function is
created and stored in a so-called closure, as part of the function definition.
In such a case changing the option would have no effect, and always the default
or maybe a value given as package/module option would be used.

While there may be valid use cases for such behaviour this should usually be
taken as an indicator for issues with the package design and discussed as such.


## Custom Options

Options may not only be used to configure *openLilyLib* packages but also within
custom documents or project infrastructures.

In order to use options they have first to be registered, giving an option path and a default/original value:

```lilypond
\registerOption my-project.settings.use-original-clefs ##t
```

Of course it should be made sure that the option path is unique among all
possible openLilyLib package options.

Current option values can be retrieved through the `\getOption` command:

```lilypond
\getOption my-project.settings.use-original-clefs
% or in Scheme syntax
(getOption '(my-project settings use-original-clefs))
```

There are commands to set and get option values in various forms, but these are
described in detail in the [oll-core](../../oll-core/options/index.html)
documentation.

### Avoid Namespace Pollution

One important use case is storing (configuration) values as *openLilyLib* options instead of simple variables, which can also help avoiding name clashes.

```lilypond
\registerOption my-project.beamColor #red
% is better than
beamColor = #red
% or
#(define beamColor red)
```

### Storing Data in Options

Another, maybe surprising, (ab)use of options is storing data in them, for
example music expressions:

```lilypond
melody = { c' d' e' }
text = lyricmode { One Two Three}

\setOption my-project.melody \melody
\setOption my-project.lyrics \text
```

While not interesting in this simple form this approach can be a foundation for
extremely complex and versatile infrastructures where the content of an edition
is collected from various places.
