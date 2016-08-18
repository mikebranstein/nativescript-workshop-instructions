## Navigation

You've learned how to create pages and add text to pages with the `<Label text="..." />` element. But, switching the default start page for the application just to test each page is a little cumbersome. 

Just like HTML applications, NativeScript apps are a collection of pages. Similarly, moving between pages is called navigating.

In this section, you'll be learning how to navigate between pages by placing a Button on a page, attaching a `tap` event to the button, and responding to the `tap` event by writing some JavaScript code. 

### Adding multiple UI elements to a page

Before we go too much further, I need to introduce you to something called a layout. Layouts are UI elements (similar to the `<Label />` element) that allow you to organize the UI of each page. 

Up until now, we've been putting `<Label />` elements directly underneath the `<Page>` element of each page. What is not completely obvious is that most UI elements (like `<Page>`) can only have a single child element. You can technically add multiple elements within a `<Page>`element; but they won't display in your app.

> To display multiple elements on a page, you need to use a layout.

Let's learn about the simplest (and most common) first layout.

<h4 class="exercise-start">
    <b>Exercise</b>: Using the StackLayout to organize UI elements in a "stack"
</h4>

Go to the `home-page`, and add a `<StackLayout>` element to the page, directly within the `<Page>` element. Move the existing `<Label />` element inside of the `<StackLayout>`.

```xml
<Page>
    <StackLayout>
        <Label text="Welcome to the Tekmo app!" />
    </StackLayout>
</Page>
```

Change the app's default starting page back to the `home-page` page.

```javascript
var application = require("application");
application.start({ moduleName: "home-page" });
```

As you can see, the home page doesn't look very different. 

![image](images/chapter4/tekmo-1.PNG)

Add another `<Label />` element and observe the changes.

```xml
<Page>
    <StackLayout>
        <Label text="Welcome to the Tekmo app!" />
        <Label text="To navigate to another page of the Tekmo app, use the buttons below." />
    </StackLayout>
</Page>
```

![image](images/chapter4/tekmo-2.PNG)

<div class="exercise-end"></div>

As you can see, the `<StackLayout>` stacks UI elements on top of each other on a page. 

![image](images/chapter4/tekmo-2.PNG)

### Wrapping text

But wait! Do you see the text you just added? It's running off the side of the page. 

> **NOTE** By default, text within a `<Label />` element does not wrap to new lines.

Let's learn how to fix that.

<h4 class="exercise-start">
    <b>Exercise</b>: Wrapping text
</h4>

Add the `textWrap="true"` attribute to the `<Label />` element to wrap the text to multiple lines.

```xml
<Page>
    <StackLayout>
        <Label text="Welcome to the Tekmo app!" />
        <Label textWrap="true" text="To navigate to another page of the Tekmo app, use the buttons below." />
    </StackLayout>
</Page>
```

Now, your text will wrap to multiple lines!

![image](images/chapter4/tekmo-3.PNG)

<div class="exercise-end"></div>

### Navigating with Buttons

We've finally made it to navigation. If you recall, I said we'd be doing 3 things to navigate from one page to another:

1. Add a `<Button />` element to the page
2. Add the `tap` event to the button
3. Write JavaScript code to respond to the `tap` event and navigate to a new page

<h4 class="exercise-start">
    <b>Exercise</b>: Add a button to a page
</h4>

Add a `<Button />` element to the page, after the last `<Label />`. Buttons have a similar property named `text` that allows you to change the text of the button. 

```xml
<Button text="About" />
```

Next, add a `tap` event attribute to the `<Button />` element. Most UI elements have a variety of *events* that can execute JavaScript code when triggered. When an event is triggered, it will automatically run the function name specified in the event attribute. 

```xml
<Button text="About" tap="onTap" />
``` 

The complete code listing for the `home-page` page is below.

```xml
<Page>
    <StackLayout>
        <Label text="Welcome to the Tekmo app!" />
        <Label textWrap="true" text="To navigate to another page of the Tekmo app, use the buttons below." />
        <Button text="About" tap="onTap" />
    </StackLayout>
</Page>
```

![image](images/chapter4/tekmo-4.PNG)

<div class="exercise-end"></div>

In the above code, when the button's `tap` event is triggered (i.e., when the button is tapped), the JavaScript function named `onTap` will be called. But, where does the `onTap` function reside?

If you recall from an earlier section, you learned that NativeScript pages are a collection of XML, CSS, and JavaScript files, linked together by their naming convention. 

With this in mind, to associate JavaScript code with the `home-page` page, create a file named `home-page.js`. 

<h4 class="exercise-start">
    <b>Exercise</b>: Link the button's onTap event with the onTap() JavaScript function
</h4>

Create a file named `home-page.js` in the `app` folder of your app.

![image](images/chapter4/code-tekmo.PNG)

Open the file in VS Code and add a function named `onTap`. Be sure to export the function, so the page can access it.

```javascript
function onTap() 
{
    // do something
}
exports.onTap = onTap;
```

Head back to GenyMotion, wait for your app to reload, and click the `About` button. Pressing the button doesn't do much right now. In fact, nothing happens because the `onTap` function is empty.

<div class="exercise-end"></div>

### Learning to use console.log

One of the easiest ways to tell what's happening in your NativeScript code is by using the `console.log()` function. `console.log()` outputs text to the command line. Let's add it to the `About` button's `onTap` event.

<h4 class="exercise-start">
    <b>Exercise</b>: Logging messages to the command line
</h4>

Add a call to `console.log()` to the `onTap()` function.

```javascript
function onTap() 
{
    console.log('onTap called...');
}
exports.onTap = onTap;
```

Wait for your app to reload in GenyMotion, then click the `About` button. You should see the text *onTap called...* output to your command line.

![image](images/chapter4/tekmo-on-tap.gif)

<div class="exercise-end"></div>

### An introduction to modules

The last thing you need to learn about before navigating between pages is the NativeScript code modules. The core modules are cross-platform abstractions provided by NativeScript that allow you to interact with various aspects of the Android and iOS platforms (i.e., cameras, images, files, and navigation). 

The modules are actually written in TypeScript, transpiled down to JavaScript, and included in every NativeScript project by default. You don't need to know how the modules work under the scenes, but sometimes it's neat to see the guts of NativeScript. Let's take a quick look.

<h4 class="exercise-start">
    <b>Exercise</b>: Looking at the core modules
</h4>

As I've said, the core modules are included in every NativeScript project. These are included in the project by using [npm](https://www.npmjs.com/). You don't need to manually run `npm` to include the core modules. 

To find the core modules, go back to VS Code. Open the `node_modules` folder that is in the root of the tekmo app. Note: this is **not** in the `app` folder, it is outside the folder. 

In the `node_modules` folder, open the `tns-core-modules` folder. There's a lot to see here.

![image](images/chapter4/core-modules.PNG)

Inside of the `tns-core-modules` folder is a massive hierarchy of folders and files. These files make up the entirety of the NativeScript framework. You'll learn how to use these throughout the lab, but I also want to point you to the [official NativeScript documentation](https://docs.nativescript.org), which is a comprehensive listing the core modules and how to use them.

Inside of the `tns-core-modules` folder, find the folder `ui` and then sub-folder `frame`. Go ahead and open the `frame` folder.

> **WARNING** Be careful when you're looking at modules. Don't change their code!

![image](images/chapter4/frame-module.PNG)

Inside, you'll find a variety of files. 

The frame module is used to navigate between pages, so we'll be using it later. I don't want to go into the weeds too far here, because it's not really important for you to know how and what the frame module does, but as we begin to use modules, just know that if you're curious to know how and what module functions do, you can always come and look at their source code directly in the `tns-core-modules` folder.

Take a few minutes to explore the module code (if you'd like). Close the modules folders and files if you have them open before you continue. 

<div class="exercise-end"></div>

### Navigating to another page

After the brief detour looking at the core modules, let's get back on track with navigation between pages.

<h4 class="exercise-start">
    <b>Exercise</b>: Navigating from the home page to the about page
</h4>

Return to the `home-page.js` file, where we added the `onTap()` function. 

```javascript
function onTap() 
{
    console.log('onTap called...');
}
exports.onTap = onTap;
```

We'll be modifying this code to load the frame module and then use the `navigate()` method of the frame module to navigate to the about page.

Import the frame module by using the `require()` function. Place this at the top of the `home-page.js` file.

```javascript
var frameModule = require('ui/frame');
```

> **NOTE** You don't need to give NativeScript the full path to the frame module. This is because NativeScript has special conventions built into the framework that know exactly how to find and load modules by specifying a folder. 

To navigate from one page to another, you use the `navigate()` function of the `topmost()` property on the frame module. Add the following code to the `onTap()` function.

```javascript
frameModule.topmost().navigate("about-page");
```

So, you may be thinking, "What's this `topmost()` thing?" Every page in a NativeScript app has something called the *topmost* frame. To get the topmost frame, we use the `topmost()` property of the frame module. Once you have that topmost frame, you can call the `navigate()` function to navigate to another page. 

> **NOTE** `navigate()` can take additional arguments to perform different types of animated navigations, and to pass data between pages when navigation occurs. You'll learn how to do that later.

Let's check the results of the navigation in your emulator. Tap the About button and you should navigate to the about page.

![image](images/chapter4/nav.gif)

If you're running on Android, you can hit the back button to return to the Home page. On iOS, you'll notice a `< Back` button at the top of the page, automatically added. 

NativeScript keeps track of your navigation history, so this is built into the framework. There are ways to remove the back button and to tell NativeScript to not track your history; however, I'm not going to cover that here. Check out the [docs](http://docs.nativescript.org/core-concepts/navigation#navigate-without-history) for details. 

For reference, here's the complete code for the `home-page.js` file, including the navigation to the About page.

```javascript
var frameModule = require('ui/frame');

function onTap() 
{
    console.log('onTap called...');
    frameModule.topmost().navigate("about-page");
}
exports.onTap = onTap;
```

<div class="exercise-end"></div>

Go ahead and add buttons to the home page for navigation to the Contact Us and Products pages, then adding the necessary code to navigate to each page. Try it all by yourself first. If you get stuck, look back through the exercises. The code is also included below for reference.

<h4 class="exercise-start">
    <b>Exercise</b>: Navigating to the Contact Us page
</h4>

Add a button to the `home-page.xml` file. 

```xml
<Button text="Contact Us" tap="onTapContactUs" />
```

Add the event handler code in the `home-page.js` file.

```javascript
function onTapContactUs() { 
    frameModule.topmost().navigate("contact-us-page");
}
exports.onTapContactUs = onTapContactUs;
```

<div class="exercise-end"></div>

And now the Products page.

<h4 class="exercise-start">
    <b>Exercise</b>: Navigating to the Products page
</h4>

Add a button to the `home-page.xml` file. 

```xml
<Button text="Products" tap="onTapProducts" />
```

Add the event handler code in the `home-page.js` file.

```javascript
function onTapProducts() { 
    frameModule.topmost().navigate("products-page");
}
exports.onTapProducts = onTapProducts;
```

<div class="exercise-end"></div>
