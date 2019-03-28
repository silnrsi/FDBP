---
published: true
layout: bookpage
weight: 110
outlevel: 3.1
category: Font Metadata
title: Font Naming
---

Fonts typically have two names by which they're identified: the internal font name that appears in application menus and the font filename. **These two names should be synchronized in a particular way.**

## Internal font names

The most effective font names (those seen in application menus, etc.) have a few characteristics:

- They are unique to the particular font family.
- They do not include "Unicode", as most fonts are Unicode-encoded. If the font is _not_ Unicode-encoded, then an indication of that may be added to the name, as in "Anaconda L" (for legacy).
- They do not include specific script or language names. If a font family has multiple language-specific versions, then some indication of the language (such as an [Ethnologue] code), may be added, as in "Anaconda GDX".
- They are not strongly geographic, such as the name of a province or city. In some situations a font named after a particular place can cause people in other areas to not use it.
- They are not references to particular people, such as political leaders or recent cultural heroes. Legendary or historic names are much better, as long as they are not strongly exclusive to a certain subculture.
- They may include spaces, but not numerals or any punctuation. There are some rare situations in which numbers can cause technical problems.

New fontnames should be checked for conflicts with existing fonts. The easiest way to do that is to search on [namecheck.fontdata.com].

## Font filenames

An individual font file name is typically no different from that of other files in an operating system, and is (for the most part) only bound by the limitations on legal names in that operating system. **However there is a pattern of font file naming that has become reasonably common, and that we recommend:**

> FontFamilyName-StyleName.otf

Here the spaces are removed in the family name and between any weight or style names, then a single hyphen is placed between the two. For example, the Bold Italic weight of "Source Sans Pro" would be named:

> SourceSansPro-BoldItalic.otf

Note that even if there is only one style in the family, that style should be included in the font filename, for example:

> Lateef-Regular.ttf

## Font families

Some applications and operating systems can handle complex font families with many weights, however many still do not, and trying to coordinate a well-functioning family across multiple platforms is a technical nightmare. **Best practice is that font families should normally be grouped in sets of four that correspond to Regular, Italic, Bold, and Bold Italic weights. If a design has more than four weights/styles, it is best to split them into separate groups of two or four and change the main font name for each group.**

For example, say the "Anaconda Pro" font family has four upright weights (Light, Regular, Semibold, Bold) and four corresponding italic faces. The most trouble-free way to deliver these would be as two separate font families, Anaconda Pro Light:

- Anaconda Pro Light - Regular  _(designed as Anaconda Pro - Light)_
- Anaconda Pro Light - Italic  _(designed as Anaconda Pro - Light Italic)_
- Anaconda Pro Light - Bold  _(designed as Anaconda Pro - Semibold)_
- Anaconda Pro Light - Bold Italic  _(designed as Anaconda Pro - Semibold Italic)_

and Anaconda Pro:

- Anaconda Pro - Regular  _(designed as Anaconda Pro - Regular)_
- Anaconda Pro - Italic  _(designed as Anaconda Pro - Italic)_
- Anaconda Pro - Bold  _(designed as Anaconda Pro - Bold)_
- Anaconda Pro - Bold Italic  _(designed as Anaconda Pro - Bold Italic)_

## About name strings stored in OpenType fonts
Within the OpenType font file, the naming table (tag `name`) allows multilingual strings to be associated with the ‎font. These strings can represent copyright notices, font names, ‎family names, style names, feature names and values, etc.. Within the naming table, such strings are organized by Platform, Encoding, Language, and NameID. ‎

### About platform-specific names
In the early days of TrueType and OpenType, different operating systems needed different encodings for these strings. Apple operating systems needed names stored using "script manager" encodings, while Microsoft operating systems used UCS-2. In those days for a font to work on multiple platforms, each name (e.g., the _family name_ or _style name_) had to be included in the name table multiple times (once for each platform).

While today's OpenType specification still permits inclusion of multiple platform-specific versions of each name, it is no longer necessary to do so, and they only serve to increase the size of the font file with no benefit.

Based on [this GitHub issue comment], for fonts that have a usable set of PlatformID 3 (Windows) names, **if _any_ PlatformID 1 (macOS) strings are provided then at least four such -- those with NameIDs 1, 2, 3 and 6 -- must be provided for the font to work on some at least some versions of macOS** (though this doesn't appear to be the case as of macOS 10.13.6). 

**We recommend that OpenType fonts do not include in the naming (`name`) table any strings with PlatformID values other than 3 (Windows)** as all modern operating systems will use naming tables constructed in this way.

### About language-specific names

The naming table allows for any given name (e.g., _family name_) to be provided in more than one language. However, **every naming (`name`) table entry must be provided in at least the English language.**

## References

[ScriptSource blog post regarding font naming recommendations]

[Ethnologue]: http://www.ethnologue.com/
[namecheck.fontdata.com]: http://namecheck.fontdata.com
[ScriptSource blog post regarding font naming recommendations]: http://scriptsource.org/cms/scripts/page.php?item_id=entry_detail&uid=k7dwx5fhnz
[this GitHub issue comment]: https://github.com/fonttools/fonttools/issues/1170#issuecomment-368492829