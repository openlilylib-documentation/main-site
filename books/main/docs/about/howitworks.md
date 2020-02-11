# How It Works

The basic approach to using *openLilylib* involves two steps, loading `oll-core`
and then either using packages or programmatically working with the provided
functionality (for examples see the [Getting Started](../getstarted/get.md)
section).

When `oll-core` has been loaded other packages and modules can be loaded through
*openLilyLib's* interface and used according to the package author's intentions
and documentation.

On the other hand, `oll-core` provides rich functionality (mostly because it is
needed for internal use by the package mechanism) that can be used by user code,
either directly in documents or for building custom project libraries (which
themselves may be wrapped as (private) *openLilyLib* packages). This
functionality includes option handling or logging functions, but also low-level
file/path handling routines or tools to simplify the handling of grobs
(GRaphical OBjects). Details about this can be found in `oll-core`'s
[documentation](../oll-core/index.html).