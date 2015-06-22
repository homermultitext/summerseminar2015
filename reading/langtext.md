---
title: From language to digital text
layout: page
---

## Introductory note
Key points to understand after reading this section
For any digital text, you must be able to identify its
- language
- writing system
- character set and character encoding

## Language and writing systems
Language is a uniquely human form of expression and communication.
At different times in the past 5,000 years or so, in a number of cultures, systems for expressing language in writing have evolved or been invented. No writing system simply records spoken language: speech captured in written form always involves translating spoken language into the conventions of a writing system. Modern English orthography, for example, cannot indicate patterns of tone or inflection that can be very meaningful in spoken English. By the same token, in literate cultures, literary expressions composed in writing for reading can express information or ideas that are impossible to capture in speech. (Visual poetry, in which the spatial arrangement of text on a page is an important part of the composition, is an extreme case; a simpler example would be written conventions that unambiguously distinguish homophones that can only be disambiguated in speech by inference from context.)

Since reading any text therefore requires us to understand both its language (possibly including a more specific dialectical variant) and its writing system, we should explicitly identify both of those features of any text we edit or study. The Greek alphabet used in Ionia in the fifth century BCE is the direct ancestor of the modern Greek alphabet. The letter eta represented a vowel, the long version of the short vowel written with the letter epsilon. In Athens, on the other hand, a local Athenian alphabet was used for most of the fifth century BCE. The Attic alphabet included a glyph essentially identical in appearance to the Ionic eta, but it represented a consonant, pronounced like a modern English H (or like the “rough breathing” in modern writing of ancient Attic). In 403 BC, the Athenians voted to adopt the Ionic alphabet as their official writing system. The language spoken in Athens did not change, but the writing system did: any reader (or any computer program) that tries to interpret a text written in the “old Attic” alphabet as though it were written in the modern, Ionic alphabet will fail spectacularly, even though the language is unchanged.

[Note: our sources for dating this event to the archonship of Euclid in 403/402 BCE include the Suda, sigma, 77, headword Σαμίων ὁ δῆμος. There are good cross references in the Suda Onlne translation and commentary on this passage to other sources for this episode.]

## Types of writing systems
Broadly speaking, writing systems can be categorized into three main types.
*Ideographic* writing systems use single signs to represent a concept or entire word. *Syllabic* writing systems spell language out phonetically, using individual signs to represent an entire syllable. *Alphabetic* systems spell language out phonetically, using individual signs to represent discrete sounds (vowels or consonants).

Many historical writing systems combine features of these primary systems with each other, and with other kinds of written symbols.
For example: in Akkadian cuneiform, a word might be indicated by a Sumerogram (that is, a sign representing a word or concept not in Akkadian, but in Sumerian) completed by a phonetically spelled Akkadian ending. Qualifying signs may add further “markup,” or information that is not articulated in the vocalization of the text, e.g., that a word identifies a divinity or a human figure, or that a given word is in the plural. Traditionally, when Assyriologists publish texts, they clearly distinguish between *transliteration* — a sign-by-sign reading of what the writing system represents — and *transcription* — a reading, in the original language, of the continuous text of what the writing system represents.

## Digital texts
Before the twentieth century CE, all written texts shared an essential property: elements of the writing system were encoded visually, and could only be processed by human readers.

Digital texts are different. A text might be presented visually in some specific medium (large-format computer screen, cell-phone display, or letter-sized paper printout), or it might not (e.g., a text might be processed for speech output, or it might be processed for some kind of analysis without any visual or aural output). In any case, digitized versions of written texts add a further layer of representation. Symbols in a given writing system are encoded as a cluster of binary oppositions — physically, by phenomena such as low voltage/high voltage (off/on) or positive/negative magnetic charge. More abstractly, we conventionally represent the two possible values of a binary opposition as 0/1.

A single binary unit can have either one of two possible values. When two binary units are combined, the first can have either of two possible values, and so can the second. This yields a total of four possible combinations:

    00 
    01 
    10 
    11

We could choose to let these four combinations of values stand for anything we like.  “North, South, East and West,” “Conquest, War, Famine, and Death” or “Porthos, Athos, Aramis and D'Artagnan” would all work equally well. Often, it can be helpful to think of the combinations of values as binary numbers or digits. (From the term binary digit, computer scientists derive the more concise punning term "bit".) Two binary digits can represent four different values; three bits can yield eight combinations representing eight values, as illustrated here:


	0 0 0
	0 0 1
	0 1 0
	0 1 1
	1 0 0
	1 1 0
	1 1 1
	

In general, n digits can represent 2^n values, so four bits can represent 16 values, five bits can represent 32 values and 6 bits can represent 64 values, etc.
If you know how many distinct symbols are in your writing system, it's not difficult to figure out how many bits you need to encode that number of distinct values. In the 1960s, the first major effort to define a standard set of binary values to represent a writing system was the ASCII standard — the American Standard Code for Information Interchange. ASCII defines values for 7 bits of data, so (since 2^7 = 128) a total of 128 values. One hundred twenty-eight characters was enough for 26 uppercase letters, 26 separate lowercase letters, punctuation marks like the question mark, comma, period, brackets and parentheses, and a few other odds and ends. Significantly, the ASCII standard made it possible to exchange data across computer systems (where before ASCII, different manufacturers might each have used an idiosyncratic set of binary values to represent the same set of characters).

ASCII really worked well only for American English: it includes no European accented characters, and no non-Latin alphabets. The public opening of the internet in the 1990s made it essential to have better standards for other writing systems, and led to development of the Unicode standard: a project aiming to define standard codes (which could be expressed as binary digits) for every character in every known writing system. Standard writers initially fell into the trap of defining a fixed size for all characters.  They used 16 bits, and since that yields the large number of 65536 possible combinations, they naïvely believed they would never need more than 16 bits.  Just a few years later, 65536 proved woefully inadequate for Unicode's needs.   Today's definition of Unicode is open-ended, and currently includes definitions for nearly 100,000 characters. Some computer users still suffer from the consequences of the original Unicode definition, however. Microsoft's operating systems do not automatically support Unicode characters beyond the first sixteen bits, for example, and programming languages like Java require extra effort to work with characters beyond this limit. (The set of Unicode's first 65536 characters is known as the “Basic Multilingual Plane.”) In 2011, Unicode is the single character set that editors of digital texts should be working with.

The way that the characters in the Unicode character set are represented on a specific computer system is called the *character encoding*. The most flexible and in many ways most convenient character encoding for Unicode is called UTF-8 (for Universal character set Transformation Format, 8 bits). It groups bits into clusters of eight, and uses from one to four clusters to represent a character. To completely specify how your digital text is encoded, you need to know: its language, its writing system, the character set (Unicode), and the character encoding (preferably UTF-8).

# Questions and exercises : ancient Greek in digital texts
1. The Library of Congress is the registrar for three-letter codes defined by the International Standards Organizations (ISO) to identify languages. You can see a complete list of codes from the ISO 639-2 standard at [this address](http://www.loc.gov/standards/iso639-2/php/code_list.php).  Find the abbreviations for all forms of Greek that are recognized by the International Standards Organization.
2. SIL is the registrar of a current initiative to expand ISO 639. See tables with the [current list of codes](http://www.sil.org/iso639-3/codes.asp).
3. Use this searchable web site to look up Unicode characters:
[http://unicodelookup.com/](http://unicodelookup.com/)
Search for “koppa”; search for “sigma.” Can you explain the results?
4. Classicists were involved with editing and analyzing digital texts long before the Unicode standard was developed. Before Unicode, one widely used approach to encoding ancient Greek, was to use the ASCII character set, but following a transcription scheme that equates ASCII characters with Greek characters..
See the table summarizing the beta code transcription in the wikipedia article [Beta code](http://en.wikipedia.org/wiki/Beta_code).

For a given digital text, if you know the language, writing system, character set and character encoding, is there any way you could tell if the text was represented in a "transcription" or "native"" version of the character set? How, for example, could you distinguish between a Greek text using the native Greek alphabet as defined in Unicode from the same text represented with Beta code (which would use only the Latin alphabet section of Unicode)?
￼