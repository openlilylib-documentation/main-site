# openLilyLib

*openLilyLib* is multiple things, but at its core it is an extension
infrastructure for the [GNU LilyPond](https://lilypond.org) notation software.
It is a system to organize functionality for specific tasks in easy-to-use
packages and make it available in consistent ways, encouraging package
developers to provide ready-to-use, includable solutions to common and obscure
notational challenges.

Existing packages support numerous use cases ranging from general separation of
content and layout, conditional page breaking or supporting alternative notation
fonts to highly specific applications like annotating scholarly editions or
supporting notation styles.

However, as a kind of side effect the infrastructure provides many building blocks itself that
can be reused to simplify the development of custom extension functionality. In this sense *openLilyLib* encourages the concept of modularity and reusability in LilyPond programming.

## How It Works

The basic approach to using *openLilylib* involves two steps: loading the main
package `oll-core` and then using the infrastructure. When `oll-core` has been
loaded other packages and modules can be loaded through *openLilyLib's*
interface and used according to the package author's intentions and
documentation.

On the other hand, `oll-core` provides rich functionality (mostly because it is
needed for internal use by the package mechanism) that can be used by user code,
either directly in documents or for building custom project libraries (which
themselves may be wrapped as (private) *openLilyLib* packages). This
functionality includes option handling or logging functions, but also low-level
file/path handling routines or tools to simplify the handling of grobs
(GRaphical OBjects). Details about this can be found in `oll-core`'s
[documentation](../oll-core/index.html).