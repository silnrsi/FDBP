---
published: true
layout: bookpage
weight: 230
outlevel: 4.3
category: Glyph Metadata
title: Glyph Naming
---
## Summary of Recommendations
**We recommend that glyph names (also called psnames or PostScript® names) be included in released (that is, shipping) fonts.**

**Developers may choose to manage two sets of glyph names: *working* glyph names ("friendly" names used during development) and *production* glyph names (used in the shipping font).**

**Per the [Adobe Glyph List Specification \[AGL\]][AGL] specification, glyph names, whether working names or production names, should be no longer than 31 characters, must be entirely composed of characters from the following set: A–Z, a–z, 0–9, . (period, U+002E FULL STOP) and _ (underscore, U+005F LOW LINE), and must not start with a digit.** Note however that 
- Adobe Font Development Kit \[AFDKO\] [Feature File Specification][FEA] allows name length up to 63 but requires that names, with the exception of `.notdef`, must not start with a digit or a period. 
- [ISO/IEC 14496-22 "Open Font Format"][OFF] recommends that names, with the exception of `.notdef` and `.null`, must start with a letter. This is not a strict requirement. For example, it is common for glyphs that are only used as components of composite glyphs to have names that start with an underscore, as in `_dot`.
- Various font tools may have other restrictions but such are not derived from any official font specifications.

**For glyphs that can end up in the final output of rendered text, the production glyph names should be selected from the [Adobe Glyph List for New Fonts \[AGLFN\]][AGLFN].**

## Introduction
For various reasons (historical, technical, convenience) most font development tools and formats provide mechanisms to name glyphs with human-readable strings (as opposed to just index numbers, for example). This section documents conventions, restrictions, and best practices for glyph naming.

## Why even have glyph names?
Given the ubiquitous support for TrueType/OpenType fonts, one might ask why do we even have glyph names? Nothing _inside_ an OpenType font requires glyphs to have names &mdash; complex layout tables `GSUB` and `GPOS`, for example, do all their work in terms of glyph indexes. Even for the `post` table itself (where glyph names are stored), one of the allowed forms, called Verson 3, is one that has no names. So one might reasonably ask: if functional fonts can be produced without glyph names, why have them at all?

The answer starts in the era before TrueType came along, in which Adobe's sophisticated page layout engine accessed glyphs by their names &mdash; glyphs had no other way to be located other than by their name. In fact, glyph names were simply another identifier in the PostScript programming language &mdash; and that is why even today glyph names have a very strict allowed form.

Going even further, some software packages are able to infer certain properties of a glyph from just its name. The most commonly cited case of this is that some PDF files do not include any representation of the _character_ stream that the document represents, but yet you can still copy _characters_ from the document to the clipboard. The reason this works at all &mdash; and it doesn't always work perfectly &mdash; is that Acrobat is able to deduce the character stream (or something close to it) by looking only at the names of the glyphs in the file.

All of this can work, however, only if the glyphs have been correctly named &mdash; meaning named according to Adobe standards. It is for exactly these reasons that we give the recommendations at the top of this article.

## Working names vs production names
The first thing to recognize is that, as we'll see in a minute, the glyph names that should be in a font when it is shipped (i.e. released) are not necessarily the most friendly and memorable names. Therefore many developers use a different set of glyph names for development purposes and, as a last step of production, change the glyph names to the "official" names. We will call these two sets of glyph names the **working names** and the **production names**, respectively.

As an example, the acceptable *production name* for a glyph representing U+0628 ARABIC LETTER BEH would be one of:

- `uni0628`
- `u0628`
- `afii57416`

However, as none of these is particularly memorable, designers might, for example, choose a *working name* of `beh`.

The use of working and production glyph names is common enough that at least one modern font format (the UFO format) provides a mechanism to manage both glyph names, and some font editing applications (GlyphsApp) automatically convert names from working to production during export.

### Not all glyphs need production names
Note that even in a shipping font, there may be glyphs that do not need production names. Any glyphs used _only_ as components of some other [composite] glyph need not have production names because the component glyphs can never end up in the output glyph stream of rendered text.

For example, many letters in the Arabic script are distinguished from each other only by the pattern of dots drawn above or below the main shape. A font might use component glyphs for each pattern of dots (one dot below, one dot above, two dots below, etc.) and also for each main shape, and then construct the desired glyph repertoire using composites that reference the appropriate base and dot glyphs. The glyphs for various patterns of dots can never appear in the output stream, so they do not need production names.

## Glyph names are also known as PostScript names

As an early industry leader with its PostScript technologies, Adobe has set &mdash; and now maintains &mdash; the standard for how glyphs are named, both in terms of what constitutes a valid name and, within that framework, what specific names are recommended. Within an OpenType font, glyph names are stored in the [`post`] table.

Because of this, glyph names are often referred to as *PostScript names* or sometimes, more simply, *psnames*.

Note that it doesn't matter whether one is talking about working names or production names, they are still considered *PostScript names* and their construction should abide by the relevant Adobe standard.

**Next:** the [Adobe Glyph List](Adobe_Glyph_List.html) standard

[`post`]: https://www.microsoft.com/typography/otspec/post.htm
[AGL]: https://github.com/adobe-type-tools/agl-specification
[AGLFN]: https://github.com/adobe-type-tools/agl-aglfn
[OFF]: http://standards.iso.org/ittf/PubliclyAvailableStandards/c066391_ISO_IEC_14496-22_2015.zip
[FEA]: https://cdn.rawgit.com/adobe-type-tools/afdko/master/FDK/Technical%20Documentation/OpenTypeFeatureFileSpecification.html#2.f.i