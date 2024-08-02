# HTML Semantics

In this Chapter we will be using: **HTML** and **CSS**

## What is HTML?

HTML is short for "HyperText Markup Language". That may sound scary, but it simply means it is a language for describing web-pages using ordinary text.

HTML describes the structure of the a document. You might write a story or an article, adding markup gives your work an underlying structure that describes what is a heading, what is a list, or a quote taken from another work. 

## What is an HTML tag?

HTML tags are the hidden keywords within a web page that define the structure of your document.

Most tags have two tags, an opening and a closing tag. For example, **```<html>```** is the opening tag and **```</html>```** is the closing tag. Note that the closing tag has the same text as the opening tag, but has an additional forward-slash ( / ) character.

## What are tag attributes?

Attributes allow you to customize a tag, and are defined within the opening tag, for example: `<img src="image1.jpg">` or `<p class="lead"> ... </p>`. For the **img** tag, the attribute is **src**, which defines where the source file of the image is located. For the **p** tag the attribute **class** defines the name of the style group that should be applied to this elemwnt. To learn more about HTML tags click on this link : [HTML tags](http://www.simplehtmlguide.com/whatishtml.php)

An attribute is always formed as `property="value"` and the value is always in quotes.

# Let's start by making the landing (shopping) page for our website.

First, let's have the basic outline/boilerplate for HTML.

You can learn more about the outline here: [HTML template](https://www.sitepoint.com/a-basic-html5-template/)

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Title of the document</title>
  </head>

  <body>
    The content of the document......
  </body>
</html>
```

The first line, ```<!DOCTYPE>``` is called **Document Type Declaration**. It tells the browser what kind of document it's looking at. In our case, it's telling the browser that our document is an Html file.

Next is the ```<html>```. This tag defines the HTML document. Everything that is part of this document must be inside the HTML tag (DOCTYPE is the only exception).

The head tag contains the title of our page, ```<title>```. The head tag contains meta information that describes the document.

The ```<body>``` element contains all the content of an HTML document, such as headings, paragraphs, **images**, **hyperlinks**, **tables**, **lists**, etc. We also link our **javascript** file here. The body tag contains everything that will visible in the browser. 

# Displaying our 'Hello World'

Let's start by displaying 'Hello World' in our browser.

> [action]
>
> In `index.html`, add a paragraph tag (```<p>```) inside the body tag. Inside the paragraph tag, write, Hello World!
>
```html
<p> Hello World </p>
 ```
>
> open your file in the browser now. Open the file in your browser, follow the steps below:
>
> 1. Choose File > Open.
> 1. Navigate to an select your HTML document.
> 1. You will see your file open in a new tab.
>
> You should see 'Hello World'.

Congratulations! 🎉 You just displayed text in your browser.

# Update progress on Github

> [action] save and push your progress on github
>
```bash
git add .
git commit -m 'displayed hello world'
git push
```
