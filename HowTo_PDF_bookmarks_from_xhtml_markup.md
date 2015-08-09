#Describes the usage of the special `bookmarks` element.

# Introduction #
To create a PDF with linked bookmarks you can use the special tag `bookmarks`. Simply add a `bookmarks` tag to the `head` of your xhtml document and fill it with `bookmark` elements. Each `bookmark` element can be configured using the two attributes `name` and `href`. The value of `name` attribute will be displayed in the PDF viewers bookmarks panel. The `href` aims at a anchor tag within the xhtml documents body. It's like normal html inner document linking. Just use the value of the anchor tags `name` attribute and prefix it with a `#`.
If you want to build a hierarchy of bookmarks (i.e. to use it as table of contents) you can use the ´bookmark` tag as a _not-empty_ element. In the PDF this will result in a collapsible tree.

As long as the `bookmark` points  to a valid anchor the PDF viewer will follow those links. If it is not valid noting special will happen. The bookmark will be created but does not link to anything.


# Details #
A little example.


**(x)html markup:**
```
 <html>  
     <head>  
         <bookmarks>  
             <bookmark name="A bookmark" href="#bm" />  
             <bookmark name="A bookmark 2" href="#bm2">  
                 <bookmark name="A bookmark 3" href="#bm3" />  
             </bookmark>  
             <bookmark name="A bookmark invalid" href="#bm99" />  
         </bookmarks>  
     </head>  
     <body>  
         <a name="bm1">Jumpmark 1</a>  
         <a name="bm2">Jumpmark 2</a>  
         <a name="bm3">Jumpmark 3</a>  
     </body>  
 </html>
```



**Resulting PDF:**

![http://www.robert-vogel.eu/wp-content/uploads/2011/01/xhtmlrenderer-bookmarks.png](http://www.robert-vogel.eu/wp-content/uploads/2011/01/xhtmlrenderer-bookmarks.png)