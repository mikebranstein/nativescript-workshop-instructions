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

Go to the `home-page`, and add a `<StackLayout> element to the page, directly within the `<Page>` element. Move the exisitng `<Label />` element inside of the `<StackLayout>`.

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

Add another `<Label />` element and observer the changes.

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

But wait! Do you see the text you just added. It's running off the side of the page. 

> NOTE: By default, text within a `<Label />` element does not wrap to new lines.

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

Next, add a `tap` event atribute to the `<Button />` element. Most UI elements have a variety of *events* that can execute JavaScript code when triggered. When an event it triggered, it will automatically run the funciton name specified in the event attribute. 

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

If you recall from an earlier section, you learned that NativeScript pages are a colleciton of XML, CSS, and JavaScript files, linked together by their naming convention. 

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

Wait for your app to relead in GenyMotion, then click the `About` button. You should see the text *onTap called...* output to your command line.

![image](images/chapter4/tekmo-on-tap.gif)

<div class="exercise-end"></div>
  
### Navigating to another page

TODO NEXT