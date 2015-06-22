---
title: XML Markup 
layout: page
---

The [previous reading selection](../langtext) looked at how a digital text represents languages and writing systems with digital character sets using a particular character encoding system. In addition to their writing system, written texts routinely include other information about a text through visual conventions. In printed English texts, for example, a reference to the title of a book is normally written in italics, and the title of an article is surrounded by quotation marks. Within a book, the title of a chapter within a book might be set off in some way (perhaps dropped lower on the page, centered, in a very large or distinct font). Editors of print editions typically expand on these conventions with explicitly defined use of brackets or other notation.

In the second half of the twentieth century, the most important system of of editorial brackets is the “Leiden conventions.” See the wikipedia article [Leiden_Conventions](http://en.wikipedia.org/wiki/Leiden_Conventions) for a summary.

Human beings learn to process this meta-information as they learn to read, and are adept at using contextual hints to interpret the information implicit in visual formatting. One of the most important principles of editing digital texts might therefore come as a surprise:

>you should never use visual formatting to encode information about a text

One of the most profound differences between a digital text and a text in any analog medium (print, manuscript, inscription or anything else), is that the editor of a digital text can separate decisions about visual presentation of a text from decisions about what a text means. In editing a text, we might explicitly indicate that a group of words represents the title of a book; we could later decide how to format book titles (as italicized, in a special font, or in any other way) without touching the source text.
This fundamental difference between digital and analog texts is important for several reasons. First, visual conventions are inevitably fuzzy or ambiguous. In addition to representing titles of books, for example, italics might be used to mark words in a foreign language, or to mark a speaker's surprise or emphasis. Humans do pretty well at disambiguating these overlapping uses, but how should an editor represent a foreign-language word in a title, for example? What if an emphatic exclamation includes a reference to a book title? In a foreign language? Citing a title of a book? “Do you mean, he has never read Römer's *Zu Aristarch und den Aristonicus-scholien der Odyssee*??” If we have separately encoded titles, foreign-language expressions and emphasized text, we could automatically identify that *Odyssee*, in German, is a title of a work within the longer German title of a book by Römer. That's significant if we wanted to do something like automatically extract or index occurrences of titles within a long text.

A second, closely related reason, is that editors of digital texts have to design their work to function with *any* kind of automated processing — not just one program used to generate a print edition or series of web pages. Scholarly editions are time-consuming to produce, and the number of scholarly editors is too small to justify redoing an edition. Digital editions must therefore specify the semantics of a text explicitly and unambiguously: visual formatting is implicit and ambiguous.

A third reason to prefer explicitly indicating the semantics of a text is that, as we shall see momentarily, the technologies for textual markup work with simple text formats that integrate easily with other essential functions we shall consider later in this seminar (specifically, version control systems to manage multiple versions of a single text, and build systems to manage collections of multiple texts).

From the tradition of an editor annotating a print copy, we refer to the addition of explicit information￼ about structure and semantics of a digital text as markup. Textual markup uses the same characters that are used for the text, but follows rules that allow us (or our software) to distinguish between text content and markup. The virtually universally used system for marking up a text today is the eXtensible Markup Language, or XML. In XML, pointed brackets enclose markup: text outside of enclosing pointed brackets is the text content of a document. If you've ever peeked behind a web page, you've seen an example of this. Most web browsers offer an option to “View source” (or similar phrase), that lets you see the actual text content transmitted over the web to your browser when you request a page. Here are a few lines from the top of the web page at  `http://shot.holycross.edu/CHSsummer2011/`

    <html> <head>
      <meta charset="UTF-8"/>
      <title>CHS Summer seminar, 2011</title>
      ...
      </head>
      <body>
      <header>Homer Multitext Seminar, Summer 2011</header>
       ...
      <article>
      <h1>CHS Summer seminar, 2011</h1>
      <h2>Schedule</h2>

The string of text `<title>` is markup (since it's between pointed brackets); the phrase “CHS Summer seminar, 2011,” on the other hand, is textual content. Your browser will normally use the markup information to decide to place the title text in the title bar of your window, rather than in the main content area. Similarly, the string `<h1>` is markup telling your browser that the next text is a level-1 heading. In laying out the page for you to read, your browser will normally draw that heading text more prominently than other text on the page. Let's turn now to a quick over of XML syntax.

>Question to consider: Why is XML's text-only format well suited to the scholarly goals of long-lived archival versions of digital editions?

##XML basics
XML grew out of experience with its ancestor, the Standard Generalized Markup Language. The main limitations of XML are very deliberate choices to make XML more practical to work with than SGML.

The contents of an XML document fall into the following distinct categories, which an XML editor like oXygen or JEdit will typically display in easily distinguished forms (e.g., using different colors):

Elements
:  Elements are the heart of an XML document. They describe the document's semantics. In XML, every element has an explicit beginning and ending. Syntactically, the beginning of the element is given by the name contained within angle brackets. (Note that this means that angle brackets are metacharacters that will need to be specially indicated in the text content of your XML document.) The end of an element is indicated by its name preceded by </ and followed by >. 

Example: the following well-formed XML consists of a single element called “p”:

    <p>One paragraph of text contained within an element “p”.</p> 

Attributes
: Attributes provide further information about a specific element. Syntactically, they are placed within the opening tag of an element and have the form attribute=”value”. 

The following example includes an element named “p” with an attribute “n” giving a name or number value for that specific element. Note that the end tag for the element retains the basic form “p” and does not include any attributes.

    <p n=”2”>One paragraph of text contained within an element “p”.</p> 

Processing Instructions
: As the name suggests, processing instructions (or PIs, to XML acronymophiles) embed in a document instructions or, more properly, suggestions about how to process the document. Syntactically, the processing instruction is bracketed by the characters <? at the beginning and ?> at the end. (Conveniently, this means that if you are parsing an XML document, the angle bracket metacharacters separate out text content from both elements and PIs.)

Every XML document should include one PI in its first line:

    <?xml version="1.0" encoding="UTF-8"?>

This helps parsers with two crucial pieces of information: first, it indicates that the document can be parsed according to the definition of version 1.0 of XML; second, it says that the document's contents are represented in Unicode using the UTF-8 encoding.

You might occasionally see other PIs. An XML editor that uses Cascading Style Sheets to determine the visual formatting of an XML document might include a PI to help the software find a CSS file, as oXygen can do:

    <?xml-stylesheet type="text/css" href="editing.css"?>
    
For scholars working on an archival edition of a text, however, you should not find yourself adding PIs to your document, since one of your goals is precisely to create an edition that is not dependent on any particular piece of software.

Comments
: Comments are *not* part of your document's content. They are addressed to other human editors, and may be thrown out by automated parsers. You can use comments to explain or clarify your use of markup to another editor. If you find that you need extensive comments in your edition, you may need to consider whether you should choose a different schema, or XML vocabulary, for your edition.

## Well-formed vs. valid XML documents
All XML documents must be what is technically termed “well-formed.” This means that the document obeys XML's general requirements: e.g., there will always be only one root element; except for the root element, all elements are fully contained within other elements; etc. A document can be well-formed regardless of whether or not its structure – that is, the arrangement of specific elements in relation to
one another - follows the rules of a particular schema. Only when those elements relate to one another properly as defined by the schema, with all required attributes and within the correct hierarchy, is the document considered valid.

One of the most important advantages of a markup language is that the structure can be verified automatically by a parser. In SGML, that structure was defined using a syntax called Document Type Definitions, or DTDs. You may still see DTDs in use to define the structure of XML documents today, but one of XML's improvements over SGML was that in XML it is possible to use other technological standards to define a document's structure.

Two widely used standards are XML Schema (a product of the WWW Consortium), and Relax NG. Relax NG is itself an XML language: documents defining an XML structure in Relax NG are XML documents following Relax NG's structure. If you need to invent your own document types, you would probably do well to use Relax NG to define its schema.

As an editor, you will always want to create documents that can be validated against a schema of some kind.

## Scholarly text editing: the Text Encoding Initiative
Given that XML is, by definition, extensible, what vocabulary should we use for editing scholarly texts? The main standard today is the Guidelines of the Text Encoding Initiative (TEI), now in version P5.

TEI's strength is also its weakness. The Guidelines try to offer suggested markup for every conceivable task of scholarly editing. For any one task the Guidelines sometimes offer multiple possibilities, among which editors may choose for the purposes of a particular project. They really are, in other words, guidelines, and not a strict technical standard. Be very cautious if someone naively asserts that documents from two different editors can easily be used together because both comply with the TEI Guidelines: there is plenty of room within the TEI for TEI-compliant texts to be incompatible in various ways.

For your initial work editing texts with TEI P5, have at hand the essential cha[pter 3 of the P5 Guidelines](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/CO.html).
This is the heart of TEI P5, and if you stick to material documented in this chapter, you'll be well on your way to creating TEI texts that really can be used with material from other editors.

The full contents of version P5 of the Text Encoding Initiative's Guidelines are [online here](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/index.html).
In addition to the table of contents, you may find the [index of all elements](http://www.tei-c.org/release/doc/tei-p5-doc/en/html/REF-ELEMENTS.html) in P5 helpful as you're working on a text.

￼￼￼
