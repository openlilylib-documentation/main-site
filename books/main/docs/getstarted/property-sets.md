# Property Sets

A property set manages properties used for a specific purpose. Typically
property sets are defined by package authors and specify either the
configuration properties of a whole *openLilyLib* package or the available
properties (or arguments) for a specific function.

It is also possible (and useful) to work with property sets in custom documents
or project infrastructures. But the necessary work for this is not discussed
here. Please refer to the [oll-core](../../oll-core/properties/index.html)
documentation for details.

## Properties and Property Sets

### Properties in a Property Set

Every property in a property set has a *name*, a *type*, a *default* value, and
(optionally) a description. It is initialized with useful original values and
can only be modified with values that pass the type check.

A typical property set for a function drawing an arrow might look like this:

| Name | Predicate | Default | Description
|---|---|---|---|
| length | `number?` | 3.75 | Length of the line *not including* the arrow-tip length |
| arrow-tip | `tip-style?` | `##t`| ##f, ##t or #'filled |
| line-style | `symbol?` | `#'solid` |
| color | `color?` | `#green` |
| angle | `integer?`| 0 |
| placement | `ly:dir?` | `#UP` | Placement of arrow above, below, or on top of the staff |

### Property Sets vs. Style Sheets

!!! note

    While the example used throughout these pages defines the *apperance* of a
    score element and while this is probably the case for the vast majority of
    use cases, property sets are *not* style sheets. The visual appearance is
    only one possible aspect of property sets. A property *may* address a visual
    quality of an element, but it can equally pass along arbitrary values such
    as (just to name a few) music expressions, export targets, naming schemes
    for output files, algorithmic choices.

### Addressing Property Sets

Property Sets are stored in a central tree structure and are addressed with a
path expressed as a symbol list. Typically this path matches or starts with a
package or module path, but this is purely conventional and not technically
mandated. Typical property sets are:

```lilypond
analysis.frames.frame
scholarly.annotate.export
```

The above custom property set might be stored in a location like

```lilypond
my-project.tools.arrow
```

### Info About a Property Set

It is any package's responsibility to properly document the available properties and their use. But for quick information it is possible to have information on a property set printed to the console output with the following command:

```lilypond
\describePropertySet <property set>
\describePropertySet scholarly.annotate.export
```

!!! todo

    To-be-implemented, see <https://github.com/openlilylib/oll-core/issues/51>

## Property Values

At any point a property set holds valid data for all its properties. Functions
can make use of them as configuration settings (see next page), but it is also
possible to have data (e.g. music expressions) stored in properties and retrieve
them (e.g. when constructing scores).

### Changing Property Values

Initially a property set holds the values defined at design time. This can be
called the “default configuration” of the property set. However, it is possible
to change these values, either as part of the project's customization or to
change appearance/behaviour throughout the document.

Individual properties can be changed with:

```lilypond
\setProperty <property set> <property> <value>
\setProperty my-project.tools.arrow length 5
```

Multiple properties can be changed in one command, e.g. to customize a package's property set:

```lilypond
\setProperties <property set> <property alist>
\setProperties analysis.frames.frame
#`((thickness . 2)
   (color . ,(rgb-color 0 .1 .2))
   (label . "foo"))
```

Since properties are typed a check is performed when trying to change a value.
If the type check fails a warning is issued to the console and the assignment is
skipped:

```lilypond
% fails because 2.5 is not an integer
\setProperty my-project.tools.arrow angle 2.5
```

Changing properties like this changes the default configuration that is used
when a function is called without further customization. The next page discusses
more complex ways for flexibly handling how properties are controlled in actual
use.

!!! attention

    Note that changing a value over time may have unexpected or no effect due to
    the way the actual function is implemented. Plese refer to the corresponding
    explanations for [options](options.md#effect-of-changing-options), which
    behave identically in this respect.

### Retrieving Property Values

Typically property values are used within functions that explicitly support the property set infrastructure. But is also possible to retrieve the current value of a property with:

```lilypond
\getProperty <property set> <property>
\getProperty analysis.frames.frame y-upper
\getProperty my-library.arrow length
```

This can for example be useful when you store music expressions in properties. In this case you could have something like the following score construct:

```lilypond
\score {
  \new Staff \with {
    instrumentName = \getProperty my-project.score.label-melody
  } \new Voice \getProperty my-project.content.melody
}
```
