## Fontbakery report

Fontbakery version: 0.7.31

<details>
<summary><b>[1] Family checks</b></summary>
<details>
<summary>⚠ <b>WARN:</b> Is the command `ftxvalidator` (Apple Font Tool Suite) available?</summary>

* [com.google.fonts/check/ftxvalidator_is_available](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/universal.html#com.google.fonts/check/ftxvalidator_is_available)
<pre>--- Rationale ---

There&#x27;s no reasonable (and legal) way to run the command `ftxvalidator` of the
Apple Font Tool Suite on a non-macOS machine. I.e. on GNU+Linux or Windows etc.

If Font Bakery is not running on an OSX machine, the machine running Font
Bakery could access `ftxvalidator` on OSX, e.g. via ssh or a remote procedure
call (rpc).

There&#x27;s an ssh example implementation at:
https://github.com/googlefonts/fontbakery/blob/master/prebuilt/workarounds
/ftxvalidator/ssh-implementation/ftxvalidator


</pre>

* ⚠ **WARN** Could not find ftxvalidator.

</details>
<br>
</details>
<details>
<summary><b>[8] PaletteMosaicFontOne-Regular.ttf</b></summary>
<details>
<summary>🔥 <b>FAIL:</b> Check `Google Fonts Latin Core` glyph coverage.</summary>

* [com.google.fonts/check/glyph_coverage](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/glyph_coverage)
<pre>--- Rationale ---

Google Fonts expects that fonts in its collection support at least the minimal
set of characters defined in the `GF-latin-core` glyph-set.


</pre>

* 🔥 **FAIL** Missing required codepoints: 0x00A1 (INVERTED EXCLAMATION MARK), 0x00A2 (CENT SIGN), 0x00A3 (POUND SIGN), 0x00A4 (CURRENCY SIGN) and 112 more. [code: missing-codepoints]

</details>
<details>
<summary>🔥 <b>FAIL:</b> Font enables smart dropout control in "prep" table instructions?</summary>

* [com.google.fonts/check/smart_dropout](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/smart_dropout)
<pre>--- Rationale ---

This setup is meant to ensure consistent rendering quality for fonts across all
devices (with different rendering/hinting capabilities).

Below is the snippet of instructions we expect to see in the fonts:
B8 01 FF    PUSHW 0x01FF
85          SCANCTRL (unconditinally turn on
                      dropout control mode)
B0 04       PUSHB 0x04
8D          SCANTYPE (enable smart dropout control)

&quot;Smart dropout control&quot; means activating rules 1, 2 and 5:
Rule 1: If a pixel&#x27;s center falls within the glyph outline,
        that pixel is turned on.
Rule 2: If a contour falls exactly on a pixel&#x27;s center,
        that pixel is turned on.
Rule 5: If a scan line between two adjacent pixel centers
        (either vertical or horizontal) is intersected
        by both an on-Transition contour and an off-Transition
        contour and neither of the pixels was already turned on
        by rules 1 and 2, turn on the pixel which is closer to
        the midpoint between the on-Transition contour and
        off-Transition contour. This is &quot;Smart&quot; dropout control.

For more detailed info (such as other rules not enabled in this snippet),
please refer to the TrueType Instruction Set documentation.


</pre>

* 🔥 **FAIL** The 'prep' table does not contain TrueType instructions enabling smart dropout control. To fix, export the font with autohinting enabled, or run ttfautohint on the font, or run the `gftools fix-nonhinting` script. [code: lacks-smart-dropout]

</details>
<details>
<summary>🔥 <b>FAIL:</b> Checking OS/2 Metrics match hhea Metrics.</summary>

* [com.google.fonts/check/os2_metrics_match_hhea](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/universal.html#com.google.fonts/check/os2_metrics_match_hhea)
<pre>--- Rationale ---

When OS/2 and hhea vertical metrics match, the same linespacing results on
macOS, GNU+Linux and Windows. Unfortunately as of 2018, Google Fonts has
released many fonts with vertical metrics that don&#x27;t match in this way. When we
fix this issue in these existing families, we will create a visible change in
line/paragraph layout for either Windows or macOS users, which will upset some
of them.

But we have a duty to fix broken stuff, and inconsistent paragraph layout is
unacceptably broken when it is possible to avoid it.

If users complain and prefer the old broken version, they have the freedom to
take care of their own situation.


</pre>

* 🔥 **FAIL** OS/2 sTypoAscender (880) and hhea ascent (1160) must be equal. [code: ascender]

</details>
<details>
<summary>⚠ <b>WARN:</b> Checking OS/2 achVendID.</summary>

* [com.google.fonts/check/vendor_id](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/vendor_id)
<pre>--- Rationale ---

Microsoft keeps a list of font vendors and their respective contact info. This
list is updated regularly and is indexed by a 4-char &quot;Vendor ID&quot; which is
stored in the achVendID field of the OS/2 table.

Registering your ID is not mandatory, but it is a good practice since some
applications may display the type designer / type foundry contact info on some
dialog and also because that info will be visible on Microsoft&#x27;s website:

https://docs.microsoft.com/en-us/typography/vendors/

This check verifies whether or not a given font&#x27;s vendor ID is registered in
that list or if it has some of the default values used by the most common font
editors.

Each new FontBakery release includes a cached copy of that list of vendor IDs.
If you registered recently, you&#x27;re safe to ignore warnings emitted by this
check, since your ID will soon be included in one of our upcoming releases.


</pre>

* ⚠ **WARN** OS/2 VendorID value 'SBYA' is not yet recognized. If you registered it recently, then it's safe to ignore this warning message. Otherwise, you should set it to your own unique 4 character code, and register it with Microsoft at https://www.microsoft.com/typography/links/vendorlist.aspx
 [code: unknown]

</details>
<details>
<summary>⚠ <b>WARN:</b> Is the Grid-fitting and Scan-conversion Procedure ('gasp') table set to optimize rendering?</summary>

* [com.google.fonts/check/gasp](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/gasp)
<pre>--- Rationale ---

Traditionally version 0 &#x27;gasp&#x27; tables were set so that font sizes below 8 ppem
had no grid fitting but did have antialiasing. From 9-16 ppem, just grid
fitting. And fonts above 17ppem had both antialiasing and grid fitting toggled
on. The use of accelerated graphics cards and higher resolution screens make
this approach obsolete. Microsoft&#x27;s DirectWrite pushed this even further with
much improved rendering built into the OS and apps.

In this scenario it makes sense to simply toggle all 4 flags ON for all font
sizes.


</pre>

* ⚠ **WARN** The gasp range 0xFFFF value 0x0A should be set to 0x0F. [code: unset-flags]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check if each glyph has the recommended amount of contours.</summary>

* [com.google.fonts/check/contour_count](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/contour_count)
<pre>--- Rationale ---

Visually QAing thousands of glyphs by hand is tiring. Most glyphs can only be
constructured in a handful of ways. This means a glyph&#x27;s contour count will
only differ slightly amongst different fonts, e.g a &#x27;g&#x27; could either be 2 or 3
contours, depending on whether its double story or single story.

However, a quotedbl should have 2 contours, unless the font belongs to a
display family.

This check currently does not cover variable fonts because there&#x27;s plenty of
alternative ways of constructing glyphs with multiple outlines for each feature
in a VarFont. The expected contour count data for this check is currently
optimized for the typical construction of glyphs in static fonts.


</pre>

* ⚠ **WARN** This check inspects the glyph outlines and detects the total number of contours in each of them. The expected values are infered from the typical ammounts of contours observed in a large collection of reference font families. The divergences listed below may simply indicate a significantly different design on some of your glyphs. On the other hand, some of these may flag actual bugs in the font such as glyphs mapped to an incorrect codepoint. Please consider reviewing the design and codepoint assignment of these to make sure they are correct.

The following glyphs do not have the recommended number of contours:

Glyph name: ampersand	Contours detected: 4	Expected: 1, 2 or 3
Glyph name: parenleft	Contours detected: 3	Expected: 1
Glyph name: parenright	Contours detected: 3	Expected: 1
Glyph name: asterisk	Contours detected: 2	Expected: 1 or 4
Glyph name: comma	Contours detected: 2	Expected: 1
Glyph name: period	Contours detected: 2	Expected: 1
Glyph name: one	Contours detected: 2	Expected: 1
Glyph name: three	Contours detected: 4	Expected: 1
Glyph name: five	Contours detected: 3	Expected: 1
Glyph name: seven	Contours detected: 2	Expected: 1
Glyph name: eight	Contours detected: 4	Expected: 3
Glyph name: colon	Contours detected: 4	Expected: 2
Glyph name: semicolon	Contours detected: 4	Expected: 2
Glyph name: question	Contours detected: 3	Expected: 2
Glyph name: at	Contours detected: 4	Expected: 2
Glyph name: C	Contours detected: 3	Expected: 1
Glyph name: D	Contours detected: 1	Expected: 2
Glyph name: E	Contours detected: 4	Expected: 1
Glyph name: G	Contours detected: 2	Expected: 1
Glyph name: L	Contours detected: 2	Expected: 1
Glyph name: Q	Contours detected: 1	Expected: 2
Glyph name: S	Contours detected: 3	Expected: 1
Glyph name: W	Contours detected: 3	Expected: 1 or 2
Glyph name: bracketleft	Contours detected: 3	Expected: 1
Glyph name: bracketright	Contours detected: 3	Expected: 1
Glyph name: c	Contours detected: 3	Expected: 1
Glyph name: f	Contours detected: 2	Expected: 1
Glyph name: h	Contours detected: 2	Expected: 1
Glyph name: m	Contours detected: 2	Expected: 1
Glyph name: n	Contours detected: 2	Expected: 1
Glyph name: r	Contours detected: 2	Expected: 1
Glyph name: s	Contours detected: 4	Expected: 1
Glyph name: u	Contours detected: 2	Expected: 1
Glyph name: w	Contours detected: 2	Expected: 1
Glyph name: braceleft	Contours detected: 3	Expected: 1
Glyph name: braceright	Contours detected: 3	Expected: 1
Glyph name: asciitilde	Contours detected: 2	Expected: 1
Glyph name: C	Contours detected: 3	Expected: 1
Glyph name: D	Contours detected: 1	Expected: 2
Glyph name: E	Contours detected: 4	Expected: 1
Glyph name: G	Contours detected: 2	Expected: 1
Glyph name: L	Contours detected: 2	Expected: 1
Glyph name: Q	Contours detected: 1	Expected: 2
Glyph name: S	Contours detected: 3	Expected: 1
Glyph name: W	Contours detected: 3	Expected: 1 or 2
Glyph name: ampersand	Contours detected: 4	Expected: 1, 2 or 3
Glyph name: asciitilde	Contours detected: 2	Expected: 1
Glyph name: asterisk	Contours detected: 2	Expected: 1 or 4
Glyph name: at	Contours detected: 4	Expected: 2
Glyph name: braceleft	Contours detected: 3	Expected: 1
Glyph name: braceright	Contours detected: 3	Expected: 1
Glyph name: bracketleft	Contours detected: 3	Expected: 1
Glyph name: bracketright	Contours detected: 3	Expected: 1
Glyph name: c	Contours detected: 3	Expected: 1
Glyph name: colon	Contours detected: 4	Expected: 2
Glyph name: comma	Contours detected: 2	Expected: 1
Glyph name: eight	Contours detected: 4	Expected: 3
Glyph name: f	Contours detected: 2	Expected: 1
Glyph name: five	Contours detected: 3	Expected: 1
Glyph name: h	Contours detected: 2	Expected: 1
Glyph name: m	Contours detected: 2	Expected: 1
Glyph name: n	Contours detected: 2	Expected: 1
Glyph name: one	Contours detected: 2	Expected: 1
Glyph name: parenleft	Contours detected: 3	Expected: 1
Glyph name: parenright	Contours detected: 3	Expected: 1
Glyph name: period	Contours detected: 2	Expected: 1
Glyph name: question	Contours detected: 3	Expected: 2
Glyph name: r	Contours detected: 2	Expected: 1
Glyph name: s	Contours detected: 4	Expected: 1
Glyph name: semicolon	Contours detected: 4	Expected: 2
Glyph name: seven	Contours detected: 2	Expected: 1
Glyph name: three	Contours detected: 4	Expected: 1
Glyph name: u	Contours detected: 2	Expected: 1
Glyph name: w	Contours detected: 2	Expected: 1 [code: contour-count]

</details>
<details>
<summary>⚠ <b>WARN:</b> Combined length of family and style must not exceed 27 characters.</summary>

* [com.google.fonts/check/name/family_and_style_max_length](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/name/family_and_style_max_length)
<pre>--- Rationale ---

According to a GlyphsApp tutorial [1], in order to make sure all versions of
Windows recognize it as a valid font file, we must make sure that the
concatenated length of the familyname (NameID.FONT_FAMILY_NAME) and style
(NameID.FONT_SUBFAMILY_NAME) strings in the name table do not exceed 20
characters.

After discussing the problem in more detail at `FontBakery issue #2179 [2] we
decided that allowing up to 27 chars would still be on the safe side, though.

[1]
https://glyphsapp.com/tutorials/multiple-masters-part-3-setting-up-instances
[2] https://github.com/googlefonts/fontbakery/issues/2179


</pre>

* ⚠ **WARN** The combined length of family and style exceeds 27 chars in the following 'WINDOWS' entries:
 FONT_FAMILY_NAME = 'Palette Mosaic Font One' / SUBFAMILY_NAME = 'Regular'

Please take a look at the conversation at https://github.com/googlefonts/fontbakery/issues/2179 in order to understand the reasoning behind these name table records max-length criteria. [code: too-long]

</details>
<details>
<summary>⚠ <b>WARN:</b> Does GPOS table have kerning information?</summary>

* [com.google.fonts/check/gpos_kerning_info](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gpos.html#com.google.fonts/check/gpos_kerning_info)

* ⚠ **WARN** GPOS table lacks kerning information. [code: lacks-kern-info]

</details>
<br>
</details>
<details>
<summary><b>[12] PaletteMosaicOne-Regular.ttf</b></summary>
<details>
<summary>💔 <b>ERROR:</b> Checking file is named canonically.</summary>

* [com.google.fonts/check/canonical_filename](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/canonical_filename)
<pre>--- Rationale ---

A font&#x27;s filename must be composed in the following manner:
&lt;familyname&gt;-&lt;stylename&gt;.ttf

- Nunito-Regular.ttf,
- Oswald-BoldItalic.ttf

Variable fonts must list the axis tags in alphabetical order in square brackets
and separated by commas:

- Roboto[wdth,wght].ttf
- Familyname-Italic[wght].ttf


</pre>

* 💔 **ERROR** Failed with FileNotFoundError: [Errno 2] No such file or directory: 'PaletteMosaicOne-Regular.ttf'

</details>
<details>
<summary>💔 <b>ERROR:</b> Show hinting filesize impact.</summary>

* [com.google.fonts/check/hinting_impact](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/hinting_impact)
<pre>--- Rationale ---

This check is merely informative, displaying and useful comparison of filesizes
of hinted versus unhinted font files.


</pre>

* 💔 **ERROR** The condition <FontBakeryCondition:hinting_stats> had an error: FileNotFoundError: [Errno 2] No such file or directory: 'PaletteMosaicOne-Regular.ttf'

</details>
<details>
<summary>💔 <b>ERROR:</b> Font has old ttfautohint applied?</summary>

* [com.google.fonts/check/old_ttfautohint](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/old_ttfautohint)
<pre>--- Rationale ---

This check finds which version of ttfautohint was used, by inspecting name
table entries and then finds which version of ttfautohint is currently
installed in the system.


</pre>

* 💔 **ERROR** The check <FontBakeryCheck:com.google.fonts/check/old_ttfautohint> had an error: FailedConditionError: The condition <FontBakeryCondition:hinting_stats> had an error: FileNotFoundError: [Errno 2] No such file or directory: 'PaletteMosaicOne-Regular.ttf'

</details>
<details>
<summary>💔 <b>ERROR:</b> Checking with fontTools.ttx</summary>

* [com.google.fonts/check/ttx-roundtrip](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/universal.html#com.google.fonts/check/ttx-roundtrip)

* 💔 **ERROR** Failed with FileNotFoundError: [Errno 2] No such file or directory: 'PaletteMosaicOne-Regular.ttf'

</details>
<details>
<summary>🔥 <b>FAIL:</b> Check `Google Fonts Latin Core` glyph coverage.</summary>

* [com.google.fonts/check/glyph_coverage](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/glyph_coverage)
<pre>--- Rationale ---

Google Fonts expects that fonts in its collection support at least the minimal
set of characters defined in the `GF-latin-core` glyph-set.


</pre>

* 🔥 **FAIL** Missing required codepoints: 0x00A1 (INVERTED EXCLAMATION MARK), 0x00A2 (CENT SIGN), 0x00A3 (POUND SIGN), 0x00A4 (CURRENCY SIGN) and 112 more. [code: missing-codepoints]

</details>
<details>
<summary>🔥 <b>FAIL:</b> Font enables smart dropout control in "prep" table instructions?</summary>

* [com.google.fonts/check/smart_dropout](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/smart_dropout)
<pre>--- Rationale ---

This setup is meant to ensure consistent rendering quality for fonts across all
devices (with different rendering/hinting capabilities).

Below is the snippet of instructions we expect to see in the fonts:
B8 01 FF    PUSHW 0x01FF
85          SCANCTRL (unconditinally turn on
                      dropout control mode)
B0 04       PUSHB 0x04
8D          SCANTYPE (enable smart dropout control)

&quot;Smart dropout control&quot; means activating rules 1, 2 and 5:
Rule 1: If a pixel&#x27;s center falls within the glyph outline,
        that pixel is turned on.
Rule 2: If a contour falls exactly on a pixel&#x27;s center,
        that pixel is turned on.
Rule 5: If a scan line between two adjacent pixel centers
        (either vertical or horizontal) is intersected
        by both an on-Transition contour and an off-Transition
        contour and neither of the pixels was already turned on
        by rules 1 and 2, turn on the pixel which is closer to
        the midpoint between the on-Transition contour and
        off-Transition contour. This is &quot;Smart&quot; dropout control.

For more detailed info (such as other rules not enabled in this snippet),
please refer to the TrueType Instruction Set documentation.


</pre>

* 🔥 **FAIL** The 'prep' table does not contain TrueType instructions enabling smart dropout control. To fix, export the font with autohinting enabled, or run ttfautohint on the font, or run the `gftools fix-nonhinting` script. [code: lacks-smart-dropout]

</details>
<details>
<summary>🔥 <b>FAIL:</b> Checking OS/2 Metrics match hhea Metrics.</summary>

* [com.google.fonts/check/os2_metrics_match_hhea](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/universal.html#com.google.fonts/check/os2_metrics_match_hhea)
<pre>--- Rationale ---

When OS/2 and hhea vertical metrics match, the same linespacing results on
macOS, GNU+Linux and Windows. Unfortunately as of 2018, Google Fonts has
released many fonts with vertical metrics that don&#x27;t match in this way. When we
fix this issue in these existing families, we will create a visible change in
line/paragraph layout for either Windows or macOS users, which will upset some
of them.

But we have a duty to fix broken stuff, and inconsistent paragraph layout is
unacceptably broken when it is possible to avoid it.

If users complain and prefer the old broken version, they have the freedom to
take care of their own situation.


</pre>

* 🔥 **FAIL** OS/2 sTypoAscender (880) and hhea ascent (1160) must be equal. [code: ascender]

</details>
<details>
<summary>🔥 <b>FAIL:</b> Checking with ots-sanitize.</summary>

* [com.google.fonts/check/ots](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/universal.html#com.google.fonts/check/ots)

* 🔥 **FAIL** ots-sanitize returned an error code (1). Output follows:

Failed to open: PaletteMosaicOne-Regular.ttf


</details>
<details>
<summary>⚠ <b>WARN:</b> Checking OS/2 achVendID.</summary>

* [com.google.fonts/check/vendor_id](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/vendor_id)
<pre>--- Rationale ---

Microsoft keeps a list of font vendors and their respective contact info. This
list is updated regularly and is indexed by a 4-char &quot;Vendor ID&quot; which is
stored in the achVendID field of the OS/2 table.

Registering your ID is not mandatory, but it is a good practice since some
applications may display the type designer / type foundry contact info on some
dialog and also because that info will be visible on Microsoft&#x27;s website:

https://docs.microsoft.com/en-us/typography/vendors/

This check verifies whether or not a given font&#x27;s vendor ID is registered in
that list or if it has some of the default values used by the most common font
editors.

Each new FontBakery release includes a cached copy of that list of vendor IDs.
If you registered recently, you&#x27;re safe to ignore warnings emitted by this
check, since your ID will soon be included in one of our upcoming releases.


</pre>

* ⚠ **WARN** OS/2 VendorID value 'DRPT' is not yet recognized. If you registered it recently, then it's safe to ignore this warning message. Otherwise, you should set it to your own unique 4 character code, and register it with Microsoft at https://www.microsoft.com/typography/links/vendorlist.aspx
 [code: unknown]

</details>
<details>
<summary>⚠ <b>WARN:</b> Is the Grid-fitting and Scan-conversion Procedure ('gasp') table set to optimize rendering?</summary>

* [com.google.fonts/check/gasp](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/gasp)
<pre>--- Rationale ---

Traditionally version 0 &#x27;gasp&#x27; tables were set so that font sizes below 8 ppem
had no grid fitting but did have antialiasing. From 9-16 ppem, just grid
fitting. And fonts above 17ppem had both antialiasing and grid fitting toggled
on. The use of accelerated graphics cards and higher resolution screens make
this approach obsolete. Microsoft&#x27;s DirectWrite pushed this even further with
much improved rendering built into the OS and apps.

In this scenario it makes sense to simply toggle all 4 flags ON for all font
sizes.


</pre>

* ⚠ **WARN** The gasp range 0xFFFF value 0x0A should be set to 0x0F. [code: unset-flags]

</details>
<details>
<summary>⚠ <b>WARN:</b> Check if each glyph has the recommended amount of contours.</summary>

* [com.google.fonts/check/contour_count](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/googlefonts.html#com.google.fonts/check/contour_count)
<pre>--- Rationale ---

Visually QAing thousands of glyphs by hand is tiring. Most glyphs can only be
constructured in a handful of ways. This means a glyph&#x27;s contour count will
only differ slightly amongst different fonts, e.g a &#x27;g&#x27; could either be 2 or 3
contours, depending on whether its double story or single story.

However, a quotedbl should have 2 contours, unless the font belongs to a
display family.

This check currently does not cover variable fonts because there&#x27;s plenty of
alternative ways of constructing glyphs with multiple outlines for each feature
in a VarFont. The expected contour count data for this check is currently
optimized for the typical construction of glyphs in static fonts.


</pre>

* ⚠ **WARN** This check inspects the glyph outlines and detects the total number of contours in each of them. The expected values are infered from the typical ammounts of contours observed in a large collection of reference font families. The divergences listed below may simply indicate a significantly different design on some of your glyphs. On the other hand, some of these may flag actual bugs in the font such as glyphs mapped to an incorrect codepoint. Please consider reviewing the design and codepoint assignment of these to make sure they are correct.

The following glyphs do not have the recommended number of contours:

Glyph name: ampersand	Contours detected: 4	Expected: 1, 2 or 3
Glyph name: parenleft	Contours detected: 3	Expected: 1
Glyph name: parenright	Contours detected: 3	Expected: 1
Glyph name: asterisk	Contours detected: 2	Expected: 1 or 4
Glyph name: comma	Contours detected: 2	Expected: 1
Glyph name: period	Contours detected: 2	Expected: 1
Glyph name: one	Contours detected: 2	Expected: 1
Glyph name: three	Contours detected: 4	Expected: 1
Glyph name: five	Contours detected: 3	Expected: 1
Glyph name: seven	Contours detected: 2	Expected: 1
Glyph name: eight	Contours detected: 4	Expected: 3
Glyph name: colon	Contours detected: 4	Expected: 2
Glyph name: semicolon	Contours detected: 4	Expected: 2
Glyph name: question	Contours detected: 3	Expected: 2
Glyph name: at	Contours detected: 4	Expected: 2
Glyph name: C	Contours detected: 3	Expected: 1
Glyph name: D	Contours detected: 1	Expected: 2
Glyph name: E	Contours detected: 4	Expected: 1
Glyph name: G	Contours detected: 2	Expected: 1
Glyph name: L	Contours detected: 2	Expected: 1
Glyph name: Q	Contours detected: 1	Expected: 2
Glyph name: S	Contours detected: 3	Expected: 1
Glyph name: W	Contours detected: 3	Expected: 1 or 2
Glyph name: bracketleft	Contours detected: 3	Expected: 1
Glyph name: bracketright	Contours detected: 3	Expected: 1
Glyph name: c	Contours detected: 3	Expected: 1
Glyph name: f	Contours detected: 2	Expected: 1
Glyph name: h	Contours detected: 2	Expected: 1
Glyph name: m	Contours detected: 2	Expected: 1
Glyph name: n	Contours detected: 2	Expected: 1
Glyph name: r	Contours detected: 2	Expected: 1
Glyph name: s	Contours detected: 4	Expected: 1
Glyph name: u	Contours detected: 2	Expected: 1
Glyph name: w	Contours detected: 2	Expected: 1
Glyph name: braceleft	Contours detected: 3	Expected: 1
Glyph name: braceright	Contours detected: 3	Expected: 1
Glyph name: asciitilde	Contours detected: 2	Expected: 1
Glyph name: C	Contours detected: 3	Expected: 1
Glyph name: D	Contours detected: 1	Expected: 2
Glyph name: E	Contours detected: 4	Expected: 1
Glyph name: G	Contours detected: 2	Expected: 1
Glyph name: L	Contours detected: 2	Expected: 1
Glyph name: Q	Contours detected: 1	Expected: 2
Glyph name: S	Contours detected: 3	Expected: 1
Glyph name: W	Contours detected: 3	Expected: 1 or 2
Glyph name: ampersand	Contours detected: 4	Expected: 1, 2 or 3
Glyph name: asciitilde	Contours detected: 2	Expected: 1
Glyph name: asterisk	Contours detected: 2	Expected: 1 or 4
Glyph name: at	Contours detected: 4	Expected: 2
Glyph name: braceleft	Contours detected: 3	Expected: 1
Glyph name: braceright	Contours detected: 3	Expected: 1
Glyph name: bracketleft	Contours detected: 3	Expected: 1
Glyph name: bracketright	Contours detected: 3	Expected: 1
Glyph name: c	Contours detected: 3	Expected: 1
Glyph name: colon	Contours detected: 4	Expected: 2
Glyph name: comma	Contours detected: 2	Expected: 1
Glyph name: eight	Contours detected: 4	Expected: 3
Glyph name: f	Contours detected: 2	Expected: 1
Glyph name: five	Contours detected: 3	Expected: 1
Glyph name: h	Contours detected: 2	Expected: 1
Glyph name: m	Contours detected: 2	Expected: 1
Glyph name: n	Contours detected: 2	Expected: 1
Glyph name: one	Contours detected: 2	Expected: 1
Glyph name: parenleft	Contours detected: 3	Expected: 1
Glyph name: parenright	Contours detected: 3	Expected: 1
Glyph name: period	Contours detected: 2	Expected: 1
Glyph name: question	Contours detected: 3	Expected: 2
Glyph name: r	Contours detected: 2	Expected: 1
Glyph name: s	Contours detected: 4	Expected: 1
Glyph name: semicolon	Contours detected: 4	Expected: 2
Glyph name: seven	Contours detected: 2	Expected: 1
Glyph name: three	Contours detected: 4	Expected: 1
Glyph name: u	Contours detected: 2	Expected: 1
Glyph name: w	Contours detected: 2	Expected: 1 [code: contour-count]

</details>
<details>
<summary>⚠ <b>WARN:</b> Does GPOS table have kerning information?</summary>

* [com.google.fonts/check/gpos_kerning_info](https://font-bakery.readthedocs.io/en/latest/fontbakery/profiles/gpos.html#com.google.fonts/check/gpos_kerning_info)

* ⚠ **WARN** GPOS table lacks kerning information. [code: lacks-kern-info]

</details>
<br>
</details>

### Summary

| 💔 ERROR | 🔥 FAIL | ⚠ WARN | 💤 SKIP | ℹ INFO | 🍞 PASS | 🔎 DEBUG |
|:-----:|:----:|:----:|:----:|:----:|:----:|:----:|
| 4 | 7 | 10 | 174 | 10 | 143 | 0 |
| 1% | 2% | 3% | 50% | 3% | 41% | 0% |

**Note:** The following loglevels were omitted in this report:
* **SKIP**
* **INFO**
* **PASS**
* **DEBUG**
