# Package Development

The most likely area of work you will find yourself in when contributing to
*openLilyLib* is development on individual packages. However, it is generally
useful to familiarize yourself with the documentation of
[oll-core](../oll-core/index.html), *openLilyLib*'s internal framework, as
nearly every package does depend on it &ndash; not only for basic package
infrastructure support but also by reusing its building blocks.

## Working on Existing Packages

### Fixing Things

The most immediate way to get involved in package development is fixing bugs or
enhancing existing features. If you intend doing any of this it is useful to get
in touch with the package maintainers, typically through the package's Github
issue tracker, which is listed on the package's overview page on this website.

Please try to adhere to the existing coding standard you encounter in the
package. If this seems to deviate substantially from the overall coding style in
*openLilyLib* you are invited to *gently* and *politely* encouraging the package
maintainer to move into the common direction. Guidance on this is given in
`oll-core`'s documentation.

### Adding Modules / Functionality

Modularity is built into *openLilyLib*'s design, and many packages are organized
in dedicated *modules*. If you find yourself using a package heavily but think
it could use substantial enhancements in functionality it may be a case for
adding a new module to the package.

It is wise to get in touch with the maintainers *in advance* to discuss such
ideas in order to avoid misunderstandings and disagreement. In any case you
should have familiarized yourself with the tools and building blocks `oll-core`
provides regarding the package infrastructure.

## Creating New Packages

The [Github organization](https://github.com/openlilylib) is the central
location and development platform for the “official” *openLilyLib* packages,
but it is by no means the only place to make use of the extension
infrastructure.

### Local Use and Packages

An *openLilyLib* package is simply a directory of Lilypond code working against
a given API, and anybody having installed *openLilyLib* can immediately wrap
some code as an *openLilyLib* package. It can be very useful to simply *use*
*openLilyLib*'s building blocks in custom project infrastructures, but it may
also be useful to wrap recurring functionality of your projects in a custom
*openLilyLib* package.

### Independent *openlilylib* Packages

In addition everybody is free to release *openLilyLib* package in other places,
provided it is under a license that is compatible to *openLilyLib*'s use of the
GPL. However, when you do so it is your own responsibility to keep your package
in sync with *openlilylib*'s potentially changing interface.

### New Package Contributions

If you have an idea for functionality that would lend itself to being wrapped as
an *openLilyLib* package, or if that holds true for existing library code you
might get in touch with us and suggest a package. The best place for such prior
discussion would be the `lilypond-user` mailing list.
