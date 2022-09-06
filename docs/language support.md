# Language Support

Original Release (Super Famicom)

- Original Japanese Release from 1995

Collection of Mana / Seiken Densetsu Collection (Nintendo Switch)

- Japanese Release from 2017
- International Release from 2019 (English, French, German, Spanish)

Fan Translations

- English Translation V1.01 by Neill Corlett, SoM2Freak
- French Translation RC1 by Terminus Traduction (Copernic)
- German Translation V1.00 RC3 to V3.0 by G-Trans (Special-Man, LavosSpawn)
- Italian Translation V1.00b by Mumble Translations (Clomax, Ombra, Chester)
- Spanish Translation V1.03 by Magno, Vegetal Gibber

## Automatic Language Detection

The filename is being used to determine the translation patch. Unfortunately, there is no way to detect the translation patch from the save file data directly, so the filename has to suffice.

Please refer to the source code for the actual regular expressions.

### Detection Order

1. Original Japanese ROM name without any translation information (Japanese)

    | | |
    | ---| --- |
    | **Japanese** | Seiken Densetsu 3 (J) <br/> Seiken Densetsu 3 (Japan) |

2. Switch release (Japanese, Multilingual)

    | | |
    | ---| --- |
    | **Japanese** | Seiken Densetsu 3 (J) (Seiken Densetsu Collection) <br/> Seiken Densetsu 3 (Japan) (Seiken Densetsu Collection) |
    | **Multilingual** | Trials of Mana (W) <br/> Trials of Mana (World) <br/> Trials of Mana (W) (Collection of Mana) <br/> Trials of Mana (World) (Collection of Mana) |

    Looking for “Trials of Mana”, “Collection of Mana” and “Seiken Densetsu Collection”.

3. Patch name (English, French, German, Italian, Spanish, incl. Japanese)

    | | |
    | ---| --- |
    | **English** | SD3EN101.IPS |
    | **French** | SEIKEN3F.IPS |
    | **German** | SEIKEN3D.IPS <br/> SD3GER203.IPS <br/> SD3DE30.IPS |
    | **Italian** | SD3_JAP_ITA_V100_BETA_6A93E9F.IPS <br/> SD3_ENG_ITA_V100_BETA_6A93E9F.IPS |
    | **Spanish** | SOM2SP.IPS |

    So, either one of `SD3` or `SOM2` or `SEIKEN3`, followed by a one to three letter language code, followed by an optional version number.

    Only Italian differs from this pattern slightly.

4. Translator / translation team (English, French, German, Italian, Spanish)

    | | |
    | ---| --- |
    | **English** | Neill Corlett, SoM2Freak |
    | **French** | Terminus Traduction, Copernic |
    | **German** | G-Trans, Special-Man, LavosSpawn |
    | **Italian** | Mumble Translations, Clomax, Ombra, Chester |
    | **Spanish** | Magno, Vegetal Gibber |

5. Language / language code (English, French, German, Italian, Spanish, incl. Japanese)

    | | |
    | ---| --- |
    | **English** | en, eng, english |
    | **French** | fr, fra, fre, french, français, francais |
    | **German** | de, deu, ger, german, deutsch |
    | **Italian** | it, ita, italian, italiano |
    | **Japanese** | ja, jp, jap, japanese |
    | **Spanish** | es, sp, esp, spa, spanish, español, espanol, castellano |

    Only two and three letter language codes are taken into account here, no single letter codes.

6. Fallback to English

### Remarks

- File names are treated case-insensitive.
- There is also a pre-patched ROM circulating named `Seiken Densetsu 3 (Japan) [En by LNF+Neill Corlett+SoM2Freak v1.01]`. This is covered by rule 4 and 5.
- The mere name `SEIKEN3` does not provide enough information to determine the language. Most likely it will be English. In any case, according to the above rule-set, the last rule will apply with English as fallback.

## UI Changes

When loading a save file, the program will automatically try to determine the used translation patch. In addition, you can also select the translation patch manually from the combo box at the top.

If you change the translation patch after having loaded a save file, the current player names will automatically be mapped to the new encoding, thus, leading to a possible drop of unsupported characters. If this happens, just load the save file again.

Also, the program will check for unsupported characters on input, which means you can only enter valid characters from the currently selected translation patch. Although, most ASCII characters are present in all language encodings.

For compatibility both half-width and full-width characters are supported.

A player's name is limited to a maximum length of 6 characters for the Japanese release and all translation patches based on it. Only the multilingual release from the Collection of Mana allows a maximum length of 12 characters.

## Regarding the Nintendo Switch Release

In 2017 the Seiken Densetsu Collection was released that had an identical copy of the original Seiken Densetsu 3 release. As such, this version uses the exact same encoding scheme, and it will be auto-detected as the original Japanese release.

In 2019 the Collection of Mana was released internationally. For the first time, it offered official translations for English, French, German and Spanish, but neither Italian nor any other language if you so will ;) Besides a newly translated script, some character names, location and item names were also changed. Whichever translation you prefer, is up to you. Although, I have to admit that the German translation from G-Trans is pretty darn awesome, hehe.

The biggest difference, however, is the character encoding. The multilingual version uses the same character set for all aforementioned languages, which is basically identical to Latin-1. Because it uses a single byte encoding, player names can be twice as long, allowing for up to 12 characters!

**Experimental.** Because there are some encoding issues regarding quotation marks, an alternative translation patch option with a fix is offered. Normally, the single and the double quotation mark from the ASCII range appear as typographical ones in-game. However, the character set also does have the normal straight ones in its repertoire. The fix makes it so, that you can use both straight and typographical quotation marks alongside for your character names. So only the single and the double quotation marks from the ASCII range are transformed, and the typographical quotation marks from outside the ASCII range are unaffected from this fix.

## Remarks

There are currently two encoding files to choose from when converting from Japanese to Unicode: One with full-width encoding in Unicode and the other one with half-width encoding in Unicode. Both work equally well, and the only effect it has the visual presentation in the text input box. For now I went with full-width.

You can change this by simply overwriting `encoding_japanese_to_unicode.json` with either `encoding_japanese_to_unicode_halfwidth.json` or `encoding_japanese_to_unicode_fullwidth.json`.

This said, when converting from Unicode to Japanese, both half-width and full-width characters are encoded properly.

## Known Issues

- The Italian and the Spanish cartridge encoding both have a codepoint for the double L (ll). However, there is no according Unicode codepoint for it.

- The multilingual encoding has multiple conflicting codepoints for quotation marks.

