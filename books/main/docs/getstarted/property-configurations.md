# Property Configurations

As described on the previous page property values effective in a `with-property-set` function are defined (in order) by

* the property set definition (design time default)
* modified default configuration (`\setProperty`)
* local override (`\with {}` block)

In order to save typing, ensure consistency, and to allow semantic markup values
for it is possible to save subsets of a property set within a *property
configuration*.

## Defining Property Configurations

A property configuration is created with the command

```lilypond
\definePropertyConfiguration <path> <property-alist>
```

`path` is a symbol list that consists of the property set's path with an
appended name. The second argument is an association list with the properties
and their desired values.

```lilypond
\definePropertyConfiguration my-project.tools.arrow.watch
#`((color . ,red)
   (angle . 90)
   (placement . ,UP))
```

This creates a property configuration `watch` for the property set
`my-project.tools.arrow`introduced on the preceding pages, with a few property
overrides. Note that you can only set existing properties to values that pass
the type check.

!!! note

    It is not allowed to use `default` as the name for a property configuration.

Depending on the nature of the function and the property set, your computing and
language background and the use case at hand you may understand property
configurations to be similar to stylesheets in a word processor or DTP app, or
to presets in a synthesizer or audio effect. But essentially it is more like
property overrides in a subclass in a programming language, updating values of a
subset of properties in a property set.

## Using Property Configurations

Once a property configuration has been defined it can be loaded in the
invocation of a `with-property-set` function.

### Shorthand Invocation

It is possible to pass the name of a property configuration as the first
argument of a `with-property-set` function. In this case no further `\with {}`
block may be used to further specify properties. This is a convenient shortcut
if a property configuration is desired but no further configuration is
necessary:

```lilypond
\myArrow watch c'
```

will create an arrow with the current default values and the values from the
`watch` configuration.

### Explicit Invocation

If additional configuration is required a property configuration can also be requested in a `\with {}` block, as follows:

```lilypond
\myArrow \with {
  configuration = watch
}
```

In this case additional properties may be specified along with the property configuration.

!!! note

    It is not possible to mix the two invocations and pass both the name as symbol *and* the `\with {}` block to the function.

### Property Precedence

With property configurations the order of operations is changed. When a configuration is involved the actual value of a property is determined by

* the property set definition (design time default)
* modified default configuration (`\setProperty`)
* **new:** values from the property configuration
* local override (`\with {}` block)

This means that a) any properties *not* specified in the configuration use the
current default values and b) local overrides also override the values from the
property configuration. This is especially useful if some properties have to
respond to the actual engraving situations while others have significance for
the semantic attribution.

## Repeatedly Using a Configuration

Often the same property configuration will be used for multiple consecutive function calls. In this case it is possible to switch the property configuration that is used for a given property set at any time:

```lilypond
\usePropertyConfiguration my-project.tools.arrow.watch
% use  "watch"
\myArrow c'
\myArrow c'
% use current defaults again
\usePropertyConfiguration my-project.tools.arrow.default
\myArrow c'
```
