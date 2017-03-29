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

You _could_ use a version number based on [semantic versioning][Semver] which has a form of `MAJOR.MINOR.PATCH`. However, it is not straightforward how the three parts of semantic versioning map to the two parts of a font version. In this [discussion][Twardoch] Adam Twardoch states he personally uses a font version in the form of _M.mpp_ where

- _M_ is the major version
- _m_ is the minor version
- _pp_ is the patch version

to connect these two concepts. He does not, however, specify what these values might represent in a project. **Developers may choose to use these however they wish, but we've chosen to use a flexible version of this in the form of _M.nnn_ where**

- _M_ is the major version
- _nnn_ is the minor version

The minor version is increased whenever a new version of a font is made available to anyone outside the internal development team. That may be a bug fix version, or a test version, or even a main release. If the new version has significant changes, but not enough to warrant a major version number change, the minor version may jump to a nice round number, say from .172 to .200. 

## Location of the version number and version string

Version information in stored in [two locations within a font][OTSpec]:

- `head` table - two numbers (majorVersion and minorVersion as above)
- `name` table - a longer string that can also contain additional information

The `head` table version numbers may be the only data that operating systems and installation routines use to compare multiple font versions and choose the most recent, so **it is important that if two fonts have differences they should have different `head` table versions**. These values can only be numbers. 

The `name` table version string is text that can contain numbers, letters, and punctuation. **We recommend that this string have three parts, separated by spaces, in the form** `Version M.nnn extrainfo` where

- `Version` is just the word "Version"
- `M.nnn` is the major.minor version number
- `extrainfo` is any additional text that may be useful to the user

This `extrainfo` may be a build number, a test version indicator such as 'beta 3', a date or time stamp, or any other brief bit of information that can help the user know further information about this particular version. **We recommend, however, that developers do not use this additional info as the only indicator that two fonts are different. Only the _M.nnn_ version number should be used to differentiate between versions.** Some operating systems show the `name` table version to users, but may not look at it when comparing font version numbers.

Examples of version information in different styles:

| majorVersion | minorVersion | `name` version string |
| --- | --- | --- |
| 1 | 290 | Version 1.290 alpha1 |
| 1 | 295 | Version 1.295 beta1 |
| 1 | 296 | Version 1.296 beta2 |
| 1 | 300 | Version 1.300 |
| 2 | 101 | Version 2.101 build 693 |
| 3 | 560 | Version 2.560 20170329-1 |
| 6 | 101 | Version 6.101 FW bundle |

## Development versions

**We recommend that development versions and releases should not share the same version numbers**. No two fonts should have the same version number but two different version strings. For example, there should not be two fonts that have version strings `Version 1.234` and `Version 1.234 beta`.

Development versions may have indicators such as _alpha_ or _beta_ in the version string, but that should not be used as the only indicator that two fonts are different. For example, `Version 5.678 beta3` means "This font is version 5.678, and by the way, we're using this version as a third beta test.". It does not mean "We're intending to someday release version 5.678, and this is the third beta leading up to that release."

## How to set the version number and version string

In UFO sources the information is held in three keys in `fontinfo.plist`. FontLab (in the _Font Info_ dialog) and FontForge (go to _Element > Font Info > PS Names_) have fields for both tables.

By default, Glyphs only provides a way to set the Version major and minor numbers (in the _Font Info > Font_ panel). However there is a way to set the version string in that panel:

- Click on the + sign next to _Custom Parameter_
- Under _Property_ choose _versionString_
- Type the version string into the _Value_ field

Here is a summary of where to set version numbers and version strings:

| | FontLab | Glyphs | FontForge | UFOv2 |
| --- | --- | --- | --- | --- |
| `head` table | Complete Version record | Version | sfnt Version | versionMajor, versionMinor |
| `name` table | TrueType Version record | versionString | Version | openTypeNameVersion |


[Semver]: http://semver.org/

[Twardoch]: https://groups.google.com/d/msg/googlefonts-discuss/w6-i0Opikbc/nlFPEibsCQ8J

[OTSpec]: https://www.microsoft.com/en-us/Typography/OpenTypeSpecification.aspx 