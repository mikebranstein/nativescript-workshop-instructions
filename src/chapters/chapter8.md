## Styling your app

We've spent a lot of time working through the declarative UI elements of a NativeScript app so far. But now it's time to turn back to the styling of the UI. I'll be frank. This app looks pretty bad right now. But, with a few tweaks, we can make it better. I can't promise it'll be the next Mona Lisa, but it will be better.

Styling NativeScript apps is similar to how you may style an HTML application: CSS. That's right, you can use CSS to style your NativeScript app pages.

If you recall from earlier chapters, a NativeScript page has three parts: an XML file, a JavaScript file, and a CSS file. The XML file contains declarative XML code used to structure your app; the JavaScript file contains your business logic code that can interact with your UI; and the CSS file augments the XML file, providing style.

> **NOTE** There is no right or wrong way to style this app we're working with (well, maybe there are some wrong ways...). I'm not a great UI designer, I'm much more of a backend architect and automation developer, so don't take any of my UI styling guidelines here as gospel. If you think something looks better by styling it differently, by all means, do it. If you're specially proud of something, share it with the community.

### Styling basics

Let's get started with some styling basics. Because we're using the Android platform in our workshop, there's something fairly obvious that we need to fix right away. At the top of every page, there's a large area with the app's name *tekmo* displayed. This area is called the *Action Bar*. We need to remove the action bar and we need to do it fast! 

> **NOTE** If you're running the workshop in iOS, this exercise doesn't apply to you, so feel free to skip it.

<h4 class="exercise-start">
    <b>Exercise</b>: Removing the Android action bar
</h4>

To remove the action bar, add the `actionBarHidden="true"` attribute of the `<Page>` element. Add this to each page declaration in your XML files. 

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
* Contact us
* Products

<div class="exercise-end"></div>

Let's take a brief detour and talk about the various CSS files in your project. There are two types of CSS files in a NativeScript app:
1. global (app.css)
2. page-specific (page-name.css)

The app.css file is global to your entire app, so changes you make in the app.css file will apply to every page in your app. 

If you need finer-grained control over your style, then you can create page-specific CSS files. These files are named similarly to the XML and JavaScript files, just with a different extension. 

The beauty of NativeScript CSS styles is that you don't have to remember to include references to your style files on your pages. NativeScript will automatically load the files for you (as long as they're named per the page-naming conventions we've discussed above.)

#### Inline style application

In addition to applying styles by using CSS files, you can apply styles directly to UI elements. You've seen this before when we applied the various background colors to grid cells on the Products page of the Tekmo app. See the [NativeScript inline styling documentation](https://docs.nativescript.org/ui/styling#inline-css) for more information.

#### Supported CSS properties

As I've said before, NativeScript styling is a subset of CSS styling, meaning that not every CSS property is available. For a detailed list of supported properties, check out the official NativeScript documentation on [CSS and styling](https://docs.nativescript.org/ui/styling).

#### CSS selectors

Just as in HTML applications, NativeScript can use CSS selectors to select a single element by id, a group of items by element tag name, a group of elements by class name, and a few other methods. To see the complete listing, check out the [NativeScript styling documentation](https://docs.nativescript.org/ui/styling#supported-selectors). I'm going to stick with the basic (id, class name, and XML tag name) in the workshop, but you're free to explore further on your own.

With this basic knowledge, let's get started styling our app with CSS.

> **NOTE** This is where the power of LiveSync really shines. Constant tweaks to page styling is made easy if you're using LiveSync. 

<h4 class="exercise-start">
    <b>Exercise</b>: Styling titles and text
</h4>

Another piece of low-hanging fruit is styling the titles on pages and the general purpose text we have on each page. Let's start with the titles.

I'd like to make the page titles larger and centered on pages, when they're present. Because titles appear on multiple pages, it makes sense to place a single CSS style rule in the `app.css` file for titles. 

Let's look in the `app.css` file to get started. You'll notice that the default app template for NativeScript apps already includes some CSS for elements with the *title* class. 

```css
.title {
    font-size: 30;
    horizontal-align: center;
    margin: 20;
}
```

We don't need to tweak the settings, so let's go through and apply the *title* class to the following pages. You can do this by adding a `class="title"` property to the `<Label>` elements that should be considered titles:
* Home
* About 
* Contact Us
* Products

After changing the various pages now have a prominent title with ample rooms between the title and the following page content.

![image](images/chapter8/nav-1.gif)

I see a few things that should also be changed:
* fix home page title text wrapping
* adjust normal text to give a bit of a left/right/bottom margin (app-wide) 
* add sub-title class for sub titles on the About page
* shrink the buttons - they're **HUGE**

I'm going to walk through these changes, but go ahead and try this on your own. 

Fix the home page text wrapping. (I chose to enable text wrapping and shorten the text.)

```xml
<Label textWrap="true" text="Welcome to Tekmo!" />
```

Add a left, right, and bottom margin to all text by styling all labels to have a margin of 10 pixels. (I added this to the `app.css` file to make the change globally.)

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

Change the `button` selector definition in the global `app.css` file to make the buttons appear more reasonably-sized. I couldn't decide what the *right* font size for buttons was, so I just removed the button `font-size` property.

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

I'd like to do a few things to clean up the Products page and the rest of the app:
* give all app pages a default background color instead of white 
* remove the alternating tile colors
* color the tiles white and put some space between them, so we can visually tell where one tile ends and another begins
* put a band of color across the top of each tile for the title 
* style the tile titles to stand out against the solid tile background
* right-align the price and give it color to stand out
* style the highlighted product a little different from the other tiles to make it stand out

That's a lot of changes. Feel free to try the changes on your own, or follow along with me. If your end product doesn't look exactly like mine, that's OK.

Let's start by giving all app pages a default background color instead of white. Add a `background-color` property to the `app.css` file.

```
Page {
    background-color: #EFEFEF;
}
```  

Remove the alternating tile backgrounds from the Products page by deleting the inline style attributes from each stack layout in the grid layout. The grid layout should look like this:

```xml
<GridLayout rows="*,*,*,*" columns="*,*" width="300" height="600">
    <StackLayout row="0" col="0" colSpan="2">
        <Label text="Super Marshmallow Man" textWrap="true" />
        <Label textWrap="true" text="Escape from certain death int his wild adventure!" />
        <Label text="$34.99" />
    </StackLayout>
    <StackLayout row="1" col="0">
        <Label text="Couch Commander" textWrap="true" /> 
        <Label text="$24.99" />
    </StackLayout>
    <StackLayout row="1" col="1">
        <Label text="Mummy Madness" textWrap="true" /> 
        <Label text="$32.99" />
    </StackLayout>
    <StackLayout row="2" col="0">
        <Label text="Pyro Robots" textWrap="true" /> 
        <Label text="$19.99" />
    </StackLayout>
    <StackLayout row="2" col="1">
        <Label text="Rescue Pups" textWrap="true" /> 
        <Label text="$9.99" />
    </StackLayout>
    <StackLayout row="3" col="0">
        <Label text="Vampire Valkyrie" textWrap="true" /> 
        <Label text="$21.99" />
    </StackLayout>            
</GridLayout>
```

The Products page should look pretty plain now:

![image](images/chapter8/styling-3.PNG)

Set the background color of the tiles to white and put some space in between the tiles so we can tell where one tile ends and another begins. I chose to set this in a page-specific CSS file because the tiles are specific to the Products page. Create a file named `products-page.css` file first, then add the `tile` class selector properties.

```
.tile {
    background-color: #FFFFFF;
    margin: 5;
}
```

Apply the `tile` class to each of the stack layouts.  

```xml
<GridLayout rows="*,*,*,*" columns="*,*" width="300" height="600">
    <StackLayout row="0" col="0" colSpan="2" class="tile">
        <Label text="Super Marshmallow Man" textWrap="true" />
        <Label textWrap="true" text="Escape from certain death in this wild adventure!" />
        <Label text="$34.99" />
    </StackLayout>
    <StackLayout row="1" col="0" class="tile">
        <Label text="Couch Commander" textWrap="true" /> 
        <Label text="$24.99" />
    </StackLayout>
    <StackLayout row="1" col="1" class="tile">
        <Label text="Mummy Madness" textWrap="true" /> 
        <Label text="$32.99" />
    </StackLayout>
    <StackLayout row="2" col="0" class="tile">
        <Label text="Pyro Robots" textWrap="true" /> 
        <Label text="$19.99" />
    </StackLayout>
    <StackLayout row="2" col="1" class="tile">
        <Label text="Rescue Pups" textWrap="true" /> 
        <Label text="$9.99" />
    </StackLayout>
    <StackLayout row="3" col="0" class="tile">
        <Label text="Vampire Valkyrie" textWrap="true" /> 
        <Label text="$21.99" />
    </StackLayout>            
</GridLayout>
```

![image](images/chapter8/styling-4.PNG)

Add a band of color across the top of each tile, and place the tile title inside of the band. To do this, I wrapped the title with another stack layout, added the `title` class to the stack layout, and set the background color of the stack layout.

```xml
<GridLayout rows="*,*,*,*" columns="*,*" width="300" height="600">
    <StackLayout row="0" col="0" colSpan="2" class="tile">
        <StackLayout class="tile-title">
            <Label text="Super Marshmallow Man" textWrap="true" />
        </StackLayout>
        <Label textWrap="true" text="Escape from certain death in this wild adventure!" />
        <Label text="$34.99" />
    </StackLayout>
    <StackLayout row="1" col="0" class="tile">
        <StackLayout class="tile-title">
            <Label text="Couch Commander" textWrap="true" /> 
        </StackLayout>
        <Label text="$24.99" />
    </StackLayout>
    <StackLayout row="1" col="1" class="tile">
        <StackLayout class="tile-title">
            <Label text="Mummy Madness" textWrap="true" /> 
        </StackLayout>
        <Label text="$32.99" />
    </StackLayout>
    <StackLayout row="2" col="0" class="tile">
        <StackLayout class="tile-title">
            <Label text="Pyro Robots" textWrap="true" /> 
        </StackLayout>
        <Label text="$19.99" />
    </StackLayout>
    <StackLayout row="2" col="1" class="tile">
        <StackLayout class="tile-title">
            <Label text="Rescue Pups" textWrap="true" /> 
        </StackLayout>
        <Label text="$9.99" />
    </StackLayout>
    <StackLayout row="3" col="0" class="tile">
        <StackLayout class="tile-title">
            <Label text="Vampire Valkyrie" textWrap="true" /> 
        </StackLayout>
        <Label text="$21.99" />
    </StackLayout>            
</GridLayout>
```

Add the style to the page-specific CSS file:

```
.tile-title {
    background-color: #99ccff;
}
```

> **NOTE** There are likely other ways of adding a band of color around a label, but this was a quick way to get what I wanted accomplished.

![image](images/chapter8/styling-5.PNG)

Change the tile titles a little to increase the font size, set the color to black, and increase top margin by a few pixels. This should also be added to the `products-page.css` file.

```
.tile-title Label {
    font-size: 14;
    color: black;
    margin-top: 5;
}
```

![image](images/chapter8/styling-6.PNG) 

Make the price stand out a bit more by changing the color and right-aligning it within the stack layout. This CSS addition can also go in the `products-page.css` file. 

```
.price {
    color: #009933;
    text-align: right;
}
```

Target the prices by adding a `price` class to each pricing label on the Products page.

```xml
<GridLayout rows="*,*,*,*" columns="*,*" width="300" height="600">
    <StackLayout row="0" col="0" colSpan="2" class="tile">
        <StackLayout class="tile-title">
            <Label text="Super Marshmallow Man" textWrap="true" />
        </StackLayout>
        <Label textWrap="true" text="Escape from certain death int his wild adventure!" />
        <Label text="$34.99" class="price" />
    </StackLayout>
    <StackLayout row="1" col="0" class="tile">
        <StackLayout class="tile-title">
            <Label text="Couch Commander" textWrap="true" /> 
        </StackLayout>
        <Label text="$24.99" class="price" />
    </StackLayout>
    <StackLayout row="1" col="1" class="tile">
        <StackLayout class="tile-title">
            <Label text="Mummy Madness" textWrap="true" /> 
        </StackLayout>
        <Label text="$32.99" class="price" />
    </StackLayout>
    <StackLayout row="2" col="0" class="tile">
        <StackLayout class="tile-title">
            <Label text="Pyro Robots" textWrap="true" /> 
        </StackLayout>
        <Label text="$19.99" class="price" />
    </StackLayout>
    <StackLayout row="2" col="1" class="tile">
        <StackLayout class="tile-title">
            <Label text="Rescue Pups" textWrap="true" /> 
        </StackLayout>
        <Label text="$9.99" class="price" />
    </StackLayout>
    <StackLayout row="3" col="0" class="tile">
        <StackLayout class="tile-title">
            <Label text="Vampire Valkyrie" textWrap="true" /> 
        </StackLayout>
        <Label text="$21.99" class="price" />
    </StackLayout>            
</GridLayout>
```

![image](images/chapter8/styling-7.PNG) 

Lastly, let's slightly change the highlighted tile a bit to make it stand apart from the other tiles. Add the following CSS selectors to the `product-page.css` file.

```
.highlight .tile-title {
    font-weight: bold;
    background-color: #6699ff;
}

.highlight .tile-title Label {
    font-size: 18;
}

.highlight .price {
    font-weight: bold;
    color: red;
}
```

![image](images/chapter8/styling-8.PNG) 
 
<div class="exercise-end"></div>

That's a pretty radical change, and it wasn't too hard to do. Again, you're likely more creative than I am, so go forth and be artistic. 

### Adding images

In the final part of this chapter, you'll learn how to include images in your NativeScript app. Images and graphics can help turn a "blah" UI into something beautiful. Again, I don't have the talent to do "beautiful", but I'll teach you the basic tools of including images in your app. From there, you can run wild.

#### Challenges in displaying images on mobile devices

Before we start, I want to share some of the challenges there are with displaying images on mobile devices. First, consider the job of a cross-platform mobile framework (like NativeScript). 

> **WARNING** This section may scare you initially, and that's because cross-platform device DPIs are confusing. But don't worry: NativeScript does a good job of abstracting away the complexities of cross-platform images. Stick with me!

There are hundreds of various devices, and each device has a different screen resolution and DPI. Let's take iOS devices as an example. Apple's devices (iPhone, iPad, etc.) are considered to be a highly-controlled hardware ecosystem, resulting in fewer variances across the models of their devices; however, consider just the iPhone line of hardware. iPhone 3, 3G, 4, 4s, 5, 5s, 5c, 6, 6s, 6 plus, etc. Some of these devices share common characteristics (like screen size), but it seems with every new year, the screens change in size, or in DPI. Between all of these devices, there are 3-4 different screen sizes, and 2-3 different screen DPIs to consider. 

That's only iOS, the most "controlled" device ecosystem. Android has similar differences, but it's across a much larger variable hardware space. 

I don't want to paint a doom-and-gloom picture for you. There are very well-defined guidelines for displaying images on both iOS and Android platforms, but the true challenge is that the platforms are different. 

So, what does this mean for you? Unfortunately, a lot. As a cross-platform mobile developer, you should become familiar with the differences in screen DPI and how to create images for the various screen. I'm not going into those differences here, but you can find out more in these places:
* Android screen resolution [documentation](http://developer.android.com/guide/practices/screens_support.html#DesigningResources)
* iOS screen resolution [documentation](https://developer.apple.com/ios/human-interface-guidelines/graphics/app-icon/#//apple_ref/doc/uid/TP40006556-CH27-SW1)
* NativeScript image [documentation](https://docs.nativescript.org/ui/ui-images)
* [my website](http://nsimage.brosteins.com) for building NativeScript images 

#### Displaying images in a NativeScript app

There are several ways to display images in a NativeScript app:
* from a URL
* from the device's file system
* embedded in the app as a resource

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

So, you need 9 total images to cover all the bases...ugh! But, I've already solved that problem for you with my website, [NativeScript Image Builder](http://nsimage.brosteins.com). If you have a high-resolution image for your app, upload it to my site and I'll do all of the image building magic for you and ship the images back to you in a .ZIP file. 

You can't get away from creating all the various image sizes, but there is a declarative way to load the image once, and have NativeScript automatically display the correct image based upon your device and platform.  

Enough explaination, let's start adding some images to the app. 

<h4 class="exercise-start">
    <b>Exercise</b>: Adding images to the products page
</h4>

The first thing we need is images for each game. My friend [David Bjarnson](https://twitter.com/outerfield), was kind enough to draw up some quick images for each game. 

[Download](images/chapter8/tekmo-images.zip) the app images and unzip the contents. Inside, you'll find 2 folders: Android and iOS. Copy the contents of these folders into the `app/App_Resources/Android` and `app/App_Resources/iOS` folder of the Tekmo mobile app. Now, there are a lot of sub-directories under these folders if you copy and paste, merge the files in the sub-directories, don't jsut replace your existing Android and iOS folders. 

You can checkout each of the images by clicking on them in VS Code:

![](images/chapter8/smm.png)
![](images/chapter8/cc.png)
![](images/chapter8/mm.png)
![](images/chapter8/pr.png)
![](images/chapter8/rp.png)
![](images/chapter8/vv.png)

Add them to the products page by using the `<Image />` element. 

```xml
<GridLayout rows="*,*,*,*" columns="*,*" width="300" height="600">
    <StackLayout row="0" col="0" colSpan="2" class="tile">
        <StackLayout class="tile-title">
            <Label text="Super Marshmallow Man" textWrap="true" />
        </StackLayout>
        <Image src="res://super-marshmallow-man" />
        <Label textWrap="true" text="Escape from certain death int his wild adventure!" />
        <Label text="$34.99" class="price" />
    </StackLayout>
    <StackLayout row="1" col="0" class="tile">
        <StackLayout class="tile-title">
            <Label text="Couch Commander" textWrap="true" /> 
        </StackLayout>
        <Image src="res://couch-commander" />
        <Label text="$24.99" class="price" />
    </StackLayout>
    <StackLayout row="1" col="1" class="tile">
        <StackLayout class="tile-title">
            <Label text="Mummy Madness" textWrap="true" /> 
        </StackLayout>
        <Image src="res://mummu-madness" />
        <Label text="$32.99" class="price" />
    </StackLayout>
    <StackLayout row="2" col="0" class="tile">
        <StackLayout class="tile-title">
            <Label text="Pyro Robots" textWrap="true" /> 
        </StackLayout>
        <Image src="res://pyro-robots" />
        <Label text="$19.99" class="price" />
    </StackLayout>
    <StackLayout row="2" col="1" class="tile">
        <StackLayout class="tile-title">
            <Label text="Rescue Pups" textWrap="true" /> 
        </StackLayout>
        <Image src="res://rescue-pups" />
        <Label text="$9.99" class="price" />
    </StackLayout>
    <StackLayout row="3" col="0" class="tile">
        <StackLayout class="tile-title">
            <Label text="Vampire Valkyrie" textWrap="true" /> 
        </StackLayout>
        <Image src="res://vampire-valkyrie" />
        <Label text="$21.99" class="price" />
    </StackLayout>            
</GridLayout>
```

Also adjust the image width and height to a reasonable size on the emulator scereen.

```
Image {
    width: 80;
    height: 80;
}
```

![image](images/chapter8/styling-9.PNG) 

This looks OK, but now the Super Marshmallow Man text and price has fallen out of the tile. Ideally, I'd like the image to be left-aligned, then the description and price right-aligned. 

There are a variety of ways to do this. Two ways at the top of my head are to add another grid layout for this tile, or use a series of nested stack layouts. Let's use the stack layout method because it will introduce you to another property of the stack layout: orientation. The orientation property of the stack layout tells NativeScript whether to render the layout's contents vertically or horizontally. By default it is rendered vertically. Change the Super Marshmallow Man tile's code to add a series of nested stack layouts.

```xml
<StackLayout row="0" col="0" colSpan="2" class="tile">
    <StackLayout class="tile-title">
        <Label text="Super Marshmallow Man" textWrap="true" />
    </StackLayout>
    <StackLayout orientation="horizontal">
        <Image src="res://smm" />
        <StackLayout>
            <Label textWrap="true" text="Escape from certain death int his wild adventure!" />
            <Label text="$34.99" class="price" />
        </StackLayout>
    </StackLayout>
</StackLayout>
```

Also increase the size of the highlight image.

```
.highlight Image {
    width: 100;
    height 100;
}
```

Looks good.

![image](images/chapter8/styling-10.PNG)

That's all I'm going to tweak for now, but you can continue on your own if you'd like. 

<div class="exercise-end"></div>

This concludes our work on the Tekmo mobile app. It's basic, but thinking back, you've learned a lot with this simple little app.