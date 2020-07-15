# Property Configurations

As described on the previous page property values effective in a `with-property-set` function are defined (in order) by

* the property set definition (design time default)
* modified default configuration (`\setProperty`)
* local override (`\with {}` block)

In order to save typing, ensure consistency, and to allow semantic markup values
for subsets of a property set can be saved nd set with a *property
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
`my-project.tools.arrow`introduced in the preceding pages with a few property
overrides. Note that you can only set existing properties to values that pass
the type check.

!!! note

    It is not allowed to use `default` as the name for a property configuration

Depending on the nature of the function and the property set, your computing and
language background and the use case at hand you may understand property
configurations to be similar to stylesheets in a word processor or DTP app, or
to presets in a synthesizer or audio effect. But essentially it is more property
overrides in a subclass in a programming language, setting values to a subset of
properties in a property set.

## Using Property Configurations

Once a property configuration has been defined it can be loaded in the
invocation of a `with-property-set` function.

### Invocation

```lilypond
\myArrow \with {
  configuration = watch
}
```

will create an arrow with the current default values and the values from the
`watch` configuration.

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

!!! todo

    Not implemented yet: <https://github.com/openlilylib/oll-core/issues/53>