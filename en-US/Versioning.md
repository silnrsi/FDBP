---
published: true
layout: bookpage
weight: 120
category: Font Metadata
title: Versioning
---

A version number in a font is useful in (at least) two situations:

- Operating systems can know, based on the version number, when to update a package containing a font.
- If users are having difficulty with a font you have created, they can let you know what version of the font they have, and then you can figure out if the installed version of the font is outdated, or has known problems.

We recommend using a version number in the form of x.yyy (that is, three places past the decimal point). For example, use a version number such as `1.500`, not `1.5`. This will help the version number to be correctly understood in a variety of environments.

## Additional details

If you want to use a version number based on [semantic versioning](http://semver.org/) which has a form of `MAJOR.MINOR.PATCH` it is not straightforward how the three parts of semantic versioning map to the two parts of a font version. [Adam Twardoch][Twardoch] personally uses a font version in the form of M.mpp where

- M is the major version
- m is the minor version
- pp is the patch version

to connect these two concepts.
What these values mean to each project is not specified here.

Fonts have a version number set in two locations:

- `head` table - must be in the form of `x.yyy`
- `name` table - must be in the form `Version x.yyy` with optional text following.

We suggest that the version `x.yyy` be the same in both tables.

[Twardoch]: https://groups.google.com/forum/#!searchin/googlefonts-discuss/versioning/googlefonts-discuss/w6-i0Opikbc/Dj_tNw8epYUJ
