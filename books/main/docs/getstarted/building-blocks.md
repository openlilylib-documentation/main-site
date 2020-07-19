# Modularity

The other chapters of the “Get Started” section of this website were targeted at
*openLilyLib* end-users, giving an introduction to some common concepts likely to
be found in any *openLilyLib* package.

However, providing turnkey solutions through packages targeted at specific use
cases is only one part of the story. The other, equally important aspect of
*openLilyLib*'s idea is encouraging modularity and reusability in programming
for and with LilyPond. This can be achieved by combining functionality provided
by packages, and by reusing the building blocks at the foundation of `oll-core`.

The following paragraphs are not meant as actual documentation but as an
encouragment to explore the hidden potentials of *openLilyLib*.

## Reusing Package functionality

Many *openLilyLib* packages provide very specific functionality while others
focus on somewhat more generic aspects. It can be very efficient to create
packages that don't serve a specific end-user focused purpose but rather provide
core functionality from which more complex actual functionality can be composed.
The availability of ready-to-use solutions to lower-level programming tasks can
make it substantially more efficient to think about higher-level solutions for
real-world challenges.

The main *openLilyLib* packages provide an example for this situation. The
support package [breaks](../../breaks/index.html) implements data structures and
low-level handlers for managing multiple sets of line and page breaks.
[edition-engraver](../../edition-engraver/index.html) makes it possible to
inject elements and rendering hints into scores from external locations. Two
other packages, [page-layout](../../page-layout/index.html) and
[partial-compilation](../../partial-compilation/index.html), make use of these
supportive packages to realize their respective goals of an easy access to
alternative page breaks and selective compilation. Both would have been much
more complicated to develop (and would have produced redundant or inconsistent
code) if they couldn't build upon the underlying common code base of the support
packages.

## Reusing *oll-core*'s Building Blocks

The common *openLilyLib* functionality described in the previous sections
requires a substantial code base of underlying functionality. Also, the
interface described on these pages is not only useful when working with existing
packages but can be a very efficient base for programming one's own custom
infrastructures with LilyPond and *openLilyLib*. Option and property handling
are two more obvious areas that can be used in custom user libraries, but there
are many more functions buried in the internals of the
[oll-core](../../oll-core/index.html) package.

We encourage any ambitious user of LilyPond and *openLilyLib* to dive into
*oll-core*'s documentation to find out about its hidden treasures.
