---
published: true
layout: bookpage
weight: 140
outlevel: 3.4
category: Font Metadata
title: Line Metrics
---

Most word processors and page layout programs have two ways of setting line spacing (how far apart vertically two lines of text will be). Each program has a built-in way of guessing at a good default line spacing, but those techniques differ. Some programs look inside the font for information. Others, such as InDesign, simply set it at a percentage of the point size, usually 120%. Many also have a way to explicitly set the line spacing to a certain amount. **Whenever possible, line spacing should be set explicitly by the user rather than relying on an application's defaults. There is no technical means of specifying a consistent default line spacing across all environments from within the font.**

## Internal font line spacing settings

OpenType has a variety of internal metrics, stored in the `hhea` and `OS/2` tables, that are used by many operating systems and applications to determine default line spacing:

- in `hhea` table
  - Ascender
  - Descender
  - LineGap
- in `OS/2` table
  - sTypoAscender
  - sTypoDescender
  - sTypoLineGap
  - usWinAscent
  - usWinDescent

FontLab (in the Font Info dialog) gives you specific fields to set all eight of these values - do not let FontLab set these values automatically! Glyphs makes it easier for you and simplifies this to two settings in the Font Info/Masters panel: "Ascender" and "Descender", which it uses to set all the others.

FontForge is particularly misleading: _Element > Font Info > General_ has Ascent and Descent fields, but those are best ignored. There is a restriction in FontForge that enforces that Ascent + Descent = Em Size, which is unnecessary. All the eight values above are instead set in _Element > Font Info > OS/2_, including the "hhea" values. Be sure that the "Really use Typo metrics" box is checked.

It is possible to carefully calculate and set these values to optimize line spacing for particular environments. Karsten Lücke has an excellent [PDF that goes into great detail][Karsten]. However there is no good solution that works everywhere, so a compromise is best. **We recommend that all Ascender/Ascent values be set to be equal, Descender/Descent value be set to be equal, and LineGap be set to zero.** _Note that the WinDescent value is specified in FontForge (only) as a positive number, while the other Descender values are negative._

The "Cap height" and "x-height" values in some font design programs are not used by any app or OS, but setting them correctly might be helpful, as they may be used as guidelines.

## Avoiding trouble

Since you don’t have direct control over this default line spacing everywhere, your goal is to avoid situations where some unkind OS or app does something really bad, such as cutting off the tops or bottoms of your letters. **You should not base your line metrics decisions on how it looks in one particular application, particularly InDesign. If you do, then you will most likely run into trouble in other environments.**

When you do need to draw "outside the box" (see the [chapter on Design Metrics](Design_Metrics.html)), there is a way avoid the rare clipping situations and also improve the default line spacing. **Best practice is to set ascender values to at least the highest point in the tallest glyph in your font, and descender values to the lowest point in the deepest glyph.** If your capital ‘É’ extends to 2400 height, set your ascender values to at least 2400. Then if you have a deep swash on the ‘g’ that goes down to -900, set the descender to -900. Yes, 2400 + 900 = 3300 — a huge increase from 2048! Apps and OSes that look at these values, particularly those that might do some clipping, will then set the line spacing so that lines never collide. This is the safest and most broad solution.

What about InDesign and other programs that calculate the line spacing as a percentage of the point size? By default, InDesign will still calculate the default line spacing using the 120% of point-size method, and ‘g’ in one line might collide with ‘É’ in the next. The lines may look too close together. However at least in InDesign the typographer can set line spacing explicitly. In many apps and OSes, including some mobile apps, the typographer does not have that control. When you are testing your font, you too should follow good typographic practice and set line spacing explicitly to whatever is appropriate for the usage. **Do not allow the default line spacing in InDesign, LibreOffice, or any other application to push you into making the font less useful in other environments.**

There is one situation where you may still wish to set the ascender value lower then the tallest point and higher than the lowest point. In some fonts that have extremely high stacking diacritics, it may be OK to set the ascender value in such a way that the tallest diacritic could get partially cut off. Otherwise the default line spacing in some apps will be far too large and your users will complain. If you’re willing to allow some rare potential cutoff, then you can make more of your users happy.

## Within families

**It is also good practice to keep the ascender and descender values the same across a font family (R, B, I, BI).** Some font testing tools even report a mismatch between family members as a technical error. If they are not the same, then selecting a word in a paragraph and making it bold or italic may change the line spacing for just that one line - a frustrating and ugly problem. You may, however, set the numbers differently if you have separate font families.


[Karsten]: http://www.kltf.de/downloads/FontMetrics-kltf.pdf
