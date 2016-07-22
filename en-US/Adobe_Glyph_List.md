---
published: true
layout: bookpage
weight: 230.3
outlevel: 4.4
category: Glyph Metadata
title: Adobe GLyph List
---

# Adobe Glyph List

In the [previous article](Glyph_Naming.html) we recommended that glyphs should be named in accordance with the standard set and maintained by Adobe®. What is this standard and how does it work?

Adobe maintains this standard in two public GitHub repositories under their [adobe-type-tools] umbrella:

- [Adobe Glyph List Specification][AGL]
- [AGL & AGLFN][agl-aglfn]

The various files in these two repos work together and should be thought of as one standard &mdash; and that standard is often called, simply, **the AGL**.

# How does it work?
There are actually number of components involved, specifying:

- allowed form for glyph names, including
  + what letters are allowed
  + permitted length
- a complete list of names that PostScript interpreters/engines are guaranteed to recognize.
- a subset of the above that is recommended for new fonts.
- a general mechanism to generate names for every character that is, or ever will be, in the Unicode standard.
- how to combine names to denote ligatures
- how to denote glyph variants (swash, small caps, etc)

# Requirements for all glyph names
At the minimum, to conform to AGL requirements, a glyph name:

- can be no longer than 31 characters, and
- must consist only of characters from the following set: A–Z, a–z, 0–9, . (period, U+002E FULL STOP), and _ (underscore, U+005F LOW LINE)

In a font project, _working glyph names_ should at least meet these two minimum requirements.

## General format
Glyph names can be thought of as having two parts, which we will call _basename_ and _suffix_. These parts are identified as follows:

- If the glyph name does not contain a period (`.`) then the entire name is the basename.
- If the glyph name contains at least one period (`.`), then the _first_ period is the separator: everything before it is the basename and everything after it is the suffix.

### Suffix
The suffix can be about anything &mdash; its purpose is to identify variant glyphs. For example a `.swsh` suffix might be used to indicate a swash variant and `.smcp` used to indicate small cap.

NB: Some modern tools such as the GlyphsApp font editor understand commonly used suffixes and will automatically build font smarts for them.

### Basename
For working names the basename can be about anything. For production names, however, it is essential that the basename be constructed so that it identifies the Unicode character(s) that the glyph represents. This mapping, from glyph name to Unicode character sequence, is the essence of the [AGL] specification.

Historically, in its own fonts, Adobe has used a lot of names that are no longer recommended. For this reason there are several different glyph lists in the AGL. For new fonts, we recommend using only the names that are in the [Adobe GLyph List for New Fonts \[AGLFN\]][aglfn].

### Basename for arbitrary Unicode character(s)
What if a needed basename is not included in the AGLFN? In this case a special naming convention using the Unicode Scalar Value [USV] of the character(s) should be used.

Characters in Unicode's Basic Multilingual Plane (BMP) may be represented by either of the formats `u<CODE>` or `uni<CODE>`. Characters in Unicode's supplemental planes may be represented only by the format `u<CODE>`. &lt;CODE&gt; is the Unicode Scalar Value of the character, an uppercase hexadecimal number four to six digits long. There must be no leading zeros, unless the code value would have fewer than four hexadecimal digits, in which case it must be padded to four digits. Surrogate code values (U+D800 to U+DFFF, inclusive) and the two noncharacter code values (U+FFFE and U+FFFF) are prohibited.  

**Caution:** while both the `uni<CODE>` and `u<CODE>` notations are likely to be supported in all modern tools, there may be older applications that do not recognize the `u<CODE>` names. For that reason, for BMP characters, we recommend using `uni<CODE>`

Ligature or other decomposition sequences that contain only BMP characters may be represented by either of the following formats:

- Underscore-separated: In this format, the underscore (`_`) separates component names. Component names may be AGL, `u<CODE>` or `uni<CODE>` names. For example: `uni1234_uni5678`.
- Code-concatenated: In this format, the glyph name is expressed as `uni` followed by two or more BMP &lt;CODE&gt;s, which indicate the code values of the components. &lt;CODE&gt; follows the same specification as for `uni<CODE>` names. For example, `uni12345678` represents &lt;U+1234, U+5678&gt;.

Ligature or other decomposition sequences that contain a supplemental character may be represented only by the underscore-separated format. For example: `u12345_u102345`, `a_u12345`.

No two glyph names in a font should yield the same (non-variant) Unicode character on analysis. If they do (e.g. `u1234` and `uni1234`), the results are unspecified.

Examples:

|Glyph name|Unicode characters(s)|
|----------|---------------------|
|`uni1234`|U+1234|
|`u1234`|U+1234|
|`u12345`|U+12345|
|`u102345`|U+102345|
|`uni102345`|UNRECOGNIZED (`uni` not allowed for supp chars)|
|`uni123`|UNRECOGNIZED (zero padding required for < 4 digits)|
|`u012345`|UNRECOGNIZED (zero padding not allowed for 5 digits)|
|`uniFFFE`|UNRECOGNIZED (U+FFFE not allowed)|
|`uniFFFF`|UNRECOGNIZED (U+FFFF not allowed)|
|`a_u102345`|U+0061, U+102345|
|`uni102345106789`|U+1023, U+4510, U+6789|
|`u102345_u106789`|U+102345, U+106789|
|`u110000`|UNRECOGNIZED (&lt;CODE&gt; must be <= 0x10FFFF)|
|`u102345106789`|UNRECOGNIZED (use `_` for supp char ligatures)|
|`uniD800DC00`|UNRECOGNIZED (surrogates not allowed)|


[adobe-type-tools]: https://github.com/adobe-type-tools
[AGL]: https://github.com/adobe-type-tools/agl-specification
[agl-aglfn]: https://github.com/adobe-type-tools/agl-aglfn
[aglfn]: https://github.com/adobe-type-tools/agl-aglfn/blob/master/aglfn.txt
