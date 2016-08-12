## Basic UI elements

In this section, you'll be learning about some of the basic UI elements that go into NativeScript apps. 

### What you're building

Over the course of the next several sections, you'll be building a mobile app for Tekmo, an imaginary company that sells retro video games and video game accessories. The app will have 4 pages:

1. Home
2. About 
3. Contact Us
4. Product Listing

### Creating the Tekmo app

Let's get started with the Tekmo app by scaffolding out a new app using the CLI.

<h4 class="exercise-start">
    <b>Exercise</b>: Creating the Tekmo app
</h4>

> In this exercise, you'll be creating a new app named "tekmo" and checking to ensure the app works by running it in the GenyMotion emulator. I'll let you try it by yourself. If you need help, you can follow the directions below.

Change directories back to your Documents folder before creating the Tekmo app.

```
  cd C:\Users\dev\Documents
```

Create the app using `tns create tekmo` CLI command.

```
  tns create tekmo
```

Change directories into the Tekmo app's root directory.

```
  cd tekmo
```

Add the Android platform to the app using the `tns platform add android` command.

```
  tns platform add android
```

Run the app in the GenyMotion emulator.

```
  tns run android --emulator
```

You should see the Tekmo app running in GenyMotion.

![image](images/chapter3/tekmo-app.PNG)

<div class="exercise-end"></div>

### Cleaning up the template

As you've seen, the `tns create` command scaffolds a nifty "hello world" app. But, we don't really need all of that code. Let's clean up the app by removing several things.

<h4 class="exercise-start">
    <b>Exercise</b>: Clean up and create a blank start page
</h4>

> In this exercise, you'll be deleting the current start page, creating a new start page, and changing the `app.js` start page to point to your new home page. We haven't learned about all of these items yet. Get as far as you can before looking ahead. If you need help, you can follow the steps below.

Using VS Code, open the tekmo app by using the `Open Folder...` command. You should see the following in VS Code:

![image](images/chapter3/code-tekmo-1.PNG)

Expand the app folder and delete the existing `main-page` files (`main-page.xml` and `main-page.js`). You should also delete the `main-view-model.js` file: you won't need it.

![image](images/chapter3/code-tekmo-2.PNG)

Create a new page named `home-page.xml`, placing it in the `app` directory.

![image](images/chapter3/code-tekmo-3.PNG)

Inside of the `home-page.xml` file, add the following XML:

```xml
<Page>

</Page>
``` 

Modify the `app.js` file to point to the new home page by changing the starting page from `main-page` to `home-page`:

```javascript
var application = require("application");
application.start({ moduleName: "home-page" });
```

Re-run the app in your emulator using the `tns run` CLI command.

```
  tns run android --emulator
```

When the app runs, it should have a blank page:

![image](images/chapter3/code-tekmo-4.PNG)

<div class="exercise-end"></div>

Great work! You've replaced the default template pages with your own home page. Now, let's learn a little bit more about pages and UI elements.

### Pages

You've already learned that pages are a collection of similarly-named .xml, .css., and .js files. We'll dig into the .css and .js pages soon enough. Let's focus on the .xml file first.

Pages always begin with a .xml file. In this file, you define the UI by adding adding various XML elements. In many ways, you can think of this file like an HTML file. It has structure, driven by the elements added to it, and then is augmented by external CSS and JavaScript files. 

The first element within a Page is always a `<Page> ... </Page>` element. 

### Labels

Let's learn about another UI element, the Label. Labels are used to place text on your screen. 

<h4 class="exercise-start">
    <b>Exercise</b>: Adding text to the home page
</h4>

Start by adding a Label to the `home-page.xml` file in the `<Page> ... </Page>` element.

```xml
  <Label text="Welcome to Tekmo!" />
```

To see the changes in your app, go back to the command line, press `Ctrl-C` to and then `Y` to stop your app running. 

```
  <press Ctrl-C>
  ^CTerminate batch job (Y/N)? Y

  C:\Users\dev\tekmo>
```

Then, run the `tns run` command again to build and run your app within GenyMotion.

```
  tns run android --emulator
```

Your app will reload and show you the home page with the updated text.

![image](images/chapter3/code-tekmo-5.PNG)

<div class="exercise-end"></div>

As you just learned above, you can add text by using the `<Label text="..." />` element. 

Now, let's go ahead an create the About, Contact Us, and Products pages. But before we do that, let's talk about your development process and workflow (which ends up being fairly important). Just like developing HTML applications, NativeScript apps follow a similar development process:

1. You made code changes in an editor or IDE (i.e., VS Code)
2. You compile/build the changes (using `tns run android --emulator`)
3. You review the changes in your app using your emulator (i.e., GenyMotion)

> Hold on...this takes a long time. Ideally I'd like to make changes, then quickly look at them in GenyMotion (without manually running `tns run...` every single time.)

Luckily, there is a better way. Let me introduce you to LiveSync.

### LiveSync makes changes easy

Yes it's true. LiveSync will make your life easier. LiveSync is a component of the NativeScript CLI that listens for changes in your app, then automatically syncs them to a running emulator. Let's try it out.

<h4 class="exercise-start">
    <b>Exercise</b>: Using LiveSync
</h4>

Head back to your command prompt and terminate the `tns run...` command that is running again by pressing `Ctrl-C` to and then `Y`. 

```
  <press Ctrl-C>
  ^CTerminate batch job (Y/N)? Y

  C:\Users\dev\tekmo>
``` 

Now, use the `tns livesync android` command to tell the NativeScript CLI to `--watch` your `app` folder for changes and sync them to your running `--emulator`:

```
  tns livesync android --emulator --watch
```

The output from LiveSync is similar to that of the `tns run...` command, and it will yield the same results: run your app. 

Let's see what happens when you make a change. Head back to VS Code and change the text of the Label in the `home-page.xml` file. 

```xml
  <Label text="Welcome to the Tekmo app!" />
```

As soon as you save the `home-page.xml` file, flip back to GenyMotion to see the changes happen. It may take 2-3 seconds, so be patient. 

![image](images/chapter3/tekmo-livesync.gif)

<div class="exercise-end"></div>

As you can see LiveSync is a powerful CLI tool that can dramatically reduce your dev-build-test workflow.

>From this point forward, use `tns livesync`, as it will same you some time.

### Adding more pages

Let's continue adding the remainder of our app pages: About, Contact Us, and Products. For now, each page should have a label on it with the page's name. I'll let you try it on your own, but if you get stuck or can't remember the exact syntax, you can follow along below.

We haven't learned how to navigate between pages yet, so to test each page, replace the startup page in the `app.js` file. 

<h4 class="exercise-start">
    <b>Exercise</b>: Adding the About page
</h4>

Create an XML file named `about-page.xml` in the root of the `app` folder.

![image](images/chapter3/code-tekmo-6.PNG)

Add the `Page` and `Label` elements to the `about-page.xml` file.

```xml
<Page>
  <Label text="About" />
</Page>
```

To test your page, change the `app.js` file to load the `about-page` page first.

```javascript
var application = require("application");
application.start({ moduleName: "about-page" });
```

Wait for LiveSync to load your changes in GenyMotion.

<div class="exercise-end"></div>

Next, let's add the Contact Us page.

<h4 class="exercise-start">
    <b>Exercise</b>: Adding the Contact Us page
</h4>

Create an XML file named `contact-us-page.xml` in the root of the `app` folder.

![image](images/chapter3/code-tekmo-7.PNG)

Add the `Page` and `Label` elements to the `contact-us-page.xml` file.

```xml
<Page>
  <Label text="Contact Us" />
</Page>
```

To test your page, change the `app.js` file to load the `contact-us-page` page first.

```javascript
var application = require("application");
application.start({ moduleName: "contact-us-page" });
```

Wait for LiveSync to load your changes in GenyMotion.

<div class="exercise-end"></div>

Lastly, add the Products page.

<h4 class="exercise-start">
    <b>Exercise</b>: Adding the Products page
</h4>

Create an XML file named `products-page.xml` in the root of the `app` folder.

![image](images/chapter3/code-tekmo-8.PNG)

Add the `Page` and `Label` elements to the `products-page.xml` file.

```xml
<Page>
  <Label text="Products" />
</Page>
```

To test your page, change the `app.js` file to load the `products-page` page first.

```javascript
var application = require("application");
application.start({ moduleName: "products-page" });
```

Wait for LiveSync to load your changes in GenyMotion.

<div class="exercise-end"></div>