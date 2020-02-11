# Quick Start

Any LilyPond document wanting to make use of *openLilyLib* first has to load
[oll-core](../oll-core/index.html) with the invocation

```lilypond
\include "oll-core/package.ily"
```

After this various commands for loading packages and submodules are available.
They will be explained on the following pages, but for a starter this will load
the [stylesheets](../stylesheets/index.html) package and the `annotate` module
from the [scholarLY](../scholarly/index.html) package:

```lilypond
\include "oll-core/package.ily"
\loadPackage stylesheets
\loadModule scholarly.annotate
```