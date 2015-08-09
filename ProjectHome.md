## Welcome to Flying Saucer ##
Flying Saucer takes XML or XHTML and applies CSS 2.1-compliant stylesheets to it, in order to render to PDF (via iText), images, and on-screen using Swing or SWT. The library implements (basically) the entirety of CSS 2.1 and aims to be fully compliant with the W3C specification; it includes a small handful of CSS 3 features.

The source code is hosted on GitHub, here: http://github.com/flyingsaucerproject/flyingsaucer

We're even in the [Wikipedia](http://en.wikipedia.org/wiki/Flying_Saucer_(library))!

## Great! How do I get Started? ##

Check out our **[User's Guide](http://flyingsaucerproject.github.com/flyingsaucer/r8/guide/users-guide-R8.html)** (also available as downloadable [pdf](http://flying-saucer.googlecode.com/files/flyingsaucer-R8-users-guide.pdf)), our [mailing list archives on Mark Mail](http://markmail.org/search/?q=list:net.java.dev.xhtmlrenderer.users) and our [FAQ](FAQ.md).

There are also some older articles which may have slightly out-of-date information
  * [Generating PDFs for Fun and Profit with Flying Saucer and iText](http://today.java.net/pub/a/today/2007/06/26/generating-pdfs-with-flying-saucer-and-itext.html), by Josh Marinacci from June 2007. Josh covers using Flying Saucer to generate PDF documents.
  * [Combine JSF Facelets and the Flying Saucer XHTML Renderer](http://today.java.net/pub/a/today/2006/10/31/combine-facelets-and-flying-saucer-renderer.html) by Jacobus Steenkamp from October 2006. Jacobus covers using Flying Saucer to generate PDF, image and SVG output, with a focus on on-the-fly generation.

### Supported Features in CSS 2.1 ###

Flying Saucer supports all of CSS 2.1 with a few exceptions. Consult the [issue tracker](http://code.google.com/p/flying-saucer/issues/list) for more information on what is not supported (in particular, the issues with a summary of "Support ...") or ask on the [online discussion group](http://groups.google.com/group/flying-saucer-users). If you do encounter a compliance bug or other unexpected behavior, please open a bug or post to the [online discussion group](http://groups.google.com/group/flying-saucer-users).

Features:
  * 100% Java XML+CSS layout engine with native PDF, Swing, image rendering.
  * Strong support for the CSS 2.1 specification including extensions to better support paged media.
  * Good performance.
  * Support for XHTML including forms.
  * Arbitrary elements may be replaced with custom content.
  * Limited support for dynamic effects (for example, the :hover pseudo-class and links)
  * Some support for PDF specific features (for example, bookmarks and internal links). More coming soon.Limitations:
  * Resource loading is single threaded and occurs inline with layout.
  * Support for XHTML is weaker than XML+CSS (for example, not all XHTML presentational attributes are supported nor are X/HTML features like the `<object>` element).
  * No support for legacy HTML (although there are several open source Java HTML cleaners of varying quality available).
  * No support for incremental layout (applies to screen media only). 

## Where is the Code? ##
[Get the source here](http://github.com/flyingsaucerproject/flyingsaucer).

**Our source code is hosted on GitHub** as we've decided that we prefer Git for collaborative code development, and would like our users to take advantage of the freedom that a DVCS has to offer. **This Google Code project has no source code**. Go to our GitHub project if you would like the current sources or would like to fork or branch the project for your own purposes.

From the project's inception in 2004 until April 2010, it was hosted on java.net. We decided in 2010 to move the project to Google Code.


## Mailing List Archives ##
Flying Saucer was launched in 2004 - there is quite a bit of useful information available on our mailing lists, in the archives. We recommend you use [Mark Mail](http://markmail.org/search/?q=list:net.java.dev.xhtmlrenderer.users) - include `list:net.java.dev.xhtmlrenderer.users` to restrict queries to our old user's mailing list.

Our new, ongoing discussions are carried out in our [online discussion group](http://groups.google.com/group/flying-saucer-users).

## Special Thanks to... ##

Our User's Guide (and our prior project website) are produced using the [Xilize](http://xilize.sourceforge.net) syntax and rendering engine. The content is written in Xilize text markup, then converted to XHTML using the Xilize converter. We'd like to thank the Xilize team at CenteredWork for sharing this library. Try it out! It's a great way to write websites quickly, without losing control over formatting. Check it out!

[JetBrains](http://www.jetbrains.com), the makers of IntelliJ IDEA, has generously sponsored a license letting us use IDEA on this project under their Open Source Program. We are grateful for their support!


## External Resources ##

The Specs:
  1. W3C XHTML specification
  1. CSS 2.1 Specification (exhaustive but precise)

Libraries
  1. [iText](http://itextpdf.com/): for generating PDF files
  1. [JTidy](http://jtidy.sourceforge.net/): can be used for "cleaning up" legacy HTML
  1. [TagSoup](http://ccil.org/~cowan/XML/tagsoup/): can be used for "cleaning up" legacy HTML