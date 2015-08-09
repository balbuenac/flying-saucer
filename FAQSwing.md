## Swing Related Questions ##

  1. [How do I make my program follow hyperlinks?](#How_do_I_make_my_program_follow_hyperlinks?.md)
  1. [How do I get access to the Swing components that make up my form fields?](#How_do_I_get_access_to_the_Swing_components_that_make_up_my_form_fields?.md)
  1. [How do i get the starting index of selected text?](#How_do_i_get_the_starting_index_of_selected_text?.md)
  1. [The Size of the Rendered Document](#The_Size_of_the_Rendered_Document.md)

### How do I make my program follow hyperlinks? ###
You need a mouse listener that detects link clicks and does the HTTP request. The `BasicPanel` supports tracking mouse events and delegating them to `FSMouseListener` instances. You can use the `org.xhtmlrenderer.swing.LinkListener` class, which implements `FSMouseListener`, for basic hyperlink navigation support.

### How do I get access to the Swing components that make up my form fields? ###
Take a look at the `org.xhtmlrenderer.simple.extend.XhtmlForm` class. Form elements are "replaced" at runtime by the `org.xhtmlrenderer.swing.SwingReplacedElementFactory` if you're using the `XHTMLPanel` class for rendering. The factory actually creates a new `XhtmlForm` class which creates and tracks the components. To receive a callback when the user submits a form, add a `FormSubmissionListener` instance to your `BasicPanel`.

### How do I get the starting index of selected text? ###
> I am using the selection / highlighting capabilities in Flying Saucer. Hightlighting works fine, but I need to have the index of the selection. Is this possible?

That's not possible out of the box. The DOM interface doesn't provide position information. An option is to walk through the nodes of the document to the left of the start of the selected range and then adding all the text content lengths.

### The Size of the Rendered Document ###
> How do I figure out the size of a document I'm rendering? Can I get this from the renderer? How about preferred size of XHTMLPanel? Why isn't my panel properly sized on screen?
The rules are that the document size is calculated after a layout takes place; for rendering to a Swing panel, this can only happen if the container for the panel (e.g. the window) is displayable. See [this email thread in our mailing list](https://xhtmlrenderer.dev.java.net/servlets/ReadMsg?list=users&msgNo=777) for a discussion. In our demos/samples directory in the source distribution, the `PanelResizeToPreferredSize` and `JPanelSizeToDocument` show how this is done. Basically (quoting from the mail thread):

So basically you want to:

  1. create the frame and add components to it
  1. call `f.pack()` to make them displayable
  1. layout documents in `XHTMLPanel` instances using `doDocumentLayout(graphics)`
  1. call `f.pack()` again now that the preferred size of the `XHTMLPanel` instances has been calculated"If you are relying on a layout manager that itself relies on its components' preferred sizes (like FlowLayout) you need to make sure to follow the rules above in order for the layout manager to pick up the size of the panel **after** it has been layed out. The second call to `pack()` after `doDocumentLayout()` takes care of doing this. See `PanelResizeToPreferredSize` for an example using `FlowLayout`.

