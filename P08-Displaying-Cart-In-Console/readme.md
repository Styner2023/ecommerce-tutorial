# Displaying the Cart 
The next step is to display the items in the cart. 

Items in the cart will display in the footer. They will show as a list. Each item will be the name of the product, price, quntity, and some buttons to add, and remove items.

Imagine how you would display each shopping cart item. **Challenge:** Mock up a single item. Write the HTML that would display that item. 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-


We need these extra buttons and inputs becuase this will allow a shopper to update and edit the cart. We will have buttons to: 
- increase the quantity of an item, "+" button
- decrease the quantity of an item, "-" button
- change the quntity, input

We will also have a couple elements to display information about what is in the cart. 
- name of the item
- price of the item
- quantity of the item
- total price, quantity * price

The shopping cart itself will be a list `<ul>` and each item in the cart will be an `<li>`. 

The markup to display all of this might look like: 

```HTML
<ul id="cart-items">
  <li>
    <span>scared</span>
    <input type="number" value="1" class="input-qty" data-id="scared">
    <span>$5.99</span>
    <span>$5.99</span>
    <button class="button-add" data-id="scared">+</button>
    <button class="button-sub" data-id="scared">-</button>
  </li>
  <li>
    <span>shy</span>
    <input type="number" value="2" class="input-qty" data-id="shy">
    <span>$5.99</span>
    <span>$11.98</span>
    <button class="button-add" data-id="shy">+</button>
    <button class="button-sub" data-id="shy">-</button>
  </li>
  <li>
    <span>sleepy</span>
    <input type="number" value="3" class="input-qty" data-id="sleepy">
    <span>$5.99</span>
    <span>$17.97</span>
    <button class="button-add" data-id="sleepy">+</button>
    <button class="button-sub" data-id="sleepy">-</button>
  </li>
  <li>
    <span>surprised</span>
    <input type="number" value="6" class="input-qty" data-id="surprised">
    <span>$5.99</span>
    <span>$35.94</span>
    <button class="button-add" data-id="surprised">+</button>
    <button class="button-sub" data-id="surprised">-</button>
  </li>
</ul>
```

That's a shopping cart with four items. Notice each block is the same but the content changes. 

All cart items are contained in a list: 

```HTML
<ul id="cart-items"><li>
  ...
</ul>
```

And all items in the cart each occupy a list item: 

```HTML
<ul id="cart-items"><li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

Let's look at a single cart item. 

```HTML
<li>
  <span>surprised</span>
  <input type="number" value="6" class="input-qty" data-id="surprised">
  <span>$5.99</span>
  <span>$35.94</span>
  <button class="button-add" data-id="surprised">+</button>
  <button class="button-sub" data-id="surprised">-</button>
</li>
```

Notice the name is in a `<span>` tag. Wrpping it in a span will allow us to style the name separately from all of the other elements. 

The input will display the quantity and allow us to set the quantity to any value. Notice that this has the attribute `data-id`. We need this to identify the product when change the quantity. 

The price and the total price are both in span tags, again to allow us to style these. 

Last the two buttons "+" and "-" will allow us to increment or decrement the quantity by 1. Notice that these both have the attribute `data-id`. This is needed so we can identify the product to adjust when one of these buttons is clicked. 

## Displaying the cart
Now that we know how the cart should manifest in the DOM we can write some code that will generate our cart! 

Remember the the cart is an array of objects! It might look like this:

```JS
[
  {id: "scared", price: "5.99", qty: 1}, 
  {id: "shy", price: "5.99", qty: 2}, 
  {id: "sleepy", price: "5.99", qty: 3}, 
  {id: "surprised", price: "5.99", qty: 6}
]
```

Our goal is to loop over this list and generate the markup above for each item! We need to do this each time something is added to the cart so we should write a function! 

```JS
const displayCart = () => {

}
```

Previously you used `document.createElement()` and `el.appendChild()` to create elements and add them to the DOM. This time you will generate new elements as a string and set that string as the `innHTML` of the parent element. This will make this process easier. 

First define a new empty string. This will contain the markup once we've 

```js
const displayCart = () => {
  let cartStr = ''
  
}
```

Next add a loop that loops once for each item in the cart array: 

```JS
const displayCart = () => {
  let cartStr = ''
  for (let i = 0; i < cart.length; i += 1) {
    
  }
}
```

This loop counts with the variable `i`, continues while `i` is less than the length of the array, and adds 1 to `i` with iteration of the th loop. 

Now get the item in the cart at index `i`, and add an `<li>` tag to the `cartStr`. 

```JS
const displayCart = () => {
  let cartStr = ''
  for (let i = 0; i < cart.length; i += 1) {
    const item = cart[i]
    cartStr += `<li>

    </li>`
  }
}
```

NOTE! I used the \`\`. This is the back tick or back quote. In code this is called a template string. It allows us to insert variables into a string.

Read about Template Strings here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals

Now we can take the values from the object and insert them into the `cartStr`.

```JS
const displayCart = () => {
  let cartStr = ''
  for (let i = 0; i < cart.length; i += 1) {
    const item = cart[i]
    cartStr += `<li>
      <span>${item.id}</span>
      <input type="number" value="${item.qty}" class="input-qty" data-id="${item.id}">
      <span>${item.price}</span>
      <span>${(item.price * item.qty).toFixed(2)}</span>
      <button class="button-add" data-id="${item.id}">+</button>
      <button class="button-sub" data-id="${item.id}">-</button>
    </li>`
  }
}
```

Here you added all of those elements we described above and populated the correct values where needed. 

Last, you need to get the shopping cart element in the DOM and insert the string you assembled into the DOM. 

First, open `index.html`. Find the `<footer>` tag. Add the list with an id name: 

```HTML
<footer>
  <ul id="cart-items"></ul>
</footer>
```

Note the id name: cart-items. 

Now back to `scripts.js`, add the following two lines to the end of the `displayCart` function. 

```JS
const displayCart = () => {
  console.log(cart)
  let cartStr = ''
  for (let i = 0; i < cart.length; i += 1) {
    const item = cart[i]
    cartStr += `<li>
      <span>${item.id}</span>
      <input type="number" value="${item.qty}" class="input-qty" data-id="${item.id}">
      <span>${item.price}</span>
      <span>${(item.price * item.qty).toFixed(2)}</span>
      <button class="button-add" data-id="${item.id}">+</button>
      <button class="button-sub" data-id="${item.id}">-</button>
    </li>`
  }
  // Get the cart 
  const cartItems = document.querySelector('#cart-items')
  // Set the inner html of the cart
  cartItems.innerHTML = cartStr
}
```

Notice here you used the id name: `cart-items` which must be spelled the same as it appears in the DOM. 

NOTE! when you set the `innHTML` of an element you are replacing all of the existing html! Read about it here: https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML

One last step! Functions don't do anything unless we call them! The `displayCart` function isn't going to do anything unless we call on it. Each time we add something to the cart you need need to add a new item to the cart, then display the contents of the cart! 

Looks for the event listener that listens for the 'click' event. It should look like this: 

```JS
document.body.addEventListener('click', (e) => {
  if (e.target.matches('.add-to-cart')) {
    addItemToCart(e.target.id, e.target.dataset.price)
  }
})
```

Add another line here: 

```JS
document.body.addEventListener('click', (e) => {
  if (e.target.matches('.add-to-cart')) {
    addItemToCart(e.target.dataset.id, e.target.dataset.price)
    displayCart() // Display the cart! 
  }
})
```

After adding a new item to the cart you call `displayCart` to display the items in the cart! 

## Testing your work
Using Live Server view index.html in your browser. Click some of the "Add to Cart" buttons. Check the bottom of the page. You should see your cart displayed there. 

Look for the following things: 
- Cart items should display the name, quantity, price, total price, and two buttons "+" and "-"
- If you click the "Add to Cart" button of the same product more than once the product should only appear once, but the quantity should increase. 
- The total should display value equal to the quantity times the price. 

Think about these things while you check your work to make sure that everything is working correctly! 

If things are not right. Think about what you are seeing and ask yourself what could be going wrong. Think about where in your code the problem could be coming from. 

If you see an error message in the console, read it closely, and look for the file name and line number where the error occurs. 

## Conclusion 
What happened here? You used an array to manage a list of objects. You looped over those objects and generated HTML to represent those objects as HTML markup. 

# Update progress on Github
> [action]
>
> Now is a good time to update your progress on Github.
>
```bash
git add .
git commit -m 'displayed cart items on console'
git push
```
