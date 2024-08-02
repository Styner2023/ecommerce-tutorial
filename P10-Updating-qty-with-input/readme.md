# Updating qty with input
In this next section we are going to handle updating the qty with the input fields in the shopping cart. 

To do that we need to know a little more about events. In JavaScript there many different kinds of events. Here is a list: https://developer.mozilla.org/en-US/docs/Web/Events

Some elements in the DOM can produce certain events that other elements can't. Almost every element can accept a "click" event, because anything that can be displayed can be clicked! 

Inputs, like our `<input type="number" value="${item.qty}" class="input-qty" data-id="${item.id}">`, can accept click events but, hwat does that tell us? That someone clicked but that doesn't have much meaning in this context. 

Inputs have value that they display, and when this value changes that is also an event, which is a more meaningful event in this context! Inputs respind to events "focus", "input", and "change".

You'll use the "change" event in the next few steps. The change event occurs when you are finished editing! As you type inside the field there "input" events, when you click outside of an input it issues a "change" event to signal you are finished editing. 

## Add a new event listener
**Challenge:** Define a new event listener. Add it to the body. Make this a change event. You'll need to define a new event listener, the original listener you defined for "click" will only work for a "click" event. This new listener should listen for change events. 

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

You should have something that looks something like this: 

```JS
document.body.addEventListener('change', (e) => {
  
})
```

Your event listener should check the event target for the class name "input-qty", which is the class name assigned to our inputs. Try it yourself. 

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

```JS
document.body.addEventListener('change', (e) => {
  if (e.target.matches('.input-qty')) {
    
  }
})
```

You need a function to update the qty of a cart item. This function will take the `id` and `newValue` as parameters. 

```JS
const updateCart = (id, val) => {
  
}
```

**Challenge:** Loop over the items in the cart, update the qty of the item that matches the id. 

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
-

Might look something like this: 

```JS
const updateCart = (id, val) => {
  // Loop over cart
  for (let i = 0; i < cart.length; i += 1) {
    const item = cart[i] // get the item
    if (id === item.id) {
      // If the id matches set the qty
      item.qty = val

      return // exit this function
    }
  }
}
```

**Challenge:** If someone enters a value that 0 or a nagative number we should remove that item from the cart. 

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

Might look like this: 

```JS
const updateCart = (id, val) => {
  console.log(id, val)
  for (let i = 0; i < cart.length; i += 1) {
    const item = cart[i]
    if (id === item.id) {
      item.qty = val
      // If the value is less than 1
      if (item.qty < 1) {
        // remove this item from the cart
        cart.splice(i, 1)
      }
      return 
    }
  }
}
```

Now that we have this function, you need to call it in your "change" event! **Challenge:** Try writing this on your own!

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

Might look like this: 

```JS 
document.body.addEventListener('change', (e) => {
  if (e.target.matches('.input-qty')) {
    const name = e.target.dataset.id // get the id
    const value = e.target.value // get the value from the input
    updateCart(name, value) // call updateCart with the id and value
    displayCart() // display the cart
  }
})
```

## Test your work
Test your work. Follow the steps from the previous tests to make sure the changes we made here haven't affected any other functionality. 

Now test the new features. 
- Add an item to the cart
- change the qty - only the number should change
- click outside the field - the total price should update

It is a little awkward that we need to click outside the input to get the change to occur. This is how the "change" event works and it's import that you understand this as you might run into this in the future! 

What other events are there? Inputs also react to the "input" event. The input event triggers with each keystroke in an input field. Try this yourself. Edit the "change" event to "input". 

```JS 
document.body.addEventListener('input', (e) => {
  ...
})
```

Test your work. Observe what happens. Follow these steps: 
- Add an item to the cart. A cart item is displayed with qty 1
- Imagine that you want to change the qty to 5. 
- Click in the input field and hit backspace.
- The item disappears. What happened? 

Tyr it again:
- Add an item to the cart. the item displays with qty 1
- Imagine you want to change the qty to 10
- Click in the input field, type 0
- The qty updates to 10, along with the total price. 
- Notice the field is now inactive you will have to click into the field again to continue editing. 

Can you explain the behavior? 

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

Everything is wrorking as it should, as described above. Event is fired each time you type a character into the field. When you deleted a character and the field was empty, the system deleted the field because it thought qty was 0. In the second example, when you typed 10, the system updated the cart but also replaced the displayed elements with new updated elements, and the new input no longer had focus!

How can get around this, because this behavior would be frustrating for shoppers, who expect more from websites these days! 

There are a few more events we can use! The "keydown" event occurs when a key is pressed inside a text input field. This event "fires" each time a key is pressed. This seems too often for out needs, we need an event that only happens when the enter key is pressed. There isn't an event that works like that for an input.

There is a solution! The event object for key events also includes the key that was pressed. We can check for the "Enter" key and update the cart when the "Enter" key is pressed. 

It best, I think if we keep the original "change" event. This way if someone enters a value, and clicks out of the field or tabs to a different field, without pressing "Enter" the page will still update. 

Edit the event back to "change":

```JS
document.body.addEventListener('change', (e) => {
  ...
})
```

Add a new event listener. Use event delegation! Listen for the "keydown" event. Try it on your own...

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

Start here: 

```JS
document.body.addEventListener('keydown', (e) => {
  
})
```

Match the target with the class name: ".input-qty"...

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

Now we have this: 

```JS
document.body.addEventListener('keydown', (e) => {
  if (e.target.matches('.input-qty')) {
    
  }
})
```

From here you want to check the event key. This will be a string that is the key that was pressed. For example if you hit "a" the key would be "a". In the case of special keys, like "Enter", the name of the key is spelled out (notice the case "Enter" begins with "E").

Check for the "Enter" key and then do all of the same things you do in the change handler. 

```JS
document.body.addEventListener('keydown', (e) => {
  if (e.target.matches('.input-qty')) {
    if (e.key === "Enter") {
      const name = e.target.dataset.id
      const value = e.target.value
      updateCart(name, value)
      console.log(e)
      displayCart()
    }
  }
})
```

### Test your work!
Test this again. Follow all of the same steps you used earlier. make sure that all of the previous features are still working. 

- Add an item to the cart
- Edit the qty field, enter 12
- press enter, the display should update
- Try clicking the "+" button. The display now shows "121" thats a problem!

What happened? When we added the first item the cart stored the item as: 

```JS
[{id: "shy", price: "5.99", qty: 1}]
```

Notice qty is 1 (a number!)

When you entered a new value the object in the cart became this: 

```JS
[{id: "shy", price: "5.99", qty: "12"}]
```

Notice that "12" is a string! This is not a number! Now when you try and increase the qty with `item.qty += 1` JS concatenates, that is it adds the character to the end of the string instead of doing the math! 

Read more about this here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Addition#

This is a common error in JS! Be prepared to spot this in the future! 

How can we fix the issue here? You need to convert the string value to a number before updating the cart!

To convert strings, that contain numbers, to numbers JS provides the `parseInt()` and `parseFloat()` functions. You pass in a string and these functions return a number, or NaN (a value that is Not a Number) 

- Read about `parseInt()` here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt
- Read about `parseFloat()` here: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat

Fix the problem with `parseInt()`:

```JS
document.body.addEventListener('keydown', (e) => {
  if (e.target.matches('.input-qty')) {
    if (e.key === "Enter") {
      console.log(e.key)
      const name = e.target.dataset.id
      // Use parseInt !
      const value = parseInt(e.target.value)
      updateCart(name, value)
      console.log(e)
      displayCart()
    }
  }
})
```

Test your work again! 

## Conclusion
You further explored event listeners and again applied event delegation! Event delegation is important, you need to understand this because it is a question that you could be asked at a coding interview! 

Further you explored working with form elements, an input in this case. You saw that you can get the value entered into a form using the value property. 

Again you used core programming concepts like for loops and if else statements, arrays, objects and functions. These are building blocks of all applications. You'll often use these code structures in the applications you write!

You solved problems with strings an numbers, a common issue with JS! 

# Update progress on Github
> [action]
>
> Now is a good time to update your progress on Github.
>
```bash
git add .
git commit -m 'connect cart to footer'
git push
```
