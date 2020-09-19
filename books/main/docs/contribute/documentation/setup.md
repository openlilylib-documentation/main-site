# Setting Up the Environment

Authoring documentation for the *openLilyLib* website requires a number of
tools, but the setup should be fairly straightforward and require not too many
steps, which are described below. The toolchain allows various variations, and
if you know what you're doing you are free to deviate from the instructions.
However, it seems reasonable to describe a single process and support only this
one.

!!! note

    The procedures have so far only been tested on Linux, but should work easily
    on the other operating systems.

    We would be glad about anybody checking out installation on MacOS and
    Windows and sharing their results for this contributor's guide.

## Terminal and Editor

Most of the work generating the website is done in the terminal, so you should
be at least generally familiar with working in the terminal.

Contents are edited in plain text files, so all you *need* is an arbitrary text
editor. Please note that in a *word processor* application you have to actively
make sure files are saved in plain text, rather than arbitrary document formats.
However, we recommend using a decent text editor with strong Markdown support.
There are good free Markdown editors on the market, and it should also be a good
idea to use a programmer's editor or a full-fledged *IDE* (Integrated
Development Environment).

## Tools

### Git

Documentation is managed with the [Git](https://git-scm.com/) version control
software and hosted in a
[Github organization](https://github.com/openlilylib-documentation/). Git can be
installed from the distribution's package sources on Linux and downloaded from
the website on Mac and Windows.

Installation and first configuration is explained in a recommended
[tutorial](https://help.github.com/en/github/getting-started-with-github/set-up-git)
on Github. At the very least it is required to configure your name and email
address. Configuring the `core.editor` variable is probably a good idea too
because chances are you're not familiar with the `vim` editor that is opened in
the terminal by default. Note that there *is* some sense using an editor in the
terminal (`nano` is less irritating for novice terminal users) instead of always
have a separate window opening for each commit.

Having an account on Github is required to contribute to openLilyLib and its
documentation. We recommend to connect to GitHub with SSH (rather than HTTPS).
Please check out the information on GitHub's
[help pages](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh).

### Python 3

The tooling is done in [Python 3](https://www.python.org/), which is installed
by default on Linux and can be obtained from the home page linked above for the
other operating systems.

!!! note

    Currently the minimum requirement for Python is version 3.7

### pip3

All Python dependenies required for the toolchain are managed by
[pip3](https://pip.pypa.io/en/stable/). Depending on your system it may be
called *pip3* or *pip*, so in case of doubt please check with both names.

Probably pip3 has already been installed along with Python. You can check this
by issuing one out of

```shell
pip3 --version
pip --version
```

in a terminal. If this prints some version information you're good to go,
otherwise you have to install the tool manually. On Linux you can do that with
the package manager, the package is typically called `python3-pip`. Otherwise
you can download the script [get-pip.py](https://bootstrap.pypa.io/get-pip.py),
change to the download directory in a terminal and install pip with
`python3 get-pip.py`.

### MkDocs

Documentation is compiled with the [MkDocs](https://www.mkdocs.org/) static site
generator with a number of separate tools and plugins.

All the dependencies are wrapped within one custom plugin and can be installed
in one step.

!!! todo

    Prepare that plugin and then document it

### (LilyPond)

**TODO:** LilyPond is not used yet to produce music examples

### (Pandoc/LaTeX)

**TODO:** Pandoc and LaTeX may at one point be used to also produce
documentation in other formats, especially PDF.
