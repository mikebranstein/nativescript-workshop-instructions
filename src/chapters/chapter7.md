## Building a complex UI

I've been using the stack layout a lot in the workshop thus far, but it's not from a lack of creativity. The stack layout can hold it's own: it's concise and simple to use. But, sometimes, you need something a little more flexible. After all, the stack layout can only organize UI elements in a stack-like formation: one on top of (or below) another.

In this chapter, we're going to be learning about the grid layout, another layout that allows you to organize your UI using a grid. You'll be learn about the grid layout by building out the final page of the Tekmo app: the Products page. 

The Products page will have a grid of products listed down the page, with a heading at the top. Each game displayed will show it's name and price. In later chapters, we'll be adding an image for each game.

### Building a grid of products

We'll start by building a basic grid, then slowly modifying it to highlight some of the features of the grid layout. 

<h4 class="exercise-start">
    <b>Exercise</b>: Starting fresh
</h4>

Let's start by clearing out the Products page, adding a scroll view, stack layout, label indicating with the text of "Our Products". I'll let you try this by yourself. If you get stuck, you can follow along below or reference the previous exercises. 

Add the `<Page>`, `<ScrollView>`, `<StackLayout>`, and `<Label>` elements to the `products-page.xml` file. 

```xml
<Page>
    <ScrollView>
        <StackLayout>
            <Label text="Our Products" />
        </StackLayout>
    </ScrollView>
</Page>
```

Almost automatically, I start most of my NativeScript pages with a scroll view and stack layout. It's always a good starting point, because I'm likely to have scrolling content and the need to stack UI elements on top of each other.

After adding these elements, your page should like like so:

![image](images/chapter7/products-1.PNG)

<div class="exercise-end"></div>

Right now, you may be a bit confused and wondering where the grid layout is going to go. We've already added a stack layout, so how can I add a grid layout. Here's the secret (although it's not such a big secret): you can nest layouts. So, we'll be adding the grid layout right below the label. Thinking through the page's overall layout, it will begin with UI elements being organized in a vertical stack, then after the top label, we'll be organizing elements with a grid.

It might be hard to visualize right now, but once you get the code up and running in your emulator, it'll become clearer.

<h4 class="exercise-start">
    <b>Exercise</b>: Adding a grid layout
</h4>

Tekmo has 6 vintage games that it sells:
* Super Marshmallow Man
* Couch Commander
* Mummy Madness
* Pyro Robots
* Rescue Pups
* Vampire Valkyrie

Let's plan on having the games displayed in a 2 x 3 grid, 2 columns wide, and 3 rows high.

Add a `<GridLayout> ... </GridLayout>` element beneath the label in the `products-page.xml` file. When you add a grid layout, you need to plan for the number of rows and columns, so we'll also declare the grid layout to support 3 rows and 2 columns. Finally, I'm going to lock down the size of the grid layout to be 300 pixels wide by 450 pixels tall. 

```xml
<GridLayout rows="*,*,*" columns="*,*" width="300" height="450">

</GridLayout>
```

Grid rows and columns are defined by adding comma-separated values to the `rows` and `columns` properties of the grid layout. Each comma-separated value represents a row or column. As you can see, `rows="*,*,*"` and `columns="*,*"` means the grid has 3 rows and 2 columns, totaling to 6 grid cells.

The grid layout can be both simple and yet complex depending upon how to define the number of rows and columns. It's possible to specify the size of rows and columns by an exact pixel value, a proportion of the grid space, and proportionately to the size of other rows and columns. I'm not going to go into the details of how to do all of these things here. If you're interested in the details, I cover this topic in great detail in [NativeScript in Action](http://bit.ly/nsinaction).

So, what do the stars really mean? It's a bit complicated, but the simple answer is that each row and column will be distributed evenly over the grid layout's size. So, with 3 rows and a height of 450 pixels, each row will be 150 pixels tall. This also means the 2 columns are evenly distributed over the 300 pixels of width, resulting in columns with a width of 150 pixels. 

Putting it together, we have 6 grid cells, each 150 x 150 pixels in width and height. Funny how that worked out perfectly, right?

<div class="exercise-end"></div>

You won't be able to see this layout until we add content to the grid layout, so let's press forward.

<h4 class="exercise-start">
    <b>Exercise</b>: Adding content to a grid layout
</h4>

As I said before, I want a game title and price listed for each game. Thinking aloud, this sounds a lot like two separate UI elements, perhaps even two labels for each game. Do you know of any ways to organize multiple UI elements? Oh that's right: a stack layout. 

I'm going to let you try this next step on your own. Add 6 stack layouts to the grid layout. Each stack layout will have 2 labels inside: a label for the game's name, and a label for the game's price. Here's the game names and prices to use. If you get stuck, follow along below, but try to do this from memory (or look back at a previous exercise).

Tekmo has 6 vintage games that it sells:
* Super Marshmallow Man, $34.99
* Couch Commander, $24.99
* Mummy Madness, $32.99
* Pyro Robots, $19.99
* Rescue Pups, $9.99
* Vampire Valkyrie, $21.99

Add Super Marshmallow Man to the grid layout, by placing two `<Label>` elements inside of a `<StackLayout>` that is nested underneath the GridLayout.

```xml
<StackLayout>
    <Label text="Super Marshmallow Man" textWrap="true" />
    <Label text="$34.99" />
</StackLayout>
```

Add the remaining in the same way.

```xml
<StackLayout>
    <Label text="Couch Commander" textWrap="true" /> 
    <Label text="$24.99" />
</StackLayout>
<StackLayout>
    <Label text="Mummy Madness" textWrap="true" /> 
    <Label text="$32.99" />
</StackLayout>
<StackLayout>
    <Label text="Pyro Robots" textWrap="true" /> 
    <Label text="$19.99" />
</StackLayout>
<StackLayout>
    <Label text="Rescue Pups" textWrap="true" /> 
    <Label text="$9.99" />
</StackLayout>
<StackLayout>
    <Label text="Vampire Valkyrie" textWrap="true" /> 
    <Label text="$21.99" />
</StackLayout>
```

Let's checkout the products page in your emulator and see the results.

![image](images/chapter7/products-2.PNG)

<div class="exercise-end"></div>

Oh dear! What the heck happened?

It looks like each stack layout is positioned on top of each other. What did we forget?

> **NOTE** UI elements in a grid layout need to specify which row and column they belong to. 

<h4 class="exercise-start">
    <b>Exercise</b>: Positioning elements in a grid layout 
</h4>

Let's fix this problem by assigning a `row` and `col` property to each stack layout. The updated stack layouts should look like this:

```xml
<StackLayout row="0" col="0">
    <Label text="Super Marshmallow Man" textWrap="true" />
    <Label text="$34.99" />
</StackLayout>
<StackLayout row="0" col="1">
    <Label text="Couch Commander" textWrap="true" /> 
    <Label text="$24.99" />
</StackLayout>
<StackLayout row="1" col="0">
    <Label text="Mummy Madness" textWrap="true" /> 
    <Label text="$32.99" />
</StackLayout>
<StackLayout row="1" col="1">
    <Label text="Pyro Robots" textWrap="true" /> 
    <Label text="$19.99" />
</StackLayout>
<StackLayout row="2" col="0">
    <Label text="Rescue Pups" textWrap="true" /> 
    <Label text="$9.99" />
</StackLayout>
<StackLayout row="2" col="1">
    <Label text="Vampire Valkyrie" textWrap="true" /> 
    <Label text="$21.99" />
</StackLayout>
```

Let's check if that fixed the issue in our emulator.

![image](images/chapter7/products-3.PNG)

Yep, it did. But it's really hard to tell where each grid cell begins and ends. I can *kind of* tell that it's in a grid, but it's not really clear. 

Let's fix that by cheating a little bit. You won't learn about this for a few more chapters, but it's worth doing now to make it easier to see.

Add an alternating CSS style to each stack layout, so we can see the grid cells better. 

> **NOTE** Yeah, I said add a CSS style. NativeScript isn't HTML, but a subset of CSS can be used to style your apps. You'll learn more later, so just follow along for now.

```xml
<StackLayout row="0" col="0" style="background-color: #EEEEEE;">
    <Label text="Super Marshmallow Man" textWrap="true" />
    <Label text="$34.99" />
</StackLayout>
<StackLayout row="0" col="1" style="background-color: #CCCCCC;">
    <Label text="Couch Commander" textWrap="true" /> 
    <Label text="$24.99" />
</StackLayout>
<StackLayout row="1" col="0" style="background-color: #CCCCCC;">
    <Label text="Mummy Madness" textWrap="true" /> 
    <Label text="$32.99" />
</StackLayout>
<StackLayout row="1" col="1" style="background-color: #EEEEEE;">
    <Label text="Pyro Robots" textWrap="true" /> 
    <Label text="$19.99" />
</StackLayout>
<StackLayout row="2" col="0" style="background-color: #EEEEEE;">
    <Label text="Rescue Pups" textWrap="true" /> 
    <Label text="$9.99" />
</StackLayout>
<StackLayout row="2" col="1" style="background-color: #CCCCCC;">
    <Label text="Vampire Valkyrie" textWrap="true" /> 
    <Label text="$21.99" />
</StackLayout>
```

Now, let's check your emulator. 

![image](images/chapter7/products-4.PNG)

Much better! You can really see the grid now. 

For reference, here's the complete code listing for the Products page.

```xml
<Page>
    <ScrollView>
        <StackLayout>
            <Label text="Our Products" />
            <GridLayout rows="*,*,*" columns="*,*" width="300" height="450">
                <StackLayout row="0" col="0" style="background-color: #EEEEEE;">
                    <Label text="Super Marshmallow Man" textWrap="true" />
                    <Label text="$34.99" />
                </StackLayout>
                <StackLayout row="0" col="1" style="background-color: #CCCCCC;">
                    <Label text="Couch Commander" textWrap="true" /> 
                    <Label text="$24.99" />
                </StackLayout>
                <StackLayout row="1" col="0" style="background-color: #CCCCCC;">
                    <Label text="Mummy Madness" textWrap="true" /> 
                    <Label text="$32.99" />
                </StackLayout>
                <StackLayout row="1" col="1" style="background-color: #EEEEEE;">
                    <Label text="Pyro Robots" textWrap="true" /> 
                    <Label text="$19.99" />
                </StackLayout>
                <StackLayout row="2" col="0" style="background-color: #EEEEEE;">
                    <Label text="Rescue Pups" textWrap="true" /> 
                    <Label text="$9.99" />
                </StackLayout>
                <StackLayout row="2" col="1" style="background-color: #CCCCCC;">
                    <Label text="Vampire Valkyrie" textWrap="true" /> 
                    <Label text="$21.99" />
                </StackLayout>
            </GridLayout>
        </StackLayout>
    </ScrollView>
</Page>
```

<div class="exercise-end"></div>

### Refactoring for a special promotion

I could stop here with the grid layout, but that wouldn't be much fun. Let's do one more thing. 

After talking with Tekmo, I've just realized that want to highlight Super Marshmallow Man, by placing it front and center on the Products page. Right now it's lost a little bit. Tekmo would like a larger tile at the top of the page, highlighting Super Marshmallow Man. The tile should have a brief description of the game while also advertizing a sale price of $14.99: $20 off!

<h4 class="exercise-start">
    <b>Exercise</b>: Spanning grid cells 
</h4>

The grid layout is a flexible layout because you can also have UI elements span multiple rows and columns by using the `rowSpan` and `colSpan` properties. 

Set the Super Marshmallow Man tile to span two columns by using the `colSpan="2"` property.

```xml
<StackLayout row="0" col="0" colSpan="2" style="background-color: #EEEEEE;">
    <Label text="Super Marshmallow Man" textWrap="true" />
    <Label text="$34.99" />
</StackLayout>
```

Because the Super Marshmallow Man tile is now spanning two columns, it will be consuming the second column of the first row. We need to make a number of changes to the rest of the grid to support this:

* add a fourth row to the grid
* increase the height from 450 pixels to 600 pixels to support the 4th row
* shift the remaining stack layouts 
* color the Super Marshmallow Man tile slightly differently to make it easier to see

Add the fourth row by changing the `rows` attribute of the grid layout to include a 4th row.

```xml
<GridLayout rows="*,*,*,*" columns="*,*" width="300" height="450">
...
</GridLayout>
```

Increase the height of the grid from 450 pixels to 600 pixels.

```xml
<GridLayout rows="*,*,*,*" columns="*,*" width="300" height="600">
...
</GridLayout>
```

Shift the remaining stack layouts.

```xml
<StackLayout row="1" col="0" style="background-color: #CCCCCC;">
    <Label text="Couch Commander" textWrap="true" /> 
    <Label text="$24.99" />
</StackLayout>
<StackLayout row="1" col="1" style="background-color: #EEEEEE;">
    <Label text="Mummy Madness" textWrap="true" /> 
    <Label text="$32.99" />
</StackLayout>
<StackLayout row="2" col="0" style="background-color: #EEEEEE;">
    <Label text="Pyro Robots" textWrap="true" /> 
    <Label text="$19.99" />
</StackLayout>
<StackLayout row="2" col="1" style="background-color: #CCCCCC;">
    <Label text="Rescue Pups" textWrap="true" /> 
    <Label text="$9.99" />
</StackLayout>
<StackLayout row="3" col="0" style="background-color: #CCCCCC;">
    <Label text="Vampire Valkyrie" textWrap="true" /> 
    <Label text="$21.99" />
</StackLayout>
```

Change the color of the Super Marshmallow Man tile.

```xml
<StackLayout row="0" col="0" colSpan="2" style="background-color: #DDDDDD;">
    <Label text="Super Marshmallow Man" textWrap="true" />
    <Label text="$34.99" />
</StackLayout>
```

Finally, let's add a brief description of the game to the Super Marshmallow Man tile.

```xml
<StackLayout row="0" col="0" colSpan="2" style="background-color: #DDDDDD;">
    <Label text="Super Marshmallow Man" textWrap="true" />
    <Label textWrap="true" text="Escape from certain death in this wild adventure!" />
    <Label text="$34.99" />
</StackLayout>
```

Let's check out what this looks like in our emulator.

![image](images/chapter7/products-5.PNG)

Looks great!

Here's the complete code listing for the `products-page.xml` file as of the end of this chapter.

```xml
<Page>
    <ScrollView>
        <StackLayout>
            <Label text="Our Products" />
            <GridLayout rows="*,*,*,*" columns="*,*" width="300" height="600">
                <StackLayout row="0" col="0" colSpan="2" style="background-color: #DDDDDD;">
                    <Label text="Super Marshmallow Man" textWrap="true" />
                    <Label textWrap="true" text="Escape from certain death int his wild adventure!" />
                    <Label text="$34.99" />
                </StackLayout>
                <StackLayout row="1" col="0" style="background-color: #CCCCCC;">
                    <Label text="Couch Commander" textWrap="true" /> 
                    <Label text="$24.99" />
                </StackLayout>
                <StackLayout row="1" col="1" style="background-color: #EEEEEE;">
                    <Label text="Mummy Madness" textWrap="true" /> 
                    <Label text="$32.99" />
                </StackLayout>
                <StackLayout row="2" col="0" style="background-color: #EEEEEE;">
                    <Label text="Pyro Robots" textWrap="true" /> 
                    <Label text="$19.99" />
                </StackLayout>
                <StackLayout row="2" col="1" style="background-color: #CCCCCC;">
                    <Label text="Rescue Pups" textWrap="true" /> 
                    <Label text="$9.99" />
                </StackLayout>
                <StackLayout row="3" col="0" style="background-color: #CCCCCC;">
                    <Label text="Vampire Valkyrie" textWrap="true" /> 
                    <Label text="$21.99" />
                </StackLayout>            
            </GridLayout>
        </StackLayout>
    </ScrollView>
</Page>
```

<div class="exercise-end"></div>