## PDF Questions ##

  1. [Versions of iText Supported](#Versions_of_iText_Supported.md)
  1. [Watermarks in PDF](#Watermarks_in_PDF.md)
  1. [My PDF isn't picking up my CSS!](#My_PDF_isn't_picking_up_my_CSS!.md)
  1. [How can I print multiple pages on to one PDF, if they come from multiple documents?](#How_can_I_print_multiple_pages_on_to_one_PDF,_if_they_come_from_multiple_documents?.md)
  1. [My header is not showing up correctly in my PDF.](#My_header_is_not_showing_up_correctly_in_my_PDF..md)
  1. [How do I set a custom UserAgentCallback when generating PDF?](#How_do_I_set_a_custom_UserAgentCallback_when_generating_PDF?.md)
  1. [How can I set PDF document properties when generating a PDF?](#How_can_I_set_the_document_properties_when_generating_a_PDF?.md)
  1. [What about PDF bookmarks?](#What_about_PDF_bookmarks?.md)

### Versions of iText Supported ###

Release 8 supports version 2.x of iText, was shipped with 2.0.8 and we have users who report using 2.1.7; we believe 2.1.7 should be more or less identical to 4.2.0.

For iText 5.x support, we do have a contributed itext5 branch on GitHub though for anybody using iText 5+.  The changes were mostly just package renames along with a couple of other tweaks.  We keep the itext5 branch in sync with master so it should always be current.

### Watermarks in PDF ###
> How can I "watermark" PDF's created through FS?
Either use the background property inside of `@page` or `PdfStamper` after the PDF is already created. `PdfStamper` is part of the iText API.

### My PDF isn't picking up my CSS! ###
PDF is treated as "print" media; see the [CSS 2.1 specification section on media types](http://www.w3.org/TR/CSS21/media.html). Make sure you have specified the media type for your CSS when you link or embed it; use type "print" or "all".

### How can I print multiple pages on to one PDF, if they come from multiple documents? ###
For the first document in the set (e.g. starting with the first page in the PDF you want to render) take an ITextRenderer and call `setDocument()`, `layout()` and `createPDF()`; for each subsequent document, use the same renderer and call `setDocument()`, `layout()`, and `writeNextDocument()`. Call `finishPDF()` to complete the process. A sample follows below; a cleaned-up example, `PDFRenderToMultiplePages`, is in our demos/samples directory in our source distribution.

```
String root = "J:/Temp/fs"; 
String[] inputs = new String[] { "input1.html", "input2.html", "input3.html" }; 
String output = "output.pdf"; 
OutputStream os = null; 
try { 
   os = new FileOutputStream(new File(root, output));    
  ITextRenderer renderer = new ITextRenderer();    
  renderer.setDocument(new File(root, inputs[0]));    
  renderer.layout();    
  renderer.createPDF(os, false);    
  for (int i = 1; i < inputs.length; i++)    {
        renderer.setDocument(new File(root, inputs[i]));
        renderer.layout();
        renderer.writeNextDocument();
    }
    renderer.finishPDF();
    os.close();
    os = null;
 } finally {
    if (os != null)    {
        try        {
            os.close();
        } catch (IOException e)        {
            // ignore
        }
    }
 }
```


### My header is not showing up correctly in my PDF. ###
The values of `-fs-flow-top/right/bottom/left` and `-fs-move-to-flow` must  be strings and not keywords (e.g. `-fs-flow-top: 'header'` instead of `-fs-flow-top: header` ).The new CSS parser validates this (and will give you a warning message if you have logging turned on).


### How do I set a custom UserAgentCallback when generating PDF? ###
```
ITextRenderer renderer = new ITextRenderer(); 
ITextUserAgent callback = new ITextUserAgent(renderer.getOutputDevice());
callback.setSharedContext(renderer.getSharedContext()); renderer.getSharedContext().setUserAgentCallback(callback); 
renderer.setDocument(url); 
renderer.layout(); 
renderer.createPDF(os); 
```


### How can I set the document properties when generating a PDF? ###
You can set a PDFCreationListener on your ITextRenderer instance to do
whatever you want with the PDF either before the iText document is
opened or right before it's about to be closed.

### What about PDF bookmarks? ###
See [HowTo\_PDF\_bookmarks\_from\_xhtml\_markup](HowTo_PDF_bookmarks_from_xhtml_markup.md) for more information.

### Embedding fonts using CSS `@font-face` ###
You can embed custom fonts via CSS. Make sure the path to the font file is relative to the path of the CSS file.

```
@font-face {
	font-family: "UbuntuMono";
	src: url("UbuntuMono-R.ttf");
	-fs-pdf-font-embed: embed;
	-fs-pdf-font-encoding: Identity-H; 
}

* {
	font-family: "UbuntuMono";
}
```