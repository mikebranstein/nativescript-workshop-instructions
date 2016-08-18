## Collecting data from users

Up until now, we've been focused on displaying data to your app users, but most mobile apps aren't just sources of information, they also count on your interacting with them by collecting and submitting data.

In this section, you'll be building out the Contact Us page. As with most Contact Us pages within HTML applications, ours will allow the mobile app user to submit a question to Tekmo through a form. 

But, that's where the similarities stop. Although users will be submitting data through a *form-like* UI, they won't actually be interacting with an HTML form. 

NativeScript apps are native mobile apps. That means they're stateful and don't need to mess with HTML forms: thank goodness! 

> **NOTE** Throughout these exercises, you'll be structuring your code very similar to the previous chapter where we added UI elements, added events to the UI elements to detect user interaction points, attached event handlers, and wrote business logic inside the event handlers. This is a common NativeScript development workflow that you will repeat throughout the lifecycle of your app's developement. I like to point this out, because it's relatively straight-forward and helps you to understand what to expect when developing apps with NativeScript.

### Building a data collection UI

Before we jump straight into code, let's talk about what we're building. We want the Contact Us page to allow app users to submit a question or feedback message. In the spirit of keeping it simple, our message will have a subject and body, with a button allowing us to submit the message. 

<h4 class="exercise-start">
    <b>Exercise</b>: Making page content scrollable
</h4>

Start by replacing the elements in the `contact-us-page.xml` page with the `<Page>`, `<ScrollView>`, and `<StackLayout>` elements.

```xml
<Page>
    <ScrollView>
        <StackLayout>

        </StackLayout>
    </ScrollView>
</Page>
```

Add a `<Label />` element to the page to describe how a user can contact Tekmo. Place the label in the stack layout.

```xml
<Label textWrap="true" text="Contact us by submitting a message below." />
```

Add a `<TextField />` element underneath the label. This element will be used to accept the message subject. To let the users know the intent of the text field, let's also add an additional label right above the text field. 

```xml
<Label text="Subject:" />
<TextField />
```

Add a `<TextView />` element and another label beneath the pair of subject elements. 

```xml
<Label text="Body:" />
<TextView />
```

Finally, add a button to submit the message to Tekmo. Be sure to add the `tap` attribute so we can respond to the tap event later.

```xml
<Button text="Submit" tap="onTap" />
```

 The complete code should look like this:

 ```xml
 <Page>
    <ScrollView>
        <StackLayout>
            <Label textWrap="true" text="Contact us by submitting a message below." />
            <Label text="Subject:" />
            <TextField />
            <Label text="Body:" />
            <TextView />
            <Button text="Submit" tap="onTap" /> 
        </StackLayout>
    </ScrollView>
</Page>
```

You should see the following on the Contact Us page within your emulator.

![image](images/chapter6/contact-us-1.PNG)

<div class="exercise-end"></div>

I just introduced you to two new UI elements: the `<TextField>` and `<TextView>` elements. They're both used for collecting user input, with the only significant difference being that the text view allows you to collect multiple lines of text from a user. 

### Refactoring to clean up the UI 

After looking at the Contact Us page, it seems a bit cumbersome to create both a label and a text field/view for each data entry field. The labels feel somewhat mandatory, because without them, the user wouldn't know the purpose of these two data fields. Even worse, if you're used iOS, you won't even know the data fields exist, because iOS doesn't wrap any visual cues around UI elements. So, these text field/views appear are blank spaces on the screen. 

<h4 class="exercise-start">
    <b>Exercise</b>: Refactoring the text field and view
</h4>

Text fields and text views have an attributed named `hint` that places temporary text in the text box. When a user types into the text field or view, this temporary text disappears and is replaced with whatever they type. 

Add the the `hint` attribute to the text field and view. 

```xml
<TextField hint="Enter the subject..." />

<TextView hint="Enter the message..." />
```

Look at your emulator and see the results. Play with it, by clicking in each of the fields and entering text. Note that as you type, the temporary text you specified in the hint attribute disappears. Also note that when you delete any text you entered, the hint attribute text comes back. Pretty cool!

![image](images/chapter6/text-hint.gif)

But wait, there's more! By adding the hint attribute, we've eliminated the need for the descriptive labels.

Remove the labels from the page. The entire page should look like the code and screen shot below.

```xml
 <Page>
    <ScrollView>
        <StackLayout>
            <Label textWrap="true" text="Contact us by submitting a message below." />
            <TextField hint="Enter a subject..." />
            <TextView hint="Enter a message..." />
            <Button text="Submit" tap="onTap" /> 
        </StackLayout>
    </ScrollView>
</Page>
```

![image](images/chapter6/contact-us-2.PNG)

<div class="exercise-end"></div>

### Responding to the button tap

I almost forgot: we haven't finished the page. Try this on your own. 

Go ahead and add the tap event handler for the submit button. For now, you can log a message to the console to let you know the handler actually works. If you get stuck, look back at a previous exercise, or follow along with the code below.

<h4 class="exercise-start">
    <b>Exercise</b>: Add tap event handler for the submit button
</h4>

Create a file in the `app` directory named `contact-us-page.js`.

![image](images/chapter6/contact-us-3.PNG)

Add the `onTap()` event handler to the `contact-us-page.js` file, making sure to export it so the page can find the function.

```javascript
function onTap() {
    console.log("Submitting message...");

    // todo: add code to get data out of text field and view, then submit to Tekmo
    // step 1: get data out of text field and text view 
    // step 2: submit data to Tekmo
}
exports.onTap = onTap;
```

Test out your changes, and check the command line for the console output when you click the submit button.

<div class="exercise-end"></div>

In the next two exercises, we'll be adding code to get the data out of the text field and text view, then submit the data to Tekmo. 

Let's start by adding some code to grab the data out of the text field and text view on the Contact Us page.

> **NOTE** There are several ways of getting data in and out of UI elements. You'll be learning several of them throughout this workshop. To start, you'll be learning a very manual way, then I'll introduce you to an easier way in a future exercise.

<h4 class="exercise-start">
    <b>Exercise</b>: Get data out of a text field and text view
</h4>

To get data out of a text field or text view, we'll need access to the currently running NativeScript page. The easiest way to get access to the page is to save a reference to it when the page first loads. 

Create a variable to save the reference to the current page at the top of your `contact-us-page.js` file.

```javascript
var page;
```

Get a reference to the page when the page first loads by handling the `loaded` event of the NativeScript page. 

Add a `loaded="onLoaded"` attribute to the `contact-us-page.xml` file's `<Page>` element.

```xml
<Page loaded="onLoaded">
```

Add the corresponding handler function to the `contact-us-page.js` file.

```javascript
function onLoaded(args) {
    // todo: save page reference
}
```

You'll notice the `onLoaded()` handler function has an `args` argument variable. Every event handler has an argument; however, up until now, we have ignore this optional parameter.  This argument contains useful information about the event that has just happened, and often contains a reference to the object (or element) that the event is attached to. In our case the element belonging to the `onLoaded()` event is the `<Page>` element, so let's use the argument to grab a reference to the page.

Change the `onLoaded()` function definition to save the page reference.

```javascript
function onLoaded(args) {
    // saves a reference to the Contact Us page
    page = args.object;
}
```

Now that we have a reference to our page, we'll be using the `getViewById()` function of the page to get a reference to the text field and text view. 

Before we do this, we'll first need to add an `id` property to the text field and text view.

```xml
<TextField id="subject" hint="Enter a subject..." />

<TextView id="message" hint="Enter a message..." />
```

Now, get a reference to each of the UI elements by using the `getViewById()` function of the page. Place this code right under the `// step 1:` comment of the `onTap()` function.

```javascript
var subjectElement = page.getViewById("subject");
var messageElement = page.getViewById("message");
```

Get the entered text from each element by using the `text` property.

```javascript
var subject = subjectElement.text;
var message = messageElement.text;
```

To double-check your work so far, add in a few `console.log()` commands to output the captured subject and message values. Test it out!

![image](images/chapter6/text-console-output.gif)

For reference, here is the complete code listing for the Contact Us page.

For `contact-us-page.xml`:

```xml
 <Page loaded="onLoaded">
    <ScrollView>
        <StackLayout>
            <Label textWrap="true" text="Contact us by submitting a message below." />
            <TextField id="subject" hint="Enter a subject..." />
            <TextView id="message" hint="Enter a message..." />
            <Button text="Submit" tap="onTap" /> 
        </StackLayout>
    </ScrollView>
</Page>
```

For `contact-us-page.js`:

```javascript
var page;

function onLoaded(args) {
    page = args.object;
}
exports.onLoaded = onLoaded;

function onTap() {
    console.log("Submitting message...");

    // todo: add code to get data out of text field and view, then submit to Tekmo
    // step 1: get data out of text field and text view
    var subjectElement = page.getViewById("subject");
    var messageElement = page.getViewById("message");

    var subject = subjectElement.text;
    var message = messageElement.text;

    console.log(subject);
    console.log(message);

    // step 2: submit data to Tekmo
}
exports.onTap = onTap;
```

<div class="exercise-end"></div>

Now that you've gotten the data out of the text field and view, it's time to send the data over to Tekmo. In this next exercise, we'll be encoding our message in JSON and sending data to Tekmo via REST API endpoint. 

This is more of an advanced topic for discussion, and isn't necessarily NativeScript-specific; however, almost every mobile app you create *will* interact with some remote web service or REST API, so I feel it's important to highlight and show you how this is done in a NativeScript app.

> **NOTE** I just dropped a lot of new terms on your plate that you might not be familiar with, like JSON and REST API. Don't worry if you don't understand everything. You can just copy and paste the code in the next section, or skip it all together. This is the last part of this section, so just ahead to the next chapter if you don't want to follow along.

<h4 class="exercise-start">
    <b>Exercise</b>: Sending our message to Tekmo as JSON via their REST API
</h4>

Start by adding a reference to the *http module* at the top of the `contact-us-page.js` file. The http module allows you to send HTTP requests to an endpoint, which is exactly what we want to do. The module is part of the core modules, which means the framework is doing all the heavy lifting for you (i.e., working with the Android and iOS specific function calls to make HTTP calls simple).

Read the NativeScript documentation on the [http module](https://docs.nativescript.org/cookbook/http) for more information.

```javascript
var httpModule = require("http");
```

Build a stringified JSON object containing the subject and message. This (and all subsequent code) should go directly beneath the `// step 2` commend of the `onTap()` function.

```javascript
var data = JSON.stringify({
  "subject": subject,
  "message": message
});
```

Finally, make the request, passing in the URL (https://nstweet.brosteins.com/api/message), the HTTP method (POST), the HTTP header telling the REST API the data is being sent over in JSON format, and the stringified JSON data.

> **NOTE** The function call to `request()` returns a [promise](http://www.html5rocks.com/en/tutorials/es6/promises/), which may not be something you're familiar with. That's ok. Check out the link I provided, and you should be able to decipher what's happening below (which is essentially, making an HTTP request, and the `.then()` call holds the success and failure code paths of that original request).

Note this is an endpoint I setup for the lab. It may not be very long-lived, so, if you're receiving 404 NOT FOUND messages, I would assume it's no longer available.

```javascript
httpModule
    .request({
        url: "https://nstweet.brosteins.com/api/message",
        method: "POST",
        headers: { "Content-Type": "application/json" },
        content: data })
    .then(function(response) {
        // success
        console.log(response.statusCode);
    }, function(e) {
        // error
        console.log("Error occurred: " + e);
    });
```

Now, let's try it out, and you should see that when a user clicks the submit button, the message is sent to Tekmo and the response from Tekmo's REST API service has responded back with *200* in the command prompt.

![image](images/chapter6/http-ok.gif)

Nice work!

<div class="exercise-end"></div>

### Providing better feedback 

You've done great sending and receiving data from Tekmo's REST API service, but something doesn't feel right. Mobile apps are about having a good user experience, and last time I checked, making a user read console or command line output to let them know their message was successfully submitted to Tekmo is not in the dictionary under "good user experience".

Let's change that by providing the user with a visual indicator their message was successfully sent in our final exercises of this chapter.

<h4 class="exercise-start">
    <b>Exercise</b>: Using the dialog module to provide visual feedback
</h4>

The dialog module provides you with a variety of "pop-up" windows (or dialog windows) for providing feedback to users. Because it is also part of the NativeScript core modules, there's nothing special you need to do to start using it aside from importing the module into your JavaScript code.

Start by importing the dialog module using the `require()` syntax at the very top of the `contact-us-page.js` file.

```javascript
var dialogModule = require("ui/dialogs");
```

NativeScript has 5 different types of dialogs:
* alert
* confirmation
* prompt
* login
* action

The [dialog documentation](https://docs.nativescript.org/ui/ui-dialogs) has examples of each dialog type, so I'm not going to give you examples of each. I encourage you to review the various types, because they save you time (i.e., the login dialog provides a great cross-platform way of authenticating users with a few lines of code instead of writing dozens). 

You'll be using the alert dialog. The alert dialog displays a small dialog window, with a custom message, and a single button. 

Add a dialog alert below the `console.log()` calls with the `httpModule.request()` success and error code.

```javascript
...
.then(function(response) {
        // success
        console.log(response.statusCode);
        dialogModule.alert("Your message has been sent.");
    }, function(e) {
        // error
        console.log("Error occurred: " + e);
        dialogModule.alert("We couldn't send your message right now. Try again later.");
    })
```

Run the updated app to see how dialogs work.

![image](images/chapter6/contact-us-4.PNG)

<div class="exercise-end"></div>

The dialog module's default alert window is OK, but what if you want something a little more customized? That's actually pretty easy. 

<h4 class="exercise-start">
    <b>Exercise</b>: Customizing the alert dialog
</h4>

By default, the dialog module's `alert()` function takes a string, and it displays the contents of that string in the dialog alert window that appears. The `alert()` function also takes an *options* object that allows you to customize the alert title, the message, and the button text. Take a look at the official documentation to learn more about the [options object](https://docs.nativescript.org/ui/ui-dialogs).

Customize the success alert window by replacing the the successful alert in the `contact-us-page.js` file with one using the options object.  

```javascript
dialogModule.alert({
    title: "Thank you!",
    message: "We have received your message.",
    okButtonText: "Close"
});
```

Check back in your emulator to see the change take effect.

![image](images/chapter6/contact-us-5.PNG)

For reference, here is the complete JavaScript code for this chapter.

```javascript
var httpModule = require("http");
var dialogModule = require("ui/dialogModule");
var page;

function onLoaded(args) {
    page = args.object;
}
exports.onLoaded = onLoaded;

function onTap() {
    console.log("Submitting message...");

    // todo: add code to get data out of text field and view, then submit to Tekmo
    // step 1: get data out of text field and text view
    var subjectElement = page.getViewById("subject");
    var messageElement = page.getViewById("message");

    var subject = subjectElement.text;
    var message = messageElement.text;

    console.log(subject);
    console.log(message);

    // step 2: submit data to Tekmo
    var data = JSON.stringify({
        "subject": subject,
        "message": message
    });
    
    httpModule
        .request({
            url: "https://nstweet.brosteins.com/api/message",
            method: "POST",
            headers: { "Content-Type": "application/json" },
            content: data })
        .then(function(response) {
            // success
            console.log(response.statusCode);
            dialogModule.alert({
                title: "Thank you!",
                message: "We have received your message.",
                okButtonText: "Close"
            });
        }, function(e) {
            // error
            console.log("Error occurred: " + e);
            dialogModule.alert("We couldn't send your message right now. Try again later.");
        });
}
exports.onTap = onTap;
```

<div class="exercise-end"></div>