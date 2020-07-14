# Properties

While the options described on the previous page are a powerful concept in
*openLilyLib* they expose some inherent shortcomings that have always been a
concern since their initial implementation with the original library
infrastructure.

The first issue is a rather vague interface. While it is not possible to get or
set values of options that have not been explicitly registered it *is* possible
to register new options at any point, with barely any limitations to their
naming and positioning in a global options namespace. This makes it “easy” to
produce difficult-to-understand code with option registrations scattered all
over the place.

A more important limitation is that options have no notion of *type*. Any Scheme
value can be stored in an option, and it's the responsibility of a function or
package to deal with arbitrary input, e.g. by rejecting it, erroring out or
falling back to default values. Most packages so far haven't invested that extra
effort, so user code can in many cases pass invalid data into functions, with
completely unpredictable effects.

Both of these shortcomings are fixed by the new (Summer 2020) *property set*
implementation.

The following pages describe the basic use of properties from an *end-user*
perspective. This basically covers two topics: Properties and property sets on
the one hand, property configurations on the other. The full documentation,
especially for making use of the functionality for programming purposes &ndash;
i.e. for package developers or to create custom infrastructures &ndash; is
detailed in the [oll-core](../../oll-core/properties/index.html) documentation.
