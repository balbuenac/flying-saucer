#Use a CreationListener to read `meta` tags from a xhtml and embed the data into the resulting PDF.

# Introduction #
A PDF file can contain metadata. In most cases a xhtml document contains special `meta` tags in the `head` element. To transfer those meta data from the source xhtml to the target PDF one can use the `PDFCreationListener` interface (package ´org.xhtmlrenderer.pdf`).

In this case we will use the `DefaultPDFCreationListener` class which already implements the `PDFCreationListener` interface and overrides one of its methods.

# Details #
The following example is based upon code from Jesse Keller (jesse.keller@roche.com) and Patrick Wright (pdoubleya@gmail.com) in mailing list net.java.dev.xhtmlrenderer.users

Topic: Adding metadata (title, subject, author, creator) to a pdf document

Url: https://xhtmlrenderer.dev.java.net/servlets/ReadMsg?listName=users&msgNo=1897


Our new class `MetaDataCreationListener` will inherit from `DefaultPDFCreationListener`. We have two methods:

  * `public void parseMetaTags( Document sourceXHTML )`: This method reads the `title` tag and all `meta` tags from the `head` of our xhtml document and stores the values in a private field.
  * `public void preOpen( ITextRenderer iTextRenderer )`: This method overrides the base class' method. This method is called _before_ the PDF is created. Using the `ITextRenderer.getWriter()` getter we retrieve a `com.​lowagie.​text.​pdf.PdfWriter` instance. The call to `getInfo()` gives us a `com.​lowagie.​text.​pdf.PdfDictionary` object which we can fill with our data. There are some `PdfName`s predefined like `PdfName.AUTHOR` or `PdfName.KEYWORDS`. If we have additional meta data we want to include we just create custom fields with `new PdfName(key)`.


```
public class MetaDataCreationListener extends DefaultPDFCreationListener {

    Properties headMetaTags = new Properties();

    public void parseMetaTags(Document sourceXHTML) {
	//Could also use XPATH, I suppose.
	Element headTag = (Element) sourceXHTML.getDocumentElement()
					.getElementsByTagName("head")
					.item(0);
	NodeList metaTags = headTag.getElementsByTagName("meta");

	for (int i = 0; i < metaTags.getLength(); ++i) {
	    Element thisNode = (Element) metaTags.item(i);
	    String name = thisNode.getAttribute("name");
	    String content = thisNode.getAttribute("content");
	    if (name.length() != 0 && content.length() != 0) {
		this.headMetaTags.setProperty(name, content);
	    }
	}

	//No title meta tag given --> take it from title tag
	if ( this.headMetaTags.getProperty("title") == null ) {
	    Element titleTag = (Element)headTag.getElementsByTagName("title").item(0);
	    this.headMetaTags.setProperty("title", titleTag.getTextContent());
	}

	return;
    }

    @Override
    public void preOpen(ITextRenderer iTextRenderer) {
	Enumeration e = this.headMetaTags.propertyNames();
	
	while (e.hasMoreElements()) {
	    String key = (String) e.nextElement();
	    PdfString val = new PdfString(this.headMetaTags.getProperty(key), PdfObject.TEXT_UNICODE);
	    iTextRenderer.getWriter().setViewerPreferences(PdfWriter.DisplayDocTitle);
	    if (key == null ? "title" == null : key.equals("title")) {
		iTextRenderer.getWriter().getInfo().put(PdfName.TITLE, val);
	    } else if (key == null ? "author" == null : key.equals("author")) {
		iTextRenderer.getWriter().getInfo().put(PdfName.AUTHOR, val);
	    } else if (key == null ? "subject" == null : key.equals("subject")) {
		iTextRenderer.getWriter().getInfo().put(PdfName.SUBJECT, val);
	    } else if (key == null ? "creator" == null : key.equals("creator")) {
		iTextRenderer.getWriter().getInfo().put(PdfName.CREATOR, val);
	    } else if (key == null ? "description" == null : key.equals("description")) {
		iTextRenderer.getWriter().getInfo().put(PdfName.DESC, val);
	    } else if (key == null ? "keywords" == null : key.equals("keywords")) {
		iTextRenderer.getWriter().getInfo().put(PdfName.KEYWORDS, val);
	    } else {
		/* This line allows for arbitrary meta tags and may not be what we want. */
		iTextRenderer.getWriter().getInfo().put(new PdfName(key), val);
	    }
	}
    }
}
```



In our application we just need a `MetaDataCreationListener` object, feed it with the DOM Document representation of our xhtml document and set the `renderer`s listener to this instance.
```
FileOutputStream pdfOutputStream = new FileOutputStream( "Output.pdf" );

DocumentBuilder dBuilder = DocumentBuilderFactory.newInstance().newDocumentBuilder();
Document doc = dBuilder.parse( new File( "Input.html" ) );

ITextRenderer renderer = new ITextRenderer();

MetaDataCreationListener mcl = new MetaDataCreationListener();
mcl.parseMetaTags( doc );

renderer.setListener( mcl );
renderer.setDocument( doc );
renderer.layout();
renderer.createPDF( pdfOutputStream );

pdfOutputStream.close();
```