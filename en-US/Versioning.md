---
published: true
layout: bookpage
weight: 120
outlevel: 3.2
category: Font Metadata
title: Versioning
---

A version number in a font is useful in (at least) two situations:

- Operating systems can know, based on the version number, when to update a package containing a font.
- If users are having difficulty with a font you have created, they can let you know what version of the font they have, and then you can figure out if the installed version of the font is outdated, or has known problems.

**We recommend using a version number in the form of x.yyy (that is, three places past the decimal point).** For example, use a version number such as `1.500`, not `1.5`. This will help the version number to be correctly understood in a variety of environments.

## What to use for a version number

You _could_ use a version number based on [semantic versioning][Semver] which has a form of `MAJOR.MINOR.PATCH`. However, it is not straightforward how the three parts of semantic versioning map to the two parts of a font version. In this [discussion][Twardoch] Adam Twardoch states he personally uses a font version in the form of M.mpp where

- M is the major version
- m is the minor version
- pp is the patch version

to connect these two concepts. What these values might represent in a given each project is not specified here.

## Setting the version number

Fonts have a version number set in two locations:

- `head` table
- `name` table

FontLab (in the Font Info dialog) and FontForge (go to _Element > Font Info > PS Names_) have fields for both tables. Glyphs has one field for both tables. In UFO sources the information is held in three keys.

| | FontLab | Glyphs | FontForge | UFOv2 |
| --- | --- | --- | --- | --- |
| `head` table | Complete Version record | Version | sfnt Version | versionMajor, versionMinor |
| `name` table | TrueType Version record | Version | Version | openTypeNameVersion |

**We recommend that the version `x.yyy` be the same in both tables, and that the string in the `name` table use the form `Version x.yyy`.**

## Development versions

If the font is an alpha or beta development version, **we recommend that `alpha#` or `beta#` be added to the end of the `name` table string**, as in `Version 5.002 beta2`. This should only be added to the `name` table entry, not the `head` table.  

[Semver]: http://semver.org/

[Twardoch]: https://groups.google.com/d/msg/googlefonts-discuss/w6-i0Opikbc/nlFPEibsCQ8J