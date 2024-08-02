# Displaying Moods
This chapter will focus on displaying all moods on our page. Currently our page has only a navbar.

At the end of this chapter, we will be able to have something like this.

![Items display](assets/01_displaying-moods_items-display.png "Items Display")

The first thing we need are the images to display for each mood.

The next thing we will need to do is get the json data that holds all the information about each mood including the name, image url, description and price.

The json data that we will be using is located in `data.js` file.

>[action]
>
> Both the images folder and the data.js file are located inside this Github repo : [ecommerce-tutorial-files](https://github.com/Tech-at-DU/ecommerce-tutorial-files)
>
> Navigate to the github link and download the repo as a zip file.
>
![Download zip](assets/02_displaying-moods_download-zip.png "Download zip")

Now navigate to your resources folder.

>[action]
>
> Move the **images** folder that's located in the repo you've just downloaded into your project folder.
>
> Move the `data.js` into your project folder.  

# What exactly is a JSON data? 🤔
JSON, AKA JavaScript Object Notation

A JSON object contains data in the form of key/value pairs:

- The key and value pairs are separated by a colon(:)
- Located left of the colon is the key, and on the right is it's value.

If you open your `data.js` file, you will see an array of JSON data.

```js
const data = [{
  "id": 1,
  "name": "happy",
  "image": "./resources/images/happy_spongebob.gif",
  "desc": "Happiness lies in the joy of achievement and the thrill of creative effort.",
  "price": 5.99
}, {
  "id": 2,
  "name": 'sad',
  "image": './resources/images/sad_spongebob.gif',
  "desc": "Tears are words that can't be explained.",
  "price": 5.99
}
...
```

Each product is represented as an object. An object is arranged in property value pairs. The first object in the list is: 

```JS
{
  "id": 1,
  "name": "happy",
  "image": "./resources/images/happy_spongebob.gif",
  "desc": "Happiness lies in the joy of achievement and the thrill of creative effort.",
  "price": 5.99
}
```

The properties are: id, name, image, desc, and price. The name is separated from the value by a colon ":". Each property is is followed by a comma. 

> [info]
>
> Here are a few links to learn more about json objects.
>
> - [Intro to JSON](https://www.copterlabs.com/json-what-it-is-how-it-works-how-to-use-it/) - the first few chapters gives a good introduction to JSON
> - [JSON example](https://www.javatpoint.com/json-example),
> - [JSON short Tutorial](https://restfulapi.net/introduction-to-json/)

Now that we have a good understanding of JSON, we can better understand what the file we are looking at is. The ```data.js``` file contains an array of objects. Each object contains the data for each mood to be displayed. This data consists of **id, name, image, price** and **description** as a **key:value** pair.

>[action]
>
>Navigate to `index.html` file
>
> Below our header element in our `index.html` file, let's add another element called **main**. This will hold all the mood items.
>
```html
<div class='items' id='items'>
    <!-- Display moods here -->
</div>
```

We will be using javascript to dynamically display all the items for the mood shop. We will use a **for loop** to loop through each object inside the `data.js` array and assign image to the `src` attribute of the img tag, description, and price to show each mood "product".

>[action]
> Create a new file called `scripts.js`. This file will hold all your javascript logic to display the items, and future steps like adding them to the cart and removing them from the cart.
>

Link your `scripts.js` to your `index.html` by adding a `<script>` to the bottom of `index.html`. Make it look like the code snippet below:
> 
```html
<html>
	...
	<body>
	...
		<script src="scripts.js" type="module"></script>
	</body>
</html>
```
>

You're declaring this script as a "module" to allow you to use `import` which will come in the following step! 

Later when you study JavaScript in more detail you will learn more about modules. For now what you need to know, is that we need to decalre this script as a module to use the import statement, which makes it convenient to load the JSON file. 

> [action]
> Open `index.html` add the following at the bottom of the 

> Open `scripts.js`. First we need to get the reference to the containers where all the items will be in.

>[action]
>
> Add this import statement at the top of your `script.js` file.
>
> ```import data from './data.js'```

**Important!** You will need to use a server to view the page from this point on. Without a server you will see an error similar to: 

> **Failed to load resource:** Origin null is not allowed by Access-Control-Allow-Origin. Status code: 0

This a CORS (Cross Origin Resource Charing) error. In a nutshell, CORS prevents webpages from accessing local files. This is a security feature. 

To solve this problem, install Live Server in VSCode. Follow the instructions here: https://www.youtube.com/watch?v=_Tl-6HeV0Rc

**From here on, I will assume you are testing your work with Live Server!**

The next step is to load the JSON as `data` and display all of the items in the array in `div#items`. 

You can get this element using its id name. In order to do this, use the `document.querySelector()` function and pass the id of the element. 

>[action]
>
> Add this at the top of your ```scripts.js``` file:
>
> `const itemsContainer = document.querySelector('#items')`

We also need to import the json file into the `script.js`.

Now that we have access to the json array, we can loop through the array and make image elements out of it.

If you open ```data.js``` and see the image **key:value** pairs, the values are a reference to the source file of corresponding mood gifs located in the images folder. We will be using these values in the `img` `src` tag to display the images.

> [info]
>
> For those curious - [How to create an element in javascript](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)

<!--  -->

# Creating the for-loop

> [action]
>
> Now let's loop over each element inside each object and display their images. This for-loop goes inside the `scripts.js` file.
>
```js
// the length of our data determines how many times this loop goes around
for (let i = 0; i < data.length; i += 1) {
	// create a new div element and give it a class name
	const newDiv = document.createElement('div');
	newDiv.className = 'item'
	// create an image element
	const img = document.createElement('img');
	// this will change each time we go through the loop. Can you explain why?
	img.src = data[i].image
	img.width = 300
	img.height = 300
	// Add the image to the div
	newDiv.appendChild(img)
	console.log(img) // Check the console!
	itemsContainer.appendChild(newDiv)
}
```

Let's break down the above code:

## Breaking Down The JavaScript
We started with a loop. This a programming structure that looks like this: 

```JS
for (let i = 0; i < data.length; i += 1) {

}
```

This loop uses the variable `i` to count, it continues counting while `i` is less then the length of data, and adds one to `i` after each loop. 

read more about loops here: https://javascript.info/while-for#the-for-loop

While we are looping through each object in data, we create a `div` element:

```js
const newDiv = document.createElement('div');
```

This will create an HTML div element. Just as if you had written this but you in this case you did it with code!

```html
<div></div>
```

The second line assigns a class name to the div you just created!

```js
newDiv.className = 'item'
```

Just as if you had written:

```html
<div class='item'> </div>
```

We want this div we created to hold the image, description and price of each item. Let's start with the image.
We can create the image tag using `document.createElement('img')`. This creats an `<img>` tag/element. We'll store it in a variable so we can use it. 

```js
const img = document.createElement('img');
```

Each attribute that we want to add to the image could be added using `img.attributeName`, which is how you added the `src`, `width` and `height` of the image:

```js
img.src = data[i].image
img.width = 300
img.height = 300
```

**Important!** Creating an element doesn't add that element to the DOM! After you create an element if you want to make it visible you will have to add it to the DOM tree with `appendChild()`!

In the code above you added `newDiv` to the DOM as a child of `itemsContainer` with: `itemsContainer.appendChild(newDiv)`.

## Connecting `scripts.js` with `index.html`
Just like we connected our `css` file with our `index.html`, we also need to connect our `scripts.js` file with `index.html`.

> [action]
>
> Add this code right above the ending body tag (`</body>`) in `index.html`.
>
```js
<script src='scripts.js' type="module"></script>
```

`console.log` is a way to print our progress. Once you make the image, you are printing it to the console to see if it's being created. It is a good way to make sure if your code is working the way it's supposed to.

>[action]
>
> On your browser, right click and select inspect element. Navigate to console. You should see image tags.
>
> ![Console log img](assets/03_displaying-moods_console-log-img.png "Console log img")

You should see a list of `<img>` tags in the console. 

Now that you have created the image, you can append it to the `div` element you created. 

```html
<div>
  <img src='images/...' width=300 height=300>
</div>
```

You want to create one div with an img for each element in the data. You will add other things to each of these divs in a future step. 

You used `appendChild()` to append the img element to the div element.
Here's what the javascript code looks like:

```js
newDiv.appendChild(img)
```

# Append To Container

> [action]
>
> Now that we have the `div` with the image, let's go ahead and append it to the main container, so that we could display it on our page. This will be done in the `scripts.js` file.
>
```js
itemsContainer.appendChild(newDiv)
```

Our javascript code should look like this at the end:

```js
// the length of our data determines how many times this loop goes around
for (let i = 0; i < data.length; i += 1) {
	// create a new div element and give it a class name
	const newDiv = document.createElement('div');
	newDiv.className = 'item'
	// create an image element
	const img = document.createElement('img');
	// this will change each time we go through the loop. Can you explain why?
	img.src = data[i].image
	img.width = 300
	img.height = 300
	// Add the image to the div
	newDiv.appendChild(img)
	// put new div inside items container
	itemsContainer.appendChild(newDiv)
}
```

>[action]
>
> This part you'll do on your own! Inside the for loop, create a paragraph element for both description and price to be displayed
>
> ***Hint***: After you create the element, use ```element.InnerText``` to add the text description and price.
>
> This is what we want our js to make:
>
```html
<div>
  <img src='/resource...' width=300 height=300>
  <p>description of mood</p>
  <p>5.99</p>
</div>
```

<!--  -->

Solution to the above is here, but try it on your own first!

>[solution]  
>
``` js
// create a paragraph element for a description
const desc = document.createElement('P')
// give the paragraph text from the data
desc.innerText = data[i].desc
// append the paragraph to the div
newDiv.appendChild(desc)
// do the same thing for price
const price = document.createElement('P')
price.innerText = data[i].price
newDiv.appendChild(price)
```

If you open your browser, you should now be able to see something like this. 🎉🎊

![Display without button](assets/04_displaying-moods_display-without-button.png "display without button")

## Stretch challenge:
>[challenge]
>
> Use the ES6 javascript syntax forEach loop instead of the normal for loop.
[ES6 for each loop](https://gomakethings.com/looping-through-arrays-the-es6-way/)

# Add to Cart
The next thing to do would be adding an `Add To Cart` button for each of the moods.

We will be adding a button element using javascript. This will be in the same for loop we used to create the image, description and prices.

>[action]
>
> After the line where you created the price, add a line to create a button element.
>
```js
// Make a button 
const button = document.createElement('button')
```

We should also make the `id` of each button unique.

> [action]
>
> To do this we will assign each mood a data-id aattribute matching the name of the mood.
>
```js
// add a data-id name to the button
button.dataset.id = data[i].name
```

**Data attribute** are developer defined attributes. Use these when you, the developer, need to store some information with a DOM element. We need to know which product should be added to the cart when you click one of the many add to cart buttons. 

A data attribute is always formatted as `data-name` where 'name' could be any string. In this case `button.dataset.id` will make the attribute `data-id`. 

> [info]
>
> Read up on [data- attributes](https://www.w3schools.com/tags/att_data-.asp) and [custom data attributes](http://html5doctor.com/html5-custom-data-attributes/)

There needs to be a way to access the price of each Mood when their "Add to Cart" button is clicked. 🤔

We will use a ***custom data attribute*** to store the price for each mood on the button. 💡

Here's an example of the code we would use to achieve this:

```js
// creates a custom attribute called data-price. That will hold price for each element in the button
button.dataset.price = data[i].price
button.innerHTML = "Add to Cart"
newDiv.appendChild(button)
```

> [action]
>
> At this point, our for loop should create image, description, price and an 'Add to Cart' button for each mood in the data array. Make sure it matches the following:
>
```js
// the length of our data determines how many times this loop goes around
for (let i = 0; i < data.length; i += 1) {
	// create a new div element and give it a class name
	const newDiv = document.createElement('div');
	newDiv.className = 'item'
	// create an image element
	const img = document.createElement('img');
	// this will change each time we go through the loop. Can you explain why?
	img.src = data[i].image
	img.width = 300
	img.height = 300
	// Add the image to the div
	newDiv.appendChild(img)
	// put new div inside items container
	itemsContainer.appendChild(newDiv)
	// create a paragraph element for a description
	const desc = document.createElement('P')
	// give the paragraph text from the data
	desc.innerText = data[i].desc
	// append the paragraph to the div
	newDiv.appendChild(desc)
	// do the same thing for price
	const price = document.createElement('P')
	price.innerText = data[i].price
	newDiv.appendChild(price)
	// Make a button 
	const button = document.createElement('button')
	// add an  id name to the button
	button.dataset.id = data[i].name
	// creates a custom attribute called data-price. That will hold price for each element in the button
	button.dataset.price = data[i].price
	button.innerHTML = "Add to Cart"
	newDiv.appendChild(button)
}
```

Your page should now show each mood, with description, price and button.

![Display with button](assets/05_displaying-moods_display-with-button.png "display with button")

**Congrats! You have just learned how to display items dynamically using javascript.** 🎉🎊

# Update progress on Github

> [action]
>
> Now is a good time to update your progress on Github.
>
```bash
git add .
git commit -m 'displayed moods with button using javascript'
git push
```
