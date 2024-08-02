# Styling Header
Currently, the header and navbar don't really look like a header or navbar. You need to add some styles.

> Create a file named `styles.css`. This is where all your element styles would go to.
>
```bash
touch styles.css
```
> Now, open the `styles.css` file.

## Reference elements in a stylesheet
There are different ways on how to reference elements in a stylesheet.

1. by the element tag name.
1. by the class name.
1. by id name  

To learn more about selectors, visit [CSS selectors](https://www.w3schools.com/css/css_selectors.asp)

# Styling the body element
The body is the first thing we want to style.
We're going to start by styling the **font family** and **font size**.

**Font family** - there are different font families. Here we will be using: Helvetica.

**Font size** - 16px.

**Line height** - to increase spacing between lines (1.5 - 1.6) is recommended. 

Line height sets the vertical space between lines. The value is multiplied by the font size. If the font size were 16px, a line-height of 1.5 would set the space between lines to 24px. 

>[action]
>
> Open your styles.css file and add the following line of code.
>
```css
body {
  font-family: Helvetica;
  font-size: 16px;
  line-height: 1.5;
  margin: 0;
}
```
>
> Now refresh your browser.

Hmm, we were expecting to see some change but don't see any. 🤔

Can you guess why?

> [solution]
>
> That's because we haven't linked our stylesheet in our HTML file.
We need to use a ```<link>``` tag inside the ```<head>``` element to link our css file.

>[action] Navigate to `index.html`. Inside the ```<head>``` element of your `index.html`, add the ```<link>``` element.
>
```html
<link rel='stylesheet' href='styles.css'>
```
>
> Now go ahead and refresh your page.

Sweet! We see some font change!

the `rel` attribute tells the browser what type of file you are linking to, in this case a "stylesheet", and the `href` attribute tells the browser where to find that file. 

We want our website name to be on the left side and the navigation links (Home, about, cart) to be on the other side. For this, we will use **flexbox layout**.

# What is flexbox?
Flexbox helps to position elements inside a container.
We set flex properties on the parent element (container) to make elements inside the container move.

Flex box arranges all of the child elements along an axis which can horizontal or vertical.

> [info]
>
> To learn more about flexbox: [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp)

The flex container is activated by setting the **display** property to flex: `display: flex;`.

```<Header>``` is our container so we will be setting the display property of header to flex. In order to refer to our header inside the css file we will be using it's class name.


The class name for header is '**page-header**'.
we use dot (.) before the name when referring to class names in css files.

For example:  **.page-header**

>[action]
>
> Inside your `styles.css` file, add the styles for page-header.
>
```css
.page-header {
	display: flex;
	flex-direction: row;
	justify-content: space-between;
  background-color: bisque;
}
```
>
> Refresh your web page again. You should see the title and navbar lists in rows.

The navbar itself is not in rows, because the lists are inside the ```<ul>``` container. Hence we need to use flexbox on it to display the elements in rows.

>[info] To select the ```<ul>``` tag, we can use **.page-header ul**
This will select ```<ul>``` elements inside the page-header class.

>[action] Inside your `styles.css` file, add this code to style the navbar lists.
>
```css
.page-header ul {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  list-style: none;
}
```
> Refresh your page again. You should now see the lists in rows.

To remove the bullet points in each list, we can set the property list-style to none in the ```<ul>``` tag.

>[action] Modify your **.page-header ul** rule in `styles.css`
>
```css
.page-header ul {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  list-style: none;
}
```
>
> The last style we need to add to the navbar is
>
> 1. adding spaces between the nav links
> 1. removing the underlines (text decorations) on the ```<a>``` tags.
>
```css
.page-header a {
  display: block;
  padding:0.5em;
  text-decoration:none;
}
```

![Navbar Example](assets/01_styling-header_navbar-example.png "Navbar example")

Congrats! You have just made a decent looking navbar using CSS.

## CSS Rules and Selectors
Examine the CSS you just wrote. The CSS language is written in "rules". Every rule begins with a selector, followed by a block that contains properties and value pairs. 

For example: 

```CSS
body {
  font-family: Helvetica;
}
```

This "rule" defines `body` as the selector, the block defines the property of `font-family` with a value of `Helvetica`. 

Selectors identify elements where the properties and values should be applied. In this case the selector is a type, meaning a tag name, in this case the rule applies to `body` tags. 

```CSS
.page-header ul {
  list-style: none;
}
```

The selector for this rule is `.page-header ul`. The first part begins with a dot `.` which means that this is a class name! By itself, `.page-header` would apply the rule to any tag with the class name "page-header".

The space between `.page-header` and `ul` says that `ul` is a descendant of `.page-header`. 

Taken as a whole, the selector: `.page-header ul` applies the rule to any `ul` tags that are descendants of an element with the class name "page-header".

Looking at the markup below, you can see that the `<ul>` tag appears within the `<div class="page-header">` tag, so the rule above applies to this ul!

```HTML
<div class="page-header">
  <ul></ul>
</div>
<ul></ul>
```

The `<div>` tag has the class name `page-header`, so the rule above applies. The first `<ul>` appears within that tag so the selector `.page-header ul` applies to it. The second ul is not a descendant of an element with the class name `page-header` so the rule does not apply to the second ul! 

Notice how selectors can be very selective! You can use them to your advantage! 

Imagine the HTML below. 

```HTML
<div class="page-header">
  <ul></ul><!-- ul 1 -->
  <div>
    <ul></ul><!-- ul 2 -->
  </div>
</div>
<ul></ul><!-- ul 3 -->
```

In this example the selector `.page-header ul` applies to both ul 1 and 2. Since they are both within (descendants of) `.page-header`. But not to ul 3 because it is not inside of an element with the class name "page-header".

# Update progress on Github

Now is a good time to update your progress on Github.

# Stretch Challenge

> [challenge]
>
> - Change the background color of the navbar
> - Customize the navbar by changing the font size and font family to your desired choice.

```bash
git add .
git commit -m 'styled the header and navbar'
git push
```
