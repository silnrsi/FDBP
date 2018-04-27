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

One special case: **If the supported range is in one of Unicode's supplemental planes (such as [Miao]) then the _Non-Plane 0_ bit (57) should be set, even if the range already has a _ulUnicodeRange_ bit defined**. So in the case of Phoenician, which is in a supplemental plane (10900-1091F) and has a defined bit (58), both that bit and the _Non-Plane 0_ bit (57) should be set.


## 'meta' table

(to be added)


[UnicodeRanges]: https://docs.microsoft.com/en-us/typography/opentype/spec/os2#ur
[PCTYPOLabs18]: https://www.youtube.com/watch?v=eVWWAvhzrq8
[Miao]: https://www.unicode.org/charts/PDF/U16F00.pdf
