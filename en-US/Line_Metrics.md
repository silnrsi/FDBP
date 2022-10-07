---
published: true
layout: bookpage
weight: 140
outlevel: 3.4
category: Font Metadata
title: Line Metrics
---

Most word processors and page layout programs have two ways of setting line spacing (how far apart vertically two lines of text will be)—automatic and manual (“exactly”). Each program has a built-in way of automatically guessing at a good default line spacing, but those techniques differ. Some programs look inside the font for information. Others, such as InDesign, simply set it at a percentage of the point size, usually 120%. Many also have a way to explicitly (manually) set the line spacing to a certain amount. **Whenever possible, line spacing should be set explicitly by the user rather than relying on an application’s defaults. There is no technical means of specifying a consistent default line spacing across all environments from within the font. However it is important to try and make it as consistent as is reasonable, and to provide good default spacing.**

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

The `hhea` values are the historically oldest, originally established by Apple. The `OS/2` sTypo* values were added later by Microsoft and are the ones most apps should be using today. The `OS/2` usWin* values were initially intended to determine clipping—meaning that any part of the glyph that extends above _usWinAscent_, or below _usWinDescent_, could get chopped off. Unfortunately some apps misused usWin* to also set line spacing.

**It is important to set all eight of these values sensibly in order to minimize inconsistencies and problems in line spacing and clipping across a variety of environments.**

Glyphs tries to make line spacing easy to set and simplifies this to two settings in the _Font Info/Masters_ panel: _Ascender_ and _Descender_, which it uses to set all the others. However, setting optimum line spacing metrics requires manually overriding these settings through _Custom Parameters_ (see [Glyphs vertical metrics tutorial](https://glyphsapp.com/learn/vertical-metrics)). FontLab also provides access to individual vertical metrics. FontForge is particularly misleading: _Element > Font Info > General_ has _Ascent_ and _Descent_ fields, but those are best ignored. There is a restriction in FontForge that enforces that _Ascent + Descent = Em Size_, which is unnecessary. All the eight values above are instead set in _Element > Font Info > OS/2_, including the `hhea` values.

There is an additional parameter in the `OS/2` table—bit 7 of _fsSelection_—that affects line spacing. Setting this bit tells applications to use the sTypo* values for line spacing. In Glyphs you set this by adding a `Use Typo Metrics` custom parameter. In FontLab check _Prefer typo metrics_ in _File > Font Info > Other Values > Family dimensions_. In FontForge set the _Really use Typo metrics_ box. **This bit should be set for all fonts, even though some old software (e.g. Word 2003) may misinterpret it.**

The _Cap height_ and _x-height_ values in some font design programs are not used directly by apps, but setting them correctly might be helpful, as they may be used as guidelines. Recent CSS proposals also hint that setting these correctly in the font will enable improved layout alignment for things like drop caps.

**Keep the ascender and descender values the same across a font family (R, B, I, BI).** Some font testing tools report a mismatch between family members as a technical error. If they are not the same, then selecting a word in a paragraph and making it bold or italic may change the line spacing for just that one line—a frustrating and ugly problem. You may, however, set the numbers differently if you have separate font families.

## Three main strategies

Since you don’t have direct control over default line spacing everywhere, your primary goal is to avoid situations where some unkind OS or app does something really bad, such as cutting off the tops or bottoms of your letters. Your secondary goal is to give the font reasonable default line spacing. The following three strategies can be used to address both goals.

These strategies almost exactly match what Google recommends in their [vertical metrics specification](https://googlefonts.github.io/gf-guide/metrics.html). There are minor differences. One area of strong agreement is that _LineGap/sTypoLineGap_ be set to zero. There are legitimate reasons you might consider setting these to some other value, but we don’t recommend it unless you have a specific purpose. For those alternate strategies see the [Glyphs vertical metrics tutorial](https://glyphsapp.com/learn/vertical-metrics) and [John Hudson’s technique](https://typedrawers.com/discussion/4554/on-vertical-metrics-in-the-context-of-a-biscript-tamil-and-latin-font).

### Minimal—eliminate clipping

_Use this strategy if you want to do the minimum amount of work, keep things simple, and eliminate clipping. However, it may result in line spacing that is wider than desired._

**Find the highest point in the tallest glyph in your font and set all the ascender-related values to at least that height (_yMax_), then set all the descender-related values to the lowest point in the deepest glyph or lower (_yMin_).** If your capital ‘É’ extends to 2400 height, set your ascender values to at least 2400. Then if you have a deep swash on the ‘g’ that goes down to -900, set the descender to -900. Yes, 2400 + 900 = 3300 — much larger than the font UPM (2048 in this case)! There is a script for Glyphs (see [tutorial](https://glyphsapp.com/learn/vertical-metrics)) that will do this analysis for you. 

Apps and OSes that look at these values, particularly those that might do some clipping, will then set the line spacing so that lines never collide. This is the safest, easiest, and most broad solution.  _Note that the usWinDescent value is specified in FontForge (only) as a positive number, while the other Descender values are negative._

For example, in UFO3 format font sources (fontinfo.plist) this would mean:

```
openTypeHheaAscender = openTypeOS2TypoAscender = openTypeOS2WinAscent = ascender`
openTypeHheaDescender = openTypeOS2TypoDescender = descender
openTypeOS2WinDescent = -descender
openTypeHheaLineGap = openTypeOS2TypoLineGap = 0
```

**When using this strategy you should also take into account the effects of any diacritic positioning done via [Graphite](http://graphite.sil.org/) or [OpenType](http://scriptsource.org/cms/scripts/page.php?item_id=entry_detail&uid=kr5s6gwpdy).** For example, your analysis may determine that the tallest glyph in the font has a height of 2100. However, you also have OpenType code that positions a diacritic above that letter, even though there is no composite glyph for that combination in the font. When positioned by OpenType, the diacritic is raised so that the top reaches 2600 units. In this case the _ascender_ value should be set to at least 2600. This may be particularly important for non-Latin fonts with floating elements that are attached to ascenders/descenders.

The one main disadvantage of this strategy is that it may cause line spacing to be wider than would be ideal for normal usage. If you have even one rare glyph or combination that is extremely high or low the line spacing will be maximized for that glyph. Users may complain that the lines are too far apart.

The next strategy allows greater control over default line spacing without additional risk of clipping.

### Recommended—ideal line spacing for new fonts

_Use this strategy if you are creating a new font and want to fine-tune line spacing without additional risk of clipping. This may not be appropriate for fonts that have already been released._

**Begin by setting the _usWinAscent_ and _usWinDescent_ values based on the _yMax_ and _yMin_ values as in the _Minimal_ strategy.** This will eliminate most clipping.

**Set preliminary line spacing by looking at the most commonly-used glyphs and combinations in the font.** Take the high and low points of those glyphs and round the height up and depth down slightly to set the _sTypoAscender_ and _sTypoDescender_. Set the `hhea` _Ascender_ and _Descender_ to the same values and _LineGap/sTypoLineGap_ to zero.

**Test the line spacing in an application that uses the default spacing defined in the font**, such as TextEdit (macOS) or Microsoft Word (Windows). Be sure to use the current version of the app, not old versions. Do not use InDesign (see below). If the line spacing seems too large, reduce the values proportionally. If the spacing is too tight, add more proportionally.

The goal with this is to determine a line spacing that will likely please most users, even though it may be too close for some rare combinations. For example, in a Latin-script font the ascender values will need to be at least the height of Á but maybe not the rarer Ǻ (A with ring and acute above). For fonts that support multiple scripts (such as Devanagari and Latin) give more importance to the primary script (which may not be the Latin).
When you’ve settled on pleasant line spacing settings, then review the usWin* values. If they are smaller than the sTypo* ones, increase them to match. In most cases the usWin* values will be greater—leave them that way. 

### Legacy—for existing fonts

_Use this strategy for updating the line spacing metrics in an existing, published font family._

Changing any line spacing metrics in an existing font is risky. It can cause existing documents to “break” if a new version is installed. If the application has set the document line spacing based on the default spacing in the font, a change can affect page breaks, document length, and other important aspects (e.g. spacing of headers, captions, etc.). **If you decide to change the line metrics of an existing font, then be as kind to your users as is possible.**

**If your users don’t like the current line spacing treat it as a new font and use the _Recommended_ strategy above.** However you should be very careful to help users understand that it may change all their documents! If your users like the current line spacing, continue with the next steps.

**Determine the _yMax/yMin_ of the font as in the _Minimum_ strategy and compare that to the existing usWin* metrics.** If the usWin* metrics are less than _yMax/yMin_ then the glyphs may be clipped in some environments and should be changed to at least _yMax/yMin_. There are few applications that this will affect badly, and they are not often used for typographic layout (e.g. Windows Notepad).

**Change other metrics only if they are inconsistent or produce bad line spacing.** If the other line metrics are consistent with one another (_sTypoAscender=Ascender_, _sTypoDescender=Descender_, _sTypoLineGap=LineGap_), and users like the current line spacing, then set the _fsSelection_ bit 7 (_Use Typo Metrics_) and leave everything alone!

If these values are inconsistent then you may need to decide which applications/environments are more important to keep unchanged. In most cases, keeping the sTypo* metrics unchanged, and setting _fsSelection_ bit 7, will have the least impact on users. Change _Ascender_, _Descender_, and _LineGap_ to match. If iOS and macOS apps (not including InDesign) are most important, then in some cases it may be better to change the sTypo* metrics.

**Communicate your changes to users.** Any change in line spacing should be considered a “breaking” change and should only be made in major font version updates (e.g. 3.000 to 4.000). You may even consider changing the font family name to enable users to have both old and new installed at the same time (e.g. Scheherazade to Scheherazade New).

## Testing and design considerations

**Good line spacing is determined by typographic culture rather than mathematical measurements.** Typographic history and tradition shapes what a particular culture considers acceptable or ideal line spacing for their script. In some scripts the expected line spacing may be much wider than is technically necessary. Even within a single script the expectations may very for different styles and purposes. For example, in the Latin script a traditional _Garamond_ design designed for fine books may be expected to have more generous default line spacing than a simple sans serif design for UI purposes. 

**Make decisions based on the primary script.** For fonts that support multiple scripts there may be no line spacing that is ideal for all the supported scripts. In those situations you need to decide which script is most important for line spacing purposes—usually (but not always) the script for which the font will be used the most. Fonts that are designed to be part of a set of related fonts (like Noto) may need to set line spacing metrics to be more consistent with other members of the superfamily. Unfortunately there is no way to define multiple sets of metrics in a font on a per-script basis, although John Hudson has made valiant efforts to get the industry to embrace that possibility.

**Test using real-life documents.** Good line spacing is affected by context, and column width in particular. Thin columns, such as those in many newspapers, can be tightly spaced since the eye has no difficulty in finding where the next line begins. Wide columns, however, need more interlinear space since the eye needs to travel further to the beginning of the next line and needs greater distinction between lines. Testing with real documents and likely typographic contexts, especially when the application depends on default spacing, is more likely to produce useful results.

**Do not test line spacing with InDesign or any other applications that calculate line spacing as a percentage of the point size.** No matter what you set in the font, InDesign will still calculate the default line spacing using the 120% of point-size method. This means that you need to test your font outside of InDesign and especially in apps that allow no control over line spacing. Do not allow the default line spacing in InDesign, LibreOffice, or any other application to push you into making the font less useful in other environments.

## References

The following sources provide background material on line spacing technical issues. Some of them suggest alternate methods of setting line metrics. Depending on your particular use these methods may be useful. However, the _Recommended_ strategy above remains the most reliable and consistent method of setting consistent line metrics across a broad range of operating system and application versions.

- [Google Vertical Metrics Specification](https://googlefonts.github.io/gf-guide/metrics.html). A clear specification, especially for web fonts, that agrees almost completely with our recommendations.
- [Glyphs vertical metrics tutorial](https://glyphsapp.com/learn/vertical-metrics). An excellent summary of different techniques, focused on a “webfont” strategy that works well for web fonts but is slightly different from ours.
- [John Hudson’s Typedrawers post on line metrics](https://typedrawers.com/discussion/4554/on-vertical-metrics-in-the-context-of-a-biscript-tamil-and-latin-font). A solid alternate technique with similar results to the _Recommended_ technique above.
- [Karsten Lücke’s PDF on font metrics](http://www.kltf.de/downloads/FontMetrics-kltf.pdf)
Contains valuable and interesting historical detail.
