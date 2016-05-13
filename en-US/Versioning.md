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

Fonts can have a version number set in two locations:

- head table - must be in the form of `x.y`
- name table - must be in the form `Version x.y` with optional text following.
