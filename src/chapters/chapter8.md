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

### Styling a grid layout

Next, let's turn our attention to the Products page. It looks pretty bad right now. 

![image](images/chapter8/styling-2.PNG)

As you'll recall the Products page is organized using a grid layout. Styling grid layouts isn't much different than styling other UI elements, so let's dive in.

<h4 class="exercise-start">
    <b>Exercise</b>: Styling a grid layout
</h4>

I'd like to do a few things to clean up the 

<div class="exercise-end"></div>


Outline:
* give the page some background colors
* remove the tile colors
* put some space in between items
* style the heading of super marshmallow man - maybe text, different font, line, etc.
* align the price and give it a colors

### Adding images

In the final part of this chapter, you'll learn how to include images in your NativeScript app. Images and graphics can help turn a "blah" UI into something beautiful. Again, I don't have the talent to do "beautiful", but I'll teach you the basic tools of including images in your app. From there, you can run wild.

#### Challenges in displaying images on mobile devices

Before we start, I want to share some of the challenges ther are with displaying images on mobile devices. First, consider the job of a cross-platform mobile framework (like NativeScript). 

> WARNING: This section may scare you initially, and that's because cross-platform device DPIs are confusing. But don't worry: NativeScript does a good job of abstracting away the complexities of cross-platform images. Stick with me!

There are hundreds of various devices, and each device has a different screen resolution and DPI. Let's take iOS devices as an example. Apple's devices (iPhone, iPad, etc.) are considered to be a highly-controlled hardware ecosystem, resulting in fewer variances across the models of their devices; however, consider just the iPhone line of hardware. iPhone 3, 3G, 4, 4s, 5, 5s, 5c, 6, 6s, 6 plus, etc. Some of these devies share common characteristics (like screen size), but it seems with every new year, the screens change in size, or in DPI. Between all of these devices, there are 3-4 differetn screen sizes, and 2-3 different screen DPIs to consider. 

That's only iOS, the most "controlled" device ecosystem. Android has similar differences, but it's across a much larger variable hardware space. 

I don't want to paint a doom-and-gloom picture for you. There are very well-defined guidelines for displaying images on both iOS and Android platforms, but the true chalenge is that the platforms are different. 

So, what does this mean for you? Unfortunately, a lot. As a cross-platform mobile developer, you should become familiar with the differences in screen DPI and how to create images for the various screen. I'm not going into those differences here, but you can find out more in these places:
* Android screen resolution documentation
* iOS screen resolution documentation
* NativeScript image documentation
* [my website](https://nsimage.brosteins.com) for building NativeScript images 

#### Displaying images in a NativeScript app

There are several ways to display images in a NativeScript app:
* from a url
* from the device's file system
* embdedded in the app as a resource

In this workshop, you'll be learning how to display images embedded in the app as a resource. The other methods are similar, so I'll let you explore them on your own by reading the NativeScript docs.

#### Why NativeScript makes images easy

Just in case you haven't had a chance to read the Android and iOS image/screen DPI docs above, I'll briefly summarize for you. 

Imagine you have a static in-app image named `picture.png` that you'd like to display on devices (Android and iOS). For Android, you'd need to provide 6 different image resolutions, nick-named:
* **ldpi** (0.75x original resolution)
* **mdpi** (1.0x)
* **hdpi** (1.5x) 
* **xhdpi** (2.0x)
* **xxhdpi** (3.0x)
* **xxxhdpi** (4.0x)

On iOS, you'd need to provide 3 image sizes: 
* **@1x** (1.0x original resolution, iPad 2 and iPad mini)
* **@2x** (2.0x, iPhone 4s, iPhone 5, iPhone 6, iPad [retina])
* **@3x** (3.0x, iPhone 6 Plus)

So, you need 9 total images to cover all the bases...ugh! You can't get away from creating all the various image sizes, but there is a declarative way to load the image once, and have NativeScript automatically display the correct image based upon your device and platform.  

Enough explaination, let's start adding some images to the app. 

<h4 class="exercise-start">
    <b>Exercise</b>: Styling titles and text
</h4>

TODO: add content

<div class="exercise-end"></div>