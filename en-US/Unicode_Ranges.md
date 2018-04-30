---
published: false
layout: bookpage
weight: 190
outlevel: 3.6
category: Font Metadata
title: Unicode Ranges
---

There are two means within an OpenType font to indicate which scripts and Unicode ranges a font supports: the OpenType _ulUnicodeRange_ bit in the 'OS/2' table and the newer 'meta' table.

## ulUnicodeRange

The [OpenType OS/2 table specification][UnicodeRanges] lists the ranges defined by _ulUnicodeRange_ and which bits must be set to indicate support for that range. Most font editors provide a user interface that lists the ranges and allows you turn ranges on and off, so hacking bit fields is rarely necessary.

According to [Peter Constable][PCTYPOLabs18] the _ulUnicodeRange_ field is rarely used anymore by OSes to determine font script coverage. One major reason is that the field has run out of space, and no new ranges can be added. However there are older systems that still look at this info, so **the _ulUnicodeRange_ bits should be set if the font is intended to support any of the ranges defined in the [spec][UnicodeRanges]**.

One special case: **If the font includes any supplemental plane characters, then the _Non-Plane 0_ bit (57) should be set. This is true whether or not the character is in a range that has a _ulUnicodeRange_ bit defined**. So in the case of Phoenician, which is in a supplemental plane (10900-1091F) and has a defined bit (58), both that bit and the _Non-Plane 0_ bit (57) should be set.


## 'meta' table

Because of the above-mentioned limitations of the existing _ulUnicodeRange_ field, the [meta table][MetaTable] was added to the OpenType specification (starting with version 1.8 in 2016). **OpenType fonts should include the 'meta' table describing the languages and scripts for which the font was designed as well as the languages and scripts that the font is capable of supporting.**


[UnicodeRanges]: https://docs.microsoft.com/en-us/typography/opentype/spec/os2#ur
[MetaTable]: https://docs.microsoft.com/en-us/typography/opentype/spec/meta
[PCTYPOLabs18]: https://www.youtube.com/watch?v=eVWWAvhzrq8
[Miao]: https://www.unicode.org/charts/PDF/U16F00.pdf
