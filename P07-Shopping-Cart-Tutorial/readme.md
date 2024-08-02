# Shopping Cart Tutorial
This chapter along with the remaining chapters will guide you through how to make your ecommerce website functional. You will be adding a shopping cart functionality where users can add and remove items from their cart.

 For simplicity, you will have the shopping cart page on the same page where the moods are displayed.

# Ading a footer
Your shopping cart will be located in the footer of your ecommerce page.

You will add a footer element in our html.
>[action]
> Add a footer element after the main element inside your `index.html` file
>
```html
<footer>
</footer>
```

Your HTML markup should now look like this:

```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Groceries</title>
  <link rel='stylesheet' href='./resources/css/styles.css'>
</head>
<body>
  <header class='page-header'>
    <h4>The Mood Shop</h4>
    <nav>
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
        <li><a href="#">Cart</a></li>
      </ul>
    </nav>
  </header>
  <main class='items' id='items'>
    <!--
      Display moods here
     -->
  </main>
  <footer>
    <!-- Footer -->
  </footer>
  <script src='./resources/js/scripts.js' type="module"></script>
</body>
</html>
```

Follow this shopping cart tutorial to add the shopping cart functionality.

The tutorial is slightly different, but we're essentially using the same functionality of the shopping cart tutorial.

In the video tutorial, all code is written inside ```index.html```. But since we have a separate ```scripts.js``` file, we'll write the javascript code in there instead of inside the ```<script>``` tag.

You can write the javascript functions below the code you wrote for displaying moods in ```scripts.js``` file.

## What is the cart? 
You will store a list of items that a customer has added to the cart in a variable called cart. This `cart` will be an array.

An array is a list that you can add items to, remove items from, access any individual item from at an index (any position in the list), sort and other options. 

> [action]
> In your `scripts.js` add the following: 
> 

## Using functions
To get started you'll define functions that add items to the cart, remove items from the cart, add up the cost of all items in the cart and more. 

> [action]
> In your `scripts.js` add the following: 
> 
> ```JS
> const cart = []
> ```

This defines a variable named `cart` as an empty array `[]` (the empty square brackets define an empty array). 

Note that I used `const`. This defines a variable that is a "constant". This is a variable that can not be reassigned. 

Next define some functions to do some of the things we need to do. These will be empty for now, you will fill them in later! 

> [action]
> In your `scripts.js` add the following: 
> 
> ```JS
> 
> ```

## Handling clicks
To handle clicks we need an event listner. Any element can have an event listener assigned to it. Something like this: 

```JS
someEl.addEventListener('event name', handlerFunction)
```

To handle clicks on body element you might do this: 

```JS
document.body.addEventListener('click', (e) => {
  console.log(e)
})
```

The event type is `click`. This is always a string. The handler function is `(e) => {}`. An event handler always takes an event object as a parameter. 

The event object is important! It contains information describing the event that just ocurred. 

Add the following to your `scripts.js`. 

```JS
document.body.addEventListener('click', (e) => {
  console.log(e.target)
})
```

One property of the event object is `target`, this is the element that was the target of the event, with a click event it's the element that was clicked. 

Test your page, open the web inspector, and look at the console. Click on different elements on the page, you should see the element you clicked appear in the console with each click. 

I clicked a few times and saw this: 

```
[Log] <h2>angry</h2> (scripts.js, line 77)
[Log] <p>…</p> (scripts.js, line 77)
[Log] <p>To be calm is the highest achievement of the self.</p> (scripts.js, line 77)
[Log] <div class="item">…</div> (scripts.js, line 77)
[Log] <div class="items" id="items">…</div> (scripts.js, line 77)
[Log] <body>…</body> (scripts.js, line 77)
[Log] <img src="images/curious_owl.gif" width="300" height="300"> (scripts.js, line 77)
```

Notice you added the event listener to the body tag but the targets other elements inside the body tag. In some case it was the body tag itself. 

**Important concept!** Events ocurr anywhere in the DOM, then they "bubble" up the DOM tree and each parent element gets a chance to handle the event. 

Since the body is top level ancestor for all elements that are visible in the page the body gets a chance to handle all events. 

In many cases it is best practice to handle events at the body. This is called event delegation! 

**Problem*!** We need to know when one of the add to cart buttons is clicked but we don't care of other elements are clicked. 

Solve this problem like this:
- Make sure each "Add to Cart" button has the class name "add-to-cart"
- In the event listener, check that the target matches the description ".add-to-cart" (remember the `.` means this is a class name!)

In the for loop that generates all of the mood items, find the code that creates the button, and assign it the class name "add-to-cart": 

```JS
...
const button = document.createElement('button')
button.className = 'add-to-cart'
...
```

Now edit the event listener. 

```JS
document.body.addEventListener('click', (e) => {
  if (e.target.matches('.add-to-cart')) {
    console.log(e.target)
  }
})
```

Now test your work. Refresh your page, click around the page. This time you should only see messages in the console when you click the "Add to Cart" buttons. 

Here is what I saw: 

```
[Log] <button class="add-to-cart" id="happy" data-price="5.99">Add to Cart</button> (scripts.js, line 79)
[Log] <button class="add-to-cart" id="sad" data-price="5.99">Add to Cart</button> (scripts.js, line 79)
[Log] <button class="add-to-cart" id="angry" data-price="5.99">Add to Cart</button> (scripts.js, line 79)
[Log] <button class="add-to-cart" id="calm" data-price="5.99">Add to Cart</button> (scripts.js, line 79)
```

### Event Delegation
Event delegation is where another element, usually an ancestor, handles events generated by one of its descedants. 

Read more about Event Delegation here: https://javascript.info/event-delegation

## Adding items to the cart
This step asks the question what is a cart item? Any item in the cart should represent the id of the product, the price of the product, and the quantity. You can describe this with an object: 

```JS
{
  id: 'Sad',
  price: 5.99,
  qty: 1
}
```

You need to make an object like this from the product you clicked. Clicking one of the add to cart buttons we get a refernce to the button: 

```
[Log] <button class="add-to-cart" id="angry" data-price="5.99">Add to Cart</button> (scripts.js, line 79)
```

The button an id and a price. Pass these to the `addToCart` function as a parameters. 

```JS
document.body.addEventListener('click', (e) => {
  if (e.target.matches('.add-to-cart')) {
    console.log(e.target)
    addItemToCart(e.target.id, e.target.dataset.price)
    console.log(cart) // Use console.log to test your work
  }
})
```

Edit the `addToCart` function: 

```JS
const addItemToCart = (id, price) => {
  cart.push({ id, price, qty: 1 })
}
```

This should work but it has a problem. If we add more of the same item to the cart we should update the quantity of the existing item rather than adding another item. 

Do this: 

```JS
const addItemToCart = (id, price) => {
  // Loop over cart items. 
  for (let i = 0; i < cart.length; i += 1) {
    // If we find a matching item increase the quantity
    if (cart[i].id === id) {
      cart[i].qty += 1
      return // exit this function early
    }
  }
  // If no matching items were found add a new item
  cart.push({ id, price, qty: 1 })
}
```

## Why use an Array? 
An array is a list of things. In programming terms "things" can be any "type", a type in JS is a: String, Number, Boolean, or Object. 

Array's have some features that make them perfect for solving some programming problems. 
- Arrays have a flexible length, you can add and remove items from an array. [1,2,3].push(4) -> [1,2,3,4] 
- Arrays can be sorted: [2,4,1,3].sort() -> [1,2,3,4]
- You can remove items from an array [1,2,3,4].pop() -> [1,2,3]
- You write structures that loop over the conent of an array no matter how long it is. 
- You can update/edit values in an array. 
- and many other operations. 

An array is known as a collection type. That is an array is a collection of values stored in a signle identifier. An identifier is what we call the name of a variable. 

An array make the perfect solution for the shopping cart. Imagine all of the things a shopper might do, you can find them all in the list above! 

# Update progress on Github
> [action]
>
> Now is a good time to update your progress on Github.
>
```bash
git add .
git commit -m 'add item and show item functions working'
git push
```
