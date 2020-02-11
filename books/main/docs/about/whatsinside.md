# What's Inside

*openLilyLib* includes a number of packages, most of which serve a specific
notational or editorial purpose, such as [scholarLY](../scholarly/index.html)
(scholarly annotations), [page-layout](../page-layout/index.html)
(self-explaining) or the [edition-engraver](../edition-engraver/index.html), a
tool to separate content from presentation. The following page will give a
commented list of all packages included in the “official” openLilyLib library.
Available package documentation is always accessible through the “Packages”
section in the left-hand navigation column.

Besides these regular packages targeting engraving tasks there are two (three)
special packages, [oll-core](../oll-core/index.html),
[oll-misc](../oll-misc/index.html), and
[snippets](../oll-core/snippets.html).

As the name suggests, `oll-core` is the core of *openLilyLib*, providing the
nuts and bolts plus numerous low-level functions that can be used as building
blocks in programming for LilyPond.

`oll-misc` is a package including numerous small functions, organized by topic
but not serving a dedicated overall goal. `snippets` is its predecessor and
currently in transitional state without a definitive goal, being the origin of
*openLilyLib* but rather poorly structured by the fact that contributors have
added functions to a more or less random directory structure. Probably this
package will eventually be dropped when all included functions have either been
moved elsewhere, included into LilyPond itself, or removed altogether.
