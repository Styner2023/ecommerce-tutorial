# Header and Navbar

Now that you have seen how html works, let's go ahead and start with working on your website.

Start by displaying the **name** of your website and **navbar**.

You will put these two inside a ```<header>``` tag.

>[info] To learn more about header tag: [Header tag](https://www.w3schools.com/tags/tag_header.asp)

Inside our header tag, we will have ```<h1>``` tag and ```<nav>``` tag.

```<h1>...<h6>``` tags are used to define html headings.

```<h1>``` defines the most important heading. ```<h6>``` defines the least important heading.

Headings are used to signal a hierarchy of information. Imagine you have a topic, it might start with an h1 heading. Inside that topic you have two subtopics, these would use the h2 heading. 

Use the ```<nav>``` element to define a set of navigation links.
>[info]To learn more about nav tag: [nav tag](https://www.w3schools.com/tags/tag_nav.asp)

Navigation will present a list of choice, you can use a list structure, which is made of a list tag (ul or ol) that contains a List Item tags (li).
>[info]To learn more about list tag: [list tag](https://www.w3schools.com/html/html_lists.asp)

The ```<ul>``` tag defines an unordered (bulleted) list.

# Adding the Header

>[action]
>
> Inside your ```index.html```, delete the ```<p>``` tag that contains 'Hello World' ,and instead add the header element along with the navbar containing the 3 links as below.
>
> Use the ```<ul>``` tag together with the ```<li>``` tag to create an unordered lists.
>
>  Instead of copying and pasting the given code, type it out. This will give you more practice. 🤓
>
```html
<header class='page-header'>
  <h1>The Mood Shop</h1>
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Cart</a></li>
    </ul>
  </nav>
</header>
```

The `<a>` is known as the Anchor tag, we use that to link to other documents on the web. The `href` attribute usually contains the address of the link. In this case we used the `#` as a placeholder. 

<!-- -->

>[action] Now refresh your html page.

Yay! You should see the name of your site, **The Mood Shop**, and 3 links.

![Navbar No style](assets/01_header-navbar_unstyled-navbar.png "Navbar no style")

# Update Progress on Github

>[action] Now is a great time to commit your progress.
>
```bash
git add .
git commit -m 'made navbar skeleton'
git push
```
