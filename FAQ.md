# Flying Saucer Project: FAQ #

This is our list of frequently-asked questions. For a more comprehensive guide, see our User's Guide. Please contact us on our mailing list if you have more questions.

  1. [General Questions](#General_Questions.md)
  1. [General Usage Questions](#General_Usage_Questions.md)
  1. [Swing-specific Questions](FAQSwing.md)
  1. [PDF-specific Questions](FAQPDF.md)

## General Questions ##
  1. [What is Flying Saucer?](#What_is_Flying_Saucer?.md)
  1. [Wait a second! XML, XHTML, get your story straight!](#Wait_a_second!_XML,_XHTML,_get_your_story_straight!.md)
  1. [Does Flying Saucer support legacy HTML?](#Does_Flying_Saucer_support_legacy_HTML?.md)
  1. [Can I use Flying Saucer to browse websites?](#Can_I_use_Flying_Saucer_to_browse_websites?.md)
  1. [Is Flying Saucer a web browser?](#Is_Flying_Saucer_a_web_browser?.md)
  1. [What kind of applications can I use Flying Saucer for?](#What_kind_of_applications_can_I_use_Flying_Saucer_for?.md)
  1. [What XHTML/CSS features does Flying Saucer currently support?](#What_XHTML/CSS_features_does_Flying_Saucer_currently_support?.md)
  1. [What XHTML/CSS features is Flying Saucer missing?](#What_XHTML/CSS_features_is_Flying_Saucer_missing?.md)
  1. [So do you pass the Acid(2) test?](#So_do_you_pass_the_Acid(2)_test?.md)
  1. [Where can I find API specification for the project?](#Where_can_I_find_API_specification_for_the_project?.md)

### What is Flying Saucer? ###
Flying Saucer is an XHTML renderer written in Java. It's 100% Java, not a native wrapper, and it only handles well-formed XHTML + CSS. It is intended for embedding web-based user interfaces into Java applications (ex. web photo album generator, help viewer, iTunes Music Store clone). It cannot be used as a general purpose web browser since it does not support the malformed legacy HTML found on the web, though recent work on compatibility libraries may be enough to do what you need. You may be able to work with legacy HTML (e.g. HTML that is not well-formed XML) by using a pre-processor that cleans it up; there are several of these, including [JTidy](http://jtidy.sourceforge.net/) and [TagSoup](http://ccil.org/~cowan/XML/tagsoup/). See our User's Guide for details.

### Wait a second! XML, XHTML, get your story straight! ###
Flying Saucer takes well-formed XML (or a DOM Document) as input, matches it with CSS (linked, inline, attributed) and renders it. That XML could, for example, be XHTML (strict). We figure most of you are interested in rendering some form of XHTML, so in these docs we use "XHTML" as short for "well-formed XML, for example, XHTML (strict)".You can render any XML, in fact, as long as you have CSS for it. For XHTML, we have out-of-the-box default CSS styling; for any other XML, you'll need to bring your own.

### Does Flying Saucer support legacy HTML? ###

### Can I use Flying Saucer to browse websites? ###
Flying Saucer is not an HTML component. It is a rendering component for XHTML content, but it cannot handle the malformed HTML 4.0 of general webpages, and it has no support for purely stylistic markup like FONT and CENTER. You have to use valid XHTML and CSS. For most embedded uses this is fine since the application author usually has control over the documents to be loaded. If you really need full IE/Mozilla/Safari-like fidelity for general purpose webpages you should look into a commercial component like [WebRenderer](http://www.webrenderer.com). Sun's/Oracle's Swing team has said in the past few years that they are working on a Java wrapper for WebKit called JWebPane, but there is no release schedule announced so far.

### Is Flying Saucer a web browser? ###
The core renderer just handles XHTML and CSS. It doesn't know anything about form submission, managing cookies, or tracking the browsing history. It just renders XHTML/CSS to the screen. However, Flying Saucer does include a (very simple) Browser application which shows how you might develop these features yourself. You can use this as a good starting point for your own applications.

### What kind of applications can I use Flying Saucer for? ###
Flying Saucer can be used for any Java application that requires some sort of styled content, to generate high-quality PDF output based on XHTML and CSS documents, or to layout and render images based on XHTML and CSS.An application using Flying Saucer can be as simple as a chat program or as complicated as a complete ebook reader with dynamic stylesheets. Flying Saucer is very forward- thinking and is designed to be a part of the next generation of applications that combine rich desktop clients with web content. Some examples of application types are:
  * chat programs
  * online music stores
  * a Gutenberg eBook reader
  * a distributed dictionary application
  * Sherlock style map and movie search
  * Konfabulator and Dashboard components
  * an RSS reader
  * a Friendster client
  * an eBay client
  * a splash screen
  * an about box
  * a helpfile viewer
  * a javadoc viewer
  * report generation and viewing
  * a stock ticker / weather reporter

Flying Saucer has become a favorite recently for people who need to render clean XHTML to PDF; we support PDF output via the iText library.

### What XHTML/CSS features does Flying Saucer currently support? ###
Flying Saucer supports all of CSS 2.1 with a few exceptions. Consult the [issue tracker](https://xhtmlrenderer.dev.java.net/servlets/ProjectIssues) for more information on what is not supported (in particular, the issues with a summary of "Support ...") or ask on the [mailing list](https://xhtmlrenderer.dev.java.net/servlets/ProjectMailingListList).If you do encounter a compliance bug or other unexpected behavior, please open a bug or post to the [mailing list](https://xhtmlrenderer.dev.java.net/servlets/ProjectMailingListList). Our goal is 100% compliance with the CSS 2.1 specification.

### What XHTML/CSS features is Flying Saucer missing? ###
Check the [issue tracker](https://xhtmlrenderer.dev.java.net/servlets/ProjectIssues) for a list or ask on the [mailing list](https://xhtmlrenderer.dev.java.net/servlets/ProjectMailingListList) if you aren't sure.Among other things there is no support for things outside the scope of XHTML/CSS such as Javascript, Flash, or legacy HTML (though there is interest in all of those).

### So do you pass the Acid(2) test? ###
Our core developer in the [R7](https://code.google.com/p/flying-saucer/source/detail?r=7) development cycle, Pete Brant, reported that it was possible to render Acid2 pretty well, with some caveats. Quoting from him in the developer's email list

> Save for the changes below, test\_as\_xml.xml is an unmodified version of http://hixie.ch/tests/evil/acid/002-no-data/. All in all things are looking good! Changes to original test:

  1. Replace DOCTYPE with one we recognize to pick up entity references (in particular  )
  1. Wrap `<style>` tag in CDATA
  1. Close open tags as appropriate (in particular, `<p>` and table related tags in row 1 [referenced from the test guide](as.md), `<link>` in header, and bottom `<img>` (after row 14 in guide)
  1. Replace `<object data="data007">ERROR</object>` with `<img src="data007">ERROR</img>` (since we don't support HTML's `<object>` )
  1. Change CSS selector on line 55 from "#eyes-a object object object" to "#eyes-a object object img" to compensate for (4)
  1. Bottom `<img>` uses a data URL even in the non-data URL version (I assume it was just missed). Save data URL contents to disk (as data008) and update src attribute

> Of course, these changes mean that we cannot claim Acid2 compliance, but nothing there changes the nature of the test (at least as far as a CSS torture test goes). Besides those changes above, there are still the following compliance problems:

  1. The transparent pixels in the eyes row background(s) are painted as black. Weird considering that the alpha channel in the eyes graphic itself is apparently picked up fine.
  1. Hover doesn't work on generated content (hence no blue nose on mouseover)
  1. There shouldn't be a scroll bar on the page by virtue of @html { overflow: hidden; }

The resulting image is available on our project home page, as an Easter egg. See if you can find the little bandit.

### Where can I find API specification for the project? ###

JavaDoc for release 8 is available on our downloads page

http://code.google.com/p/flying-saucer/downloads/list

You should probably look at the "User" JavaDoc, which is a subset of the complete docs and is intended to document the classes of interest to end users.


## General Usage Questions ##
  1. [XML Parsing Errors: entity was referenced but not declared](#XML_Parsing_Errors_entity_was_referenced_but_not_declared.md)
  1. [Loading Documents from String Content](#Loading_Documents_from_String_Content.md)
  1. [How do I force Anti-aliasing?](#How_do_I_force_Anti-aliasing?.md)
  1. [How do I use the setDocument(...) constructor?](#How_do_I_use_the_setDocument(...)_constructor?.md)
  1. [Replacing Elements within the Document](#Replacing_Elements_within_the_Document.md)
  1. [Can I use Flying Saucer in an SWT application?](#Can_I_use_Flying_Saucer_in_an_SWT_application?.md)


### XML Parsing Errors entity was referenced but not declared ###

_I'm getting an error: The entity "ldquo" was referenced, but not declared'_

This is an XML-level problem, not to do with FS. You can't include entities like &ldquo; in your HTML without declaring them - the XML parser doesn't know what do to with them.

This has come up before, check our mail archives, for example
http://markmail.org/search/?q=list:net.java.dev.xhtmlrenderer.users+%22not+declared%22

One possible solution: add a DOCTYPE declaration at the top of the document
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```


### Loading Documents from String Content ###
> I have XML or XHTML stored in a Java String, not a file—how do I load this into an XHTMLPanel?

It's been tricky for us to come up with a decent set of method calls to cover initilizing the panel without creating tons of little methods.In Java APIs, there is some confusion on usage between a String that represents an address (like a URI or a file path) and strings that represent content. Our API tends to expect that Strings will represent addresses.You can use `panel.setDocumentFromString()` to render a document from a string containing XHTML content. The String will be passed to the standard XML parser and treated as a regular document.It's important to remember that FS expects well-formed XML documents, and we don't have an extremely friendly relationship with the XML parsers; it's always a good idea to test that your document can be loaded outside of FS, without error, using Java XML APIs, before loading them in FS. This is especially true if you are generating XHTML on-the-fly.

### How do I force Anti-aliasing? ###
Either
  * Set the appropriate configuration properties: `xr.text.aa-fontsize-threshhold`
  * Get the `Java2DTextRenderer` reference from the XHTMLPanel's `SharedContext` property, then call `setSmoothingThreshold()`The threshold is the font size at which AA should kick in, for text; font sizes below that size will **not** be drawn with AA. A threshold of -1 turns AA off completely.

Note that on some platforms and JREs, anti-aliasing can slow things down considerably. It appears to be much better with more recent Sun JREs, such as Java 6.

### How do I use the setDocument(...) constructor? ###
> When I use the `setDocument(dom, url)` constructor, what should the url parameter point to?
The url is the "base", which for a normal URL would be the parent location—the parent directory, or the location where the document you are rendering is located.If your document has absolute URIs for CSS and images, or it has no external references at all, then the base url can be null.If your document has any relative URIs for CSS or images, then the base URL should **not** be null, but rather should point to the directory or address where the current document is located.

### Replacing Elements within the Document ###
> I've created a replacedelementfactory for a custom XML element (e.g. MathML), but it's not getting replaced within the document.
Make sure the element has it's display style as inline-block or block. Only block-level elements can be replaced.

### Can I use Flying Saucer in an SWT application? ###
If you're trying to output to an SWT canvas—there is an early mockup by Vianney le Clément which was merged into the [R8](https://code.google.com/p/flying-saucer/source/detail?r=8) release. See the mailing list thread starting with:  https://xhtmlrenderer.dev.java.net/servlets/ReadMsg?listName=dev&msgNo=3452


## Developer's FAQ ##
  1. [How do I set up my CLASSPATH?](#xil_23.md)
  1. [How do I build XR without Ant?](#xil_24.md)
  1. [How do I build XR from within my IDE?](#xil_25.md)

### How do I set up my CLASSPATH? ###
You only need the
  * `core-renderer.jar`
  * `itext.jar`

The first two are required; iText is needed for PDF rendering.

In earlier releases, you needed to include a CSS parser in the CLASSPATH. This is no longer necessary, as Flying Saucer now includes a fast, compliant CSS parser.That is all you need for your own programs. You also need an XML parser to be in your classpath, but this already included in recent versions of the JRE.To run the browser or use any of it's support classes you will need the `browser.jar` file.

### How do I build XR without Ant? ###

### How do I build XR from within my IDE? ###
Our Ant `build.xml` file includes all JAR files in the `/lib` directory, plus the `/resources` directory tree in the classpath. The compile target also copies CSS and properties resources from `/src/css` and `src/conf` to `/build/resources`. If running from an IDE, you will need to synchronize this yourself.