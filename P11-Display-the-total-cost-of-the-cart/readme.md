# Display the total cost of the cart
It would be good to show the total cost of the cart. You'd find that helpful? 

To do this you need to loop over all of the items in the cart and sum the total of each items price times it's qty. 

You need to do this each time the cart is updated and displayed, so you should make a function...

Write a function that will get teh total of all items in the cart. What would you name this? Think about it, the name is very important, since it will remind you and your team what this function does. 

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

I used the name `getCartTotal`. 

```JS
const getCartTotal = () => {
  
}
```

Now you need to loop over all items in the cart...

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

This is what I wrote. It's the same as the code we've written before! 

```JS
const getCartTotal = () => {
  
  for (let i = 0; i < cart.length; i += 1) {
    
  }
  
}
```

To sum all of the items you need to define a variable to hold the total amount. This need to be defined before the loop, and not inside the loop. 

```JS
const getCartTotal = () => {
  let total = 0 // Define a variable to hold the total 
  for (let i = 0; i < cart.length; i += 1) {
    
  }
  
}
```

If the variable were defined inside the loop it be defined new with each iteration, and we'd lose the previous value. 

Next get the cart item and multiply it's qty by it's price. 

```JS
const getCartTotal = () => {
  let total = 0
  for (let i = 0; i < cart.length; i += 1) {
    // get the cart item
    const item = cart[i]
    // calculate the total price for that item 
    // and add it to the total
    total += item.qty * item.price
  }
  
}
```

An import feature of functions is that they can return values. The `return` statement ends a function, you can also follow with a value that the function can return to where it was called. 

You used this earlier with `parseInt()`. The `parseInt(str)` function takes a string and returns a number. You used it like this: 

```JS
const aNumber = parseInt("123")
```

Here you are "calling" `parseInt("123")`, and passing the argument "123" (a string), and `parseInt()` is returning a number, which is assigned to the variable `aNumber`. 

You can do this with `getCartTotal`, like this: 

```JS
const getCartTotal = () => {
  let total = 0
  for (let i = 0; i < cart.length; i += 1) {
    const item = cart[i]
    total += item.qty * item.price
  }
  return total // return total
}
```

Now you can call `getCartTotal()` and it will return the total, you might use it like this: 

```JS
const theTotal = getCartTotal()
console.log(theTotal)
```

## Displaying the cart total
The next step is to display the total amount in the cart. To do this you'll need to:

- get the total amount in the cart
- add an element to the end of the HTML string that is assembled in `displayCart()`. The element can be anything like a `<p>` or `<div>`. 

Try it on your own...

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

Here is what I came up with. I edited the `displayCart()` function.

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

  // Get the total cost in the cart
  const cartTotal = getCartTotal()
  // append a li tag at the end of the cartStr with the total
  cartStr += `<li>Total: ${cartTotal}</li>`

  const cartItems = document.querySelector('#cart-items')
  cartItems.innerHTML = cartStr
}
```

NOTE! You should place the `getCartTotal()` function above the `displayCart()` function since it should be defined before it is used. 

I used an `<li>` tag here because all of these tags end up inside the `<ul>` and a `<ul>` should only contain `<li>` tags! The `<li>` tags can contain anything. 

## Weird numbers...
You may have noticed some weird numbers like: `29.950000000000003` showing some times. 

Try adding 5 of an item to the cart. 

When you add 9 items you get: `53.910000000000004`. 

This is normal! In short this is a by product of converting numbers from base 2 to base 10. 

You are used to thinking in base 10, so 10 / 3 = 3.333333333333333 makes sense. The results above are similar but happen when the computer converts numbers from base 2 to base 10. 

How do we fix these? 

JavaScript has us covered with the `.toFixed()` method. This method converts any number into a string with a fixed number of decimal places. Here is an example:

```JS
const answer = 10 / 3
console.log(answer) // 3.3333333333333335
console.log(answer.toFixed(2)) // "3.33"
```

You need to apply toFixed at any place your code is displaying a decimal number. Here is a list of locations that I identified: 

- `displayCart()` where the total price is displayed. 
- `getCartTotal()` after the total is calculated. 

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

In `displayCart()`:

```JS
...
cartStr += `<li>
    ...
    <span>${(item.price * item.qty).toFixed(2)}</span>
    ...
  </li>`
...
```

In `getCartTotal()`:

```JS
const getCartTotal = () => {
  let total = 0
  for (let i = 0; i < cart.length; i += 1) {
    const item = cart[i]
    total += item.qty * item.price
  }
  // Use toFixed(2) to convert to string with 2 decimals
  return total.toFixed(2)
}
```

## Conclusion
In this section you defined a new function and used return to return a value. This allowed you to reuse code that calculates a value that can be displayed on the page. 

You also solved problems with displaying numbers in software using the `parseInt()` to convert strings to numbers, and `.toFixed()` to convert numbers to strings with a fixed number of decimals. 

# Update progress on Github
> [action]
>
> Now is a good time to update your progress on Github.
>
```bash
git add .
git commit -m 'add button connected to cart'
git push
```
