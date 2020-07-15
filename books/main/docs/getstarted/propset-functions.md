# Function with Property Sets

Property sets are typically used by functions that have been created with the
`with-property-set` macro.[^func-author] These functions have access to the “current“ value of
each property. This page and the following describes what “current” means in
this context and how it can be handled in user code.

## A `with-property-set` Function

Consider a function `\myArrow` that has been created with the property set
`my-project.tools.arrow` shown on the previous page. It may take a note as an
argument and print an arrow above or below it.

When called in the simplest form:

```lilypond
{
  \myArrow c'
}
```

it will use the default properties and print a solid green arrow above the
staff, with a length of 3.75 staff spaces and a non-filled tip.

## Changing the Default Configuration

If the default configuration is changed at some point with e.g.

```lilypond
\setProperties my-project.tools.arrow
#`((color ,red)
   (line-style . dashed))
```

subsequent simple function calls will use these changed properties along with
the remaining ones in their original state.

## Calling a Function with Local Overrides

Any `with-property-set` function provides an optional argument that accepts a
`\with {}` block where properties can be overridden locally for the specific
instance:

```lilypond
{
  \myFunction \with {
    line-style = dotted
    angle = 32
  } c'
}
```

This will use the original values for the length, arrow-tip, and placement
properties, the color changed in `\setProperties` before, and the line-style and
angle passed directly into the function.

While this makes it possible to have very fine-grained control over all settings
of a function, especially for properties that may have to be adjusted to the
actual engraving situation (the line length of this arrow may be a good example)
there may be the need for having multiple configurations to indicating related
cases, for example by a common color or line-style.

It wouldn't be maintainable and scalable to individually configure every single
instance manually, and therefore we have complex possibilities in the powerful
“property configurations“ described on the next page.

[^func-author]:

    This is written with the end-user in mind. For this you can assume someone
    else, typically a package author, has written a `with-property-set`
    function. Documentation on how to *write* such functions is within the
    [oll-core](../../oll-core/index.html) documentation.
