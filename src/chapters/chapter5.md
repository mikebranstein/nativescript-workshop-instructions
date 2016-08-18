## Working with more text

You've already learned about the stack layout in previous exercises. You'll recall that it allows you to stack UI elements on a page by placing the elements inside of a `<StackLayout> ... </StackLayout>` tag. 

That's the basics of the stack layout, and truthfully, there's not a lot more to tell you. So, let's move on to the About and add more content using the stack layout.

### Adding content to the About page

The About page should tell app users about the Tekmo company, it's origins, it's inspirations, and get them excited about Tekmo. So, let's use the stack layout and some label elements to add content.

<h4 class="exercise-start">
    <b>Exercise</b>: Adding content to the About page using stack layouts and labels
</h4>

Remove the existing label in the `about-page.xml` file and replace it with a `<StackLayout> ... </StackLayout>` element so we can put multiple elements on the screen.

The About page should look like this:

```xml
<Page>
    <StackLayout>

    </StackLayout>
</Page>
```

Now, add several labels describing Tekmo. You may want to use the *Copy* feature to the right for this one, it's a lot of text to type in manually.

```xml
<Label text="About Tekmo" />
<Label textWrap="true" text="Tekmo is a small online retailer specializing in retro video games sales and services. We're based in Louisville, KY." />
<Label text="Our Mission" />
<Label textWrap="true" text="We exist to bring our customers the best in retro gaming at an affordable price. We love to revisit and replay the games that shaped our childhoods, and believe that through sharing our love, we can help shape another generation of retro gaming geeks." />
<Label text="History" />
<Label textWrap="true" text="In the early 90's, it all started with Rescue Pups. This multi-player vintage platformer brought the Rambo-style side-scrolling gun fights to life in our living room. True, it was impossible to beat with the 3 lives you got by default, but that's why everyone knew the 50 lives code by heart: up, up, down, down, left, right, left, right, B, A, Start. And if you wanted a friend to play along, you could throw in the Select, Start at the end." />
<Label textWrap="true" text="After Rescue Pups, it was the classics like Super Marshmallow Man and Vampire Valkyrie. Do you remember them? We do. And we loved it! We hosted sleep overs every weekend throughout the summer, stayed up too late, got in trouble, pretended to fall asleep, then crept downstairs in the middle of the night to continue the fun." />
<Label textWrap="true" text="As we grew older, the games we played did too, but our love for the originals never stopped, and our passion for sharing these games with our friends and family grew." />
<Label textWrap="true" text="After many year, we all started having kids of our own, and we found ourselves wanting to raise our kids in our footsteps (without the midnight gaming marathons, of course). We wanted our kids to relive the adventure. Relive the thrills. Relive the classics. Tekmo was born." />
<Label textWrap="true" text="We remembered how cool it was to get 50 lives, so now our kids could enjoy playing through Rescue Pups for hours." />
<Label textWrap="true" text="And then there was Vampire Valkyrie: a side-scrolling adventure into the depths of Transylvania seeking out Dracula and his minions. After gathering your supplies in local towns, you embarked on a journey through the countryside to rescue trapped village people. We never forget to bring your stake and darn your garlic. And when we finally meet Dracula face-to-face, holy water didn't save us. And now, the fate of the world is on another 7 year old's shoulders." />
<Label textWrap="true" text="Lastly, Super Marshmallow Man is the one that pushed us over the edge with its iconic landscapes filled with clouds and wonderous sky scenes. We regularly play through the 12 worlds of Mallow Kingdom while avoiding the hungry Chompers with our friends and families: the best part is still watching someone get too close to the flames and melt!" />
```

Here's what you should see in your emulator.

![image](images/chapter5/about-no-scroll.png)

<div class="exercise-end"></div>

### Scrolling

Your app is really starting to come together. Looks good. But wait! The text on the About page scrolls off the bottom of the page. 

Go ahead try and scroll in your emulator by simulating a tap and drag to scroll the page's content. 

You can't.

This brings me to a fine point. In order to make your page's content scrollable, you need to use the `<ScrollView> ... </ScrollView>` element.

<h4 class="exercise-start">
    <b>Exercise</b>: Making page content scrollable
</h4>

Between the `<Page>` and `<StackLayout>` elements, add a `<ScrollView>` element. The scroll view should wrap the entire stack layout like so:

```xml
<Page>
    <ScrollView>
        <StackLayout>
            <Label text="About Tekmo" />
            ...
        </StackLayout>
    </ScrollView>
</Page>
``` 

Go back to your emulator and try scrolling, it should now work!

<div class="exercise-end"></div>

> **NOTE** All of the examples in the workshop place the scroll view element as the first element of a page: this makes all of the content of the page scrollable. Truth be told, you can place a scroll view anywhere on page, and your app's design may require only part of the page as having scrollable content. I won't go into details in the workshop on the various combinations, but I cover this in greater detail in my book,[NativeScript in Action](http://bit.ly/nsinaction). 

I'm going to declare the About page *finished* (for now). Let's move on to the Contact Us page.