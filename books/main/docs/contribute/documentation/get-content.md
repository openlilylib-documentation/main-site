# Setting Up the Content

Documentation for *openLilyLib* is maintained in a number of Git repositories in
the [openlilylib-documentation](https://github.com/openlilylib-documentation)
GitHub organization. The main overview site (which you are reading right now) is
the main repository
[main-site](https://github.com/openlilylib-documentation/main-site) while all
packages are documented in separate repositories integrated as
[Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules).

## Root Directory

All repositories are to be installed within one arbitrary root directory on your computer. In this documentation we assume this to exist and be named

```
$HOME/git/oll-documentation
```

We also assume that you have set up your GitHub account to use SSH authentication.

## Cloning the Contents

Different from working with regular Git repositories this requires you to take some extra steps when cloning the documentation sources. The initial task is to clone the shell repositoy `main-site` and go into that.
```
$ cd HOME/git/oll-documentation
$ git clone git@github.com:openlilylib-documentation/main-site.git
§ cd main-site
```

At last you should have a look into what has been actually downloaded:

```
$ ls -la
insgesamt 32
drwxr-xr-x  5 uliska uliska 4096 Aug 20 04:53 .
drwxr-xr-x  3 uliska uliska 4096 Aug 20 04:53 ..
drwxr-xr-x 17 uliska uliska 4096 Aug 20 04:53 books
drwxr-xr-x  2 uliska uliska 4096 Aug 20 04:53 _config
drwxr-xr-x  8 uliska uliska 4096 Aug 20 04:53 .git
-rw-r--r--  1 uliska uliska   18 Aug 20 04:53 .gitignore
-rw-r--r--  1 uliska uliska 1657 Aug 20 04:53 .gitmodules
-rw-r--r--  1 uliska uliska  209 Aug 20 04:53 README.md
```

`books` contains *empty* directories for all the currently available package documentations, while `_config` contains the configuration files for `Mkdocs-library`, our custum build tool.

```
$ ls books
analysis  bezier  breaks  edition-engraver  gridly  ji  lalily-templates  main  notation-fonts  oll-core  oll-misc  page-layout  partial-compilation  scholarly  snippets
$ ls _config/
config.yml  defaults.yml  template.yml
```

`.git` and `.gitignore` are the typical files indicating that we have a Git repository before us, and the `.gitmodules indicates that the repository includes submodules. In order to initially fetch the actual content of the submodules we need to issue two more commands from the `main-site` directory:

```
$ git submodule init
$ git submodule update
```

Now you can see that the subdirectories below `books` have also been populated
with content, typically with `_config` and `docs` directories and a `README.MD`
file (and the hidden Git stuff):

```
$ ls -la books/analysis/
insgesamt 28
drwxr-xr-x  4 uliska uliska 4096 Aug 20 05:07 .
drwxr-xr-x 17 uliska uliska 4096 Aug 20 04:53 ..
drwxr-xr-x  2 uliska uliska 4096 Aug 20 05:07 _config
drwxr-xr-x  2 uliska uliska 4096 Aug 20 05:07 docs
-rw-r--r--  1 uliska uliska   42 Aug 20 05:07 .git
-rw-r--r--  1 uliska uliska   16 Aug 20 05:07 .gitignore
-rw-r--r--  1 uliska uliska   62 Aug 20 05:07 README.md
```

### Git Submodule Remarks

This process is a bit more complicated than what you may typically encounter in
tutorials or real-world projects. The reason is that the partial books are used
by *Git* as submodules, but our build structure expects them to be directories
*beside* the main book's directory `main-site/main`. In other words: the main
site is technically a sub-book and Git submodule as well. So please don't be
confused by seemingly conflicting information elsewhere but simply follow the
direction on this page-
