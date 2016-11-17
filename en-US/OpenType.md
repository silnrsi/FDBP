---
published: true
layout: bookpage
weight: 430
outlevel: 6.3
category: OpenType
title: OpenType
---
Links to the OpenType specification, as well as other font specifications, can be found on [ScriptSource][OTinfo on SS].

## Lookup Orders

(This section has not yet been written.)

## Language Tags

(This section has not yet been written.)

## Feature Tags

The OpenType specification provides for Layout Feature tables, each of which is identified by a 4-character tag.

(This rest of this section has not yet been written.)

## Stylistic Sets and Character Variants

Tags for Layout Feature tables which are in the range "ss01" to "ss20" are registered as Stylistic Set 1 through 20. Tags in the range "cv01" to "cv99" are registered as Character Variant 1 through 99.

When should one use [Stylistic Sets] and when should one use [Character Variants]?

According to the OT spec, Character Variants (cvxx tags) should be preferred when only a few similar characters are affected, for example, all characters based on the ‘a’ form, while Stylist Sets (ssxx tags) are preferred when systematically related changes affect a large number of characters. Having said that, there are some technical and practical distinctions that may require violating these guidelines:

- The cvxx tags utilize GSUB “alternate” (type 3) lookups, thus allowing a feature to have more than on/off values.
- There are only 20 registered ssxx features, but 99 cvxx features.
- Some apps (MS Word for example) assume that users would need to turn on only one ssxx feature at a time.
- Not as many apps support cvxx [yet].

### GSUB only

Note that only substitution type lookups are allowed in Stylistic Set and Character Variant features and the features must be in the GSUB table. There may be cases where variant positioning behavior is needed, such as a feature that controls whether a particular diacritic is drawn touching its base or separated from it. While it may seem reasonable to use positioning type lookups and place the features in the GPOS table, it is unlikely that rendering engines will process such features during positioning.

## Mark classes and filter sets

(This section has not yet been written.)

[OTinfo on SS]: http://scriptsource.org/cms/scripts/page.php?item_id=entry_detail&uid=kr5s6gwpdy

[Stylistic Sets]: http://www.microsoft.com/typography/otspec/features_pt.htm#ssxx

[Character Variants]: http://www.microsoft.com/typography/otspec/features_ae.htm#cv01-cv99
