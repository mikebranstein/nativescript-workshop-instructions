## Your first app

In this exercise, you're going to create your first app. Before we get there, I'm going to introduce you to the NativeScript CLI (command line interface).

### NativeScript CLI

The NativeScript CLI is a set of command line tools that make your job as a mobile developer easy. The CLI provides tools for creating and scaffolding the files needed to develop an app, add in platform-specific files (for Android and iOS), building the app into the platform-specific mobile app containers, running your app in an emulator (Android) and simulator (iOS), and deploying your app to a physical device for testing.

The first thing we'll do is verify the CLI installation and version of NativeScript installed.

<h4 class="exercise-start">
    <b>Exercise</b>: Verifying your CLI installation
</h4>

Open a Node.js Command Prompt in Windows by clicking your Start Menu, typing 'node', and launching the "Node.js command prompt" desktop app from the Start Menu.

![image](images/chapter2/node-js-command-prompt.PNG)

Open a command prompt and run the `tns --version` command:

```
  C:\Users\dev>tns --version
  2.1.1
```

You should see version 2.1.1 is installed.

<div class="exercise-end"></div>

#### Using the tns CLI command

"tns" stands for Telerik NativeScript. Throughout the workshop, you'll be using the `tns` command from the Node.js command prompt. Remember the `tns` command, and be sure to always run it from your Node.js command prompt, as shown above.

### Creating an app

Let's get started creating your first app with NativeScript. It's pretty easy, especially with the CLI scaffolding tools.

<h4 class="exercise-start">
    <b>Exercise</b>: Creating your first app
</h4>

Change into your Documents directory:

```
  cd C:\Users\dev\Documents
```

Scaffold your first app using the  `tns create <your-app-name>` CLI command. The `tns create` command will create a directory with the same name as your app, then create the necessary directory structure needed for your app. In the example below, I named my first app "my-first-app".

```
  tns create my-first-app
```

Verify that your app was created by navigating to the my-first-app directory.

```
  cd my-first-app
```

You should see:

```
  C:\Users\dev\Documents\my-first-app>
```

Display the contents of the my-first-app directory, by running the `dir` command:

```
  dir
```

Which should display the following:

```
   Directory of C:\Users\dev\Documents\my-first-app

  08/03/2016  09:59 PM    <DIR>          .
  08/03/2016  09:59 PM    <DIR>          ..
  08/03/2016  09:59 PM    <DIR>          app
  08/03/2016  09:59 PM    <DIR>          node_modules
  08/03/2016  09:59 PM               299 package.json
  08/03/2016  09:59 PM    <DIR>          platforms
                 1 File(s)            299 bytes
                 5 Dir(s)  54,296,932,352 bytes free

  C:\Users\dev\Documents\my-first-app>
```

<div class="exercise-end"></div>

You did it! That's it: your first NativeScript app. Easy, right?

But not so impressive...yet. Let's see the app in action.

### Using the GenyMotion emulator

Now that you've created your first app, wouldn't you like to run it and see what it looks like?

Before we run the app, let's talk about NativeScript a bit more. NativeScript is a cross-platform mobile app development tool. That means write it once, run it on Android or iOS. Unfortunately, you need a Mac in order to development and run iOS apps, so unless you're using a Mac, you're out of luck.

If you're using a provided laptop, it's running Windows, so you're going to be running your app in an Android emulator named GenyMotion. Don't worry: it's already pre-installed for you. GenyMotion is free for personal use, so when you get home, you'll be able to follow along.

> **What is an Emulator?** Uh...that's a great question with a lengthy answer. [Jen Looper](https://twitter.com/jenlooper) wrote a [great article](http://developer.telerik.com/content-types/tutorials/how-do-mobile-emulators-even/) on emulators, simulators, and how your mobile app code may (or may not) look like you'd expect when.

The first thing we'll need to do is to start up the GenyMotion emulator. Let's do it. 

<h4 class="exercise-start">
    <b>Exercise</b>: Starting up GenyMotion
</h4>

Click on your Start Menu and type `geny`, click on GenyMotion to launch the GenyMotion emulator:

![image](images/chapter2/geny-motion.PNG)

GenyMotion will launch, showing you the main applicaiton window:

![image](images/chapter2/geny-app.PNG)

The GenyMotion app lists the available Android emulators in it's main window. With GenyMotion, you can add a variety of Android emulators. I've already added one for you, so just select the only emulator in the list, and press the `Start` button.

![image](images/chapter2/geny-app-start.PNG)

Time to be patient. Depending on how fast your machine is, GenyMotion may take several minutes to start the emulator. If you're using a laptop from me, I didn't spring for the best hardware, so it's slow and will take a couple of minutes.

Once the emulator has fully loaded, you should see an Android device running on your screen!

![image](images/chapter2/geny-emulator.PNG)

<div class="exercise-end"></div>

### Running your app

Congrats! You're now running an Android emulator and are ready to get your NativeScript app running on the emulator. Let's come back to our app.

<h4 class="exercise-start">
    <b>Exercise</b>: Adding the Android platform
</h4>

Before we run your app, we need to tell the app which platform we want to run it on. By default NativeScript apps don't assume you'll be running on any particular platform, so it's up to you to tell the app how to do this.

We'll use the `tns platform add android` CLI command to tell our app that it can run on Android. Run the command from the `my-first-app` directory:

```
  tns platform add android
```

This *will* take a few minutes, so be patient.

Let's verify that the Android platform has been added to the NativeScript app. Look in the current directory again:

```
  dir
```

Notice the `platforms` folder has been added. 

```
 Directory of C:\Users\mikeb\Documents\my-first-app

08/03/2016  10:26 PM    <DIR>          .
08/03/2016  10:26 PM    <DIR>          ..
08/03/2016  09:59 PM    <DIR>          app
08/03/2016  10:26 PM    <DIR>          node_modules
08/03/2016  10:26 PM               498 package.json
08/03/2016  10:25 PM    <DIR>          platforms
               1 File(s)            498 bytes
               5 Dir(s)  53,655,441,408 bytes free
```

Now, change to the `platforms` directory and look at the files within it:

```
  cd platforms
  dir
```

You'll see a folder named `android`. This folder contains the necessary files to run your app on an Android device. We're not going to dig into the contents of this folder, but if you're curious, take a look.

```
 Directory of C:\Users\mikeb\Documents\my-first-app\platforms

08/03/2016  10:25 PM    <DIR>          .
08/03/2016  10:25 PM    <DIR>          ..
08/03/2016  10:25 PM    <DIR>          android
               0 File(s)              0 bytes
               3 Dir(s)  53,639,196,672 bytes free
```

<div class="exercise-end"></div>

Now that you've added the Android platform, let's *finally* run your app!

<h4 class="exercise-start">
    <b>Exercise</b>: Running your app
</h4>

Before you actually run your app, let's make sure you're in your app's root directory `C:\Users\dev\Documents\my-first-app`:

```
  cd C:\Users\dev\Documents\my-first-app
```

Run the app using the `tns run android --emulator` command.

```
  tns run android --emulator
```

While you're waiting for your app to run in the emulator, let's take a moment to understand what's happening. When you run the `tns run android --emulator` command, you're telling the CLI to build your app, package it up, embed it within an Android .apk app, install it on to the running GenyMotion emulator, and run it. 

After a few minutes, you should see your app running within the emulator:

![image](images/chapter2/running-app.PNG)

Go ahead and play with the app for a few seconds.

<div class="exercise-end"></div>

### Understanding NativeScript apps

There's a lot going on under the scenes of your first app, so let's explore it together so you can get a feeling for the code within your first app.

<h4 class="exercise-start">
    <b>Exercise</b>: Running Visual Studio Code
</h4>

Let's start by opening a code editor. My favorite, lightweight, (and free) editor is Visual Studio Code (VS Code). VS Code is already installed on your laptop if you're using one I've provided. If you need to download VS Code, go to [VisualStudio.com](https://code.visualstudio.com/download) and download VS Code for free.

To launch VS Code, click your Start Menu and type in `code`. Click on `Visual Studio Code` to run.

![image](images/chapter2/code.PNG)

Once you're in VS Code, open your app's root directory, `C:\Users\dev\Documents\my-first-app`. You will see the app's file and folder layout on the left, and an editor window on the right. Be sure to use the `Open Folder...` option of VS Code.

![image](images/chapter2/code-app.PNG)

<div class="exercise-end"></div>

I'm not going to spend a lot of time teaching you about VS Code right now, so you may want to check out some of the videos and tutorials on [VisualStudio.com](https://code.visualstudio.com/docs) for further reference.

Let's look closer at our app's code.

<h4 class="exercise-start">
    <b>Exercise</b>: Exploring your app's code
</h4>

Let's back up to the `tns create my-first-app` CLI command and examine what's actually happening. I've shamelessly borrowed the following explanation from the official NativeScript docs, because it does such a nice job.

When `tns create my-first-app` is run, the CLI places the project in a new directory in the current directory. The newly created directory has the following structure.

```
my-first-app/
├── app
│   ├── App_Resources
│   │   └── Android
│   │       └── ...
│   │   └── iOS
│   │       └── ...
│   ├── app.css
│   ├── app.js
│   ├── main-page.js
│   ├── main-page.xml
│   ├── main-view-model.xml
│   ├── package.json
│   ├── references.d.ts
│   └── node_modules
│       └── ...
└── platforms
│   └── ...
└── package.json
```

You can see this same structure mirrored in your app within VS Code:

![image](images/chapter2/code-app-layout.PNG)

The `app` directory is the development space for your app. This is where you will write and modify code that will run when your app is run on a device (or in an emulator/simulator). 

> RULE: You can edit any file in (or under) `app` directory; however, never modify files outside of this directory. Files outside of the `app` directory are managed by NativeScript: so, hands off!

The `App_Resources` directory contains Android and iOS platform-specific files like images, splash screens, and other files. Don't worry about these now.

The `platforms` directory also contains platform-specific files, and is used as a sort-of build folder for the actual Android and iOS mobile app projects. You really shouldn't concern yourself with this folder and it's contents. Just know it's here, and per our earlier rule, *hands off*!

> RULE: Don't modify files in the `platforms` folder! 

I'm not going to go in-depth into the `node_modules` folder or the two `package.json` files. If you're curious, I cover the details of these files and folders in [NativeScript in Action](http://bit.ly/nsinaction).

Finally, we're getting to the real meaty stuff: *app.XXX* files and *main-page.XXX* files. When your app runs, the first piece of app code that runs is the app.js file. In a sense, you can think of the app.js file as a bootstrapper for your application. Let's open it up and see what's inside:

```javascript
var application = require("application");
application.start({ moduleName: "main-page" });
```

This code tells NativeScript to load the `application` module (more on these later), then it directs the app to `start` by giving it the name of the first (or home) page of your app. In this case, the first page is named `main-page`, so when you app runs, it will automatically start by displaying `main-page`.

> **NOTE** Just like HTML applications, you can think of NativeScript apps as a collection of pages. You move between page by navigating, and you can also pass data (or app state) between pages during navigation.

> **DEFINITION** A page is a collection of similarly-named files (.xml, .css, and .js). The .xml file contains your UI code, the .css file styles your UI, and the .js file contains your business logic code. NativeScript uses conventions to tell which files constitute a page, so all you need to do is name your .xml, .css, and .js files with the same prefix.

So, back to pages. Now that we know about the NativeScript page-naming convention, you understand what the `main-page` page is: it's a collection of 3 files: `main-page.xml` (the UI), `main-page.css` (styling for the UI), and `main-page.js` (any business logic code that interacts with the UI).

Let's take a look at the `main-page` page and find the 3 files:

![image](images/chapter2/code-app-layout.PNG)

Hmmm, `main-page.css` is missing. That's strange...but it's OK. It turns out pages don't *really* need all of the files. You only really need the UI definition (.xml) file. The .css and .js files are optional. If they're present, NativeScript will use them, but if they're missing, it doesn't care.

<div class="exercise-end"></div>

We've spent a lot of time on the introductory pieces of NativeScript, but we haven't gotten to really dive in an create our own app, so it's time to pick up the pace. I'll be going a little faster from here on, so when you have questions or need clarifications, stop me and we'll talk about it.