# Cascading and Filtering Property Configurations

*openLilYLib's* property configurations behave similarly to Cascading Style
Sheets for HTML. They override a subset of a parent property set, and it is
possible to create sophisticated structures to model individual but related
behaviour between similar elements. This is achieved through inheritance.

## Cascading Property Configurations

If the definition of a property configuration contains a `parent` item the configuration inherits from the referenced configuration. For example there could be a secondary “watch” element with a filled arrow-head but otherwise identical appearance which could be defined like this:[^qq]

```lilypond
\definePropertyConfiguration my-project.tools.arrow.watch-urgent
#'((parent . watch)
   (arrow-tip . filled))
```

Parents can cascade to grand- or grand-grand-parents (as long as the parent has a `parent` reference), making complex and sophisticated structures possible.

## Filtering By Property Configurations

One of the more interesting features of property sets is support for filtering,
or selectively activating by property set. There are some overlaps with
LilyPond's own
[tag](http://lilypond.org/doc/v2.19/Documentation/notation/different-editions-from-one-source#using-tags)
concept, [choices](../../analysis/index.html) from the *scholarLY* package, or
[editions](../../edition-engraver/index.html) in *edition-engraver*. It is
important that you understand the specifics of all these tools to find the best
choice for your usd case.

In a nutshell, *oll-core*'s property configuration filtering makes it possible
to activate a function only if a property configuration is used, or to include
and exclude lists of configurations.

!!! attention

    It is important to understand that this mechanism doesn't actually *do*
    anything beyond providing the *information* to the function. It is
    completely up to the function implementation, how, or if it responds to that
    information. Functions can for example conditionally highlight score
    elements, hide or completely omit them, or act in arbitrary ways on the
    information. And of course they can simply ignore it.

    Please refer to the documentation of the packages/functions to learn about
    their filtering-related behaviour.

There are three filters that can be set for each property configuration, which interact: `require-configuration`, `use-only-configurations`, and `ignore-configurations`. They are set with the command

```lilypond
\setPropertyConfFilters <property set> <filter> (<configuration list>)
```

### Requiring *Any* Property Configuration

By default functions with or without a property configuration are considered
active. It is possible to change the `require-configuration` filter to `##t` to
consider all function calls as inactive that have not selected a configuration:

```lilypond
\setPresetFilters my-project.tools.arrow require-configuration ##t
```

### Using only Selected Configurations

With the `use-only-configurations` it is possible to set active only functions
whose configuration is present in the filter's list. This filter doesn't reject
functions *without* any configuration in order not to require the user to assign
configurations to *all* function calls. However, the filter interacts with the
`require-configuration` filter and can that way suppress *all* function calls
without the listed configurations.

```lilypond
\setPresetFilters my-project.tools.arrow use-only-configurations watch.foo
```

### Ignoring Selected Configurations

The filter `ignore-configurations` accepts a list of configurations that are ignored/suppressed. Function calls without a configuration are not affected by this filter:

```lilypond
\setPresetFilters my-project.tools.arrow ignore-configurations watch.foo
```

!!! attention

    Note that because each of these filters removes configurations from the list
    it is easily possible to end up with a constellation where *no* function
    calls are considered active anymore.

### Filtering Globally vs. By Property Set

The examples above filter instances of a given property set. However, with the
fake goal of addressing `OLL.global` it is possible to filter all property
configurations by their name, regardless of the property set they affect.

This is a powerful tool when preparing scores for live update, and multiple different functions are to be displayed/hidden in common scenarios, e.g. with property configuration names like `stageOne`, `stageTwo`, `result` or similar sequences.

Note that the options outline on this and the previous pages provide a powerful
but complex web of possibiliites which you have to carefully choose and evaluate
to successfully apply.

[^qq]:

    Note that this definition doesn't need properties to be evaluated, therefore it is not necessary to use that quasiquote (backtick) syntax for the association list.
