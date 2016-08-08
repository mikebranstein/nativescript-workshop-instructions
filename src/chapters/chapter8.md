## Styling your app

We've spent a lot of time working through the declarative UI elements of a NativeScript app so far. But now it's time to turn back to the styling of the UI. I'll be frank. This app looks pretty bad right now. But, with a few tweaks, we can make it better. I can't promise it'll be the next Mona Lisa, but it will be better.

Styling NativeScript apps is similar to how you may style an HTML application: CSS. That's right, you can use CSS to style your NativeScript app pages. 

If you recall from earlier chapters, a NativeScript page has three parts: an XML file, a JavaScript file, and a CSS file. The XML file contains declarative XML code used to structure your app; the JavaScript file contains your business logic code that can interact with your UI; and the CSS file augments the XML file, providing style.

> NOTE: There is no right or wrong way to style this app we're working with (well, maybe there are some wrong ways...). I'm not a great UI designer, I'm much more of a backend architect and automation developer, so don't take any of my UI styling guidelines here as gospel. If you think something looks better by styling it differently, by all means, do it. If you're esepcially proud of something, share it with the community.

### Styling basics

Let's get started with some styling basics. Because we're using the Android platform in our workshop, there's something fairly obvious that we need to fix right away. At the top of every page, there's a large area with the app's name *tekmo* displayed. This area is called the *Action Bar*. We need to remove the action bar and we need to do it fast! 

> NOTE: If you're running the workshop in iOS, this excercise doesn't apply to you, so feel free to skip it.

<h4 class="exercise-start">
    <b>Exercise</b>: Removing the Android action bar
</h4>

To remove the action bar, add the `actionBarHidden="true"` attribute of the `<Page>` element. Add thsi to each page declaration in your XML files. 

Starting with `home-page.xml`, add the attribute to the `<Page>` element.

```xml
<Page actionBarHidden="true">
...
</Page>
```

As you can see, the action bar has been removed from the top of the app. 

![image](images/chapter8/styling-1.PNG)

Do the same thing for the remainder of the pages within the Tekmo app:
* About
* Contact use
* Products

<div class="exercise-end"></div>

Let's take a breif detour and talk about the various CSS files in your project. There are two types of CSS files in a NativeScript app:
1. global (app.css)
2. page-specific (page-name.css)

The app.css file is global to your entire app, so changes you make in the app.css file will apply to every page in your app. 

If you need finer-grained control over your style, then you can ceate page-specific CSS files. These files are named similarly to the XML and JavaScript files, just with a different extension. 

The beauty of NativeScript CSS styles is that you don't have to remember to include references to your style files on your pages. NativeScript will automatically load the files for you (as long as they're named per the page-naming conventions we've discussed above.)

#### Inline style application

In addition to applying styles by using CSS files, you can apply styles directly to UI elements. You've seen this before when we applied the various background colors to grid cells on the Products page of the Tekmo app. See the [NativeScript inline styling documentation](https://docs.nativescript.org/ui/styling#inline-css) for more information.

#### Supported CSS properties

As I've said before, NativeScript styling is a subset of CSS styling, meaning that not every CSS property is available. For a detailed list of supported properties, check out the official NativeScript documentation on [CSS and styling](https://docs.nativescript.org/ui/styling).

#### CSS selectors

Just as in HTML applications, NativeScript can use CSS selectors to select a single element by id, a group of items by element tag name, a group of elements by class name, and a few other methods. To see the complete listing, check out the [NativeScript styling documentation](https://docs.nativescript.org/ui/styling#supported-selectors). I'm going to stick with the basic (id, class name, and XML tag name) in the workshop, but you're free to explore further on your own.

With this basic knowledge, let's get started styling our app with CSS.

> NOTE: This is where the power of LiveSync really shines. Constant tweaks to page styling is made easy if you're using LiveSync. 

<h4 class="exercise-start">
    <b>Exercise</b>: Styling titles and text
</h4>

Another piece of low-hanging fruit is styling the titles on pages and the general purpose text we have on each page. Let's start with the titles.

I'd like to make the page titles larger and centerd on pages, when they're present. Because titles appear on multiple pages, it makes sense to place a single CSS style rule in the `app.css` file for titles. 

Let's look in the `app.css` file to get started. You'll notice that the default app template for NativeScript apps already includes some CSS for elements with the *title* class. 

```css
.title {
    font-size: 30;
    horizontal-align: center;
    margin: 20;
}
```

We don't need to tweek the settings, so let's go through and apply the *title* class to the following pages. You can do this by adding a `class="title"` property to the `<Label>` elements that should be considered titles:
* Home
* About 
* Contact Us
* Products

After changing the various pages now have a prominent title with ample rooms between the title and the following page content.

![image](images/chapter8/nav-1.gif)

I see a few things that should also be changed:
* fix home page title text wrapping
* adjust normal text to give a bit of a left/right/botton margin (app-wide) 
* add sub-title class for sub titles on the About page
* shrink the buttons - they're **HUGE**

I'm going to walk through these changes, but go ahead and try this on your own. 

Fix the home page text wrapping. (I chose to enable text wrapping and shorten the text.)

```xml
<Label textWrap="true" text="Welcome to Tekmo!" />
```

Add a left, right, and bottom margin to all text by styling all labels to have a margin of 10 pixels. (I added this to the `app.css` file to make the change globally.) While

```css
Label {
    margin-left: 10;
    margin-right: 10;
    margin-bottom: 10;
}
```

Add a sub-title class for sub-titled text (especially on the About page).

```css
.sub-title {
    font-size: 20;
}
```

Add the `.sub-title` class name to the sub titles on the About page.

```xml
<Label text="Our Mission" class="sub-title" />

<Label text="History" class="sub-title" />
```

Change the `button` selector definition in the global `app.css` file to make the buttons appear more reasonably-sized.mI couldn't decide what the *right* font size for buttons was, so I just removed the button `font-size` property.

```css
button {
    horizontal-align: center;
}
```

It looks a little better now. 

![image](images/chapter8/nav-2.gif)

<div class="exercise-end"></div>
