## Basic UI elements

In this section, you'll be learning aobut some of the basic UI elements that go into NativeScript apps. 

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

Using VS Code, open the tekmo app by using the `Open Folder...` command. You shoudl see the following in VS Code:

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

Modify the `app.js` file to point to the new home page by chaning the starting page from `main-page` to `home-page`:

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

Great work! You've replaced the default template pages wiht your own home page. Now, let's learn a little bit more about pages and UI elements.

### Pages

You've already learned that pages are a collection of similarly-named .xml, .css., and .js files. We'll dig into the .css and .js pages soon enough. Let's focus on the .xml file first.

Pages always begin with a .xml file. In this file, you define the UI by adding adding various XML elements. In many ways, you can think of this file like an HTML file. It has structure, driven by the elements added to it, and then is augmented by external CSS and JavaScript files. 

The first element within a Page is always a `<Page> ... </Page>` element. 

### Labels

Let's learn about another 

### LiveSync makes changes easy

### 