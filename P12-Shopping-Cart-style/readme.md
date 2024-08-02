# Shopping cart style
While the shopping cart might be working it doesn't look that great it need some styles to make it look good. 

## Fit the footer into a column
The footer seems to be all the way on the left while the rest of the page fits a column 80% the width of the page and centered. 

Can you make the center the footer and make it 80% the width of the page? 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

You can borrow this idea from the `.items`. Set the width to 80%, and margins to auto. Margin 'auto' centers the element by dividing the remaining space between the left anf right margins. 

```CSS
footer {
  width: 80%;
  margin: auto;
}
```

The list, `<ul>`, adds padding on the left, margin at the top and bottom, and those bullets to left of each list item. I think it would look better if we removed those. 

Use a selector that targets just the ul tag. 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

I used the descendant selector: 

```CSS
footer ul {
  padding: 0;
  margin: 0;
  list-style: none;
  margin-top: 1rem;
}
```

Now time to improve the typography. Look closely, you'll see the text in the input elements and the buttons is smaller than the base font size of the page. This is default style. The inputs show font size of 11px while the rest of the page is 16px. 

This make forms and form elements harder to read. Fix that! 

-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-
-

This is what I did: 

```CSS
input, button {
  font-size: 1rem;
}
```

Here my selector targets both the input and the button elements with the group selector (the comma `,`). 

The button and the input have sort of border around the outside. This looks vague and not so great lets style it! 

Also the, the border, around the input and the buttons, hugs the text really close which makes these harder to read. Better to give the text some space. Do this by adding some padding. 

```CSS
input, button {
  font-size: 1rem;
  padding: 0.5rem 0.75rem;
  border: 1px solid;
}
```

Notice! `padding: 0.5rem 0.75rem` has two values. When you set one value it applies to all four sides. When set two values the first applies to the top and bottom, while the second applies to the left and right. 

`border` is a shorthand property for all of the border properties. You must set the `border-style` or you won't see a change. 

Might be nice if we arranged the cart items across the page. Do this by setting the li to display flex. 

```CSS
footer li {
  display: flex;
  justify-content: flex-end;
  align-items: baseline;
}
```

- `justify-content: flex-end` pushes everything to the right. 
- `align-items: baseline` aligns everything vertically at the basline (the baseline is the imaginary line the text rests on)

It would be nice if the first element, the span with the name of the item, was on the left. Do this by targeting that first element and setting it's right margin to auto. 

```CSS
footer li > span:first-child {
  margin-right: auto;
}
```

You could, and it might have been better, given that first span a class name. This example shows the power of CSS selectors! The selector above looks for the footer, then finds all of the descendant li tags, then looks for the span tags that are children, gives us the first of those children! 

This is looking better! Might be nice if there were space around the element adding margin left and right to all of the elements in the li would work. 

Inspect your page and look at the li tag. 

```HTML
<li>
  <span>shy</span>
  <input type="number" value="13" class="input-qty" data-id="shy">
  <span>5.99</span>
  <span>77.87</span>
  <button class="button-add" data-id="shy">+</button>
  <button class="button-sub" data-id="shy">-</button>
</li>
```

These li tags contain three different types: span, input, and button. It would be nice if we could select them all! 

We can! Use the * selector! 

```CSS
footer li > * {
  margin: 0 1rem;
}
```

The selector above starts at the footer, finds the descendant li tags, then gets all of the children or any type. We apply 0 margin to the top and bottom, and 1rem of margin to the left and right. 

## Conclusion
That was epic! Just another day in the life of the frontend web dev.

Everything you did here was done with vanilla HTML, CSS, and JS. Its good to develop these skills because they apply everywhere. In the future you will start workign with libraries like React, and Vue JS, and while those tools are more sophisticated they are built on the ideas covered! Those tools are built with vanilla HTML, CSS, JS! Understanding these ideas is essential to being the web dev you can be! 

# Congrats!!

> [action]
>
> Now is a good time to update your progress on Github.
>
```bash
git add .
git commit -m 'cart fully functional'
git push
```

**CONGRATS on completing the Mood Shop tutorial!** You should now have a better understanding on how to use HTML, CSS, and JS together!
