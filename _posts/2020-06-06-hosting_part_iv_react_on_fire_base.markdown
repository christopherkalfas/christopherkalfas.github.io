---
layout: post
title:      "Hosting Part IV: React on Fire(base)"
date:       2020-06-06 13:29:47 -0400
permalink:  hosting_part_iv_react_on_fire_base
---



Hi gang! I built out a portfolio website last week and wanted to host it using a new hosting service. In past blog entries, I've talked about, GitHub Pages, Now, Netlify, and Heroku. So this time, I wanted to step it a notch and use Google Firebase! 

![](https://media.giphy.com/media/g79am6uuZJKSc/giphy.gif)


Before we get started, here a few things to note:
* The portfolio website is built with React ONLY
* I'm using Yarn as the package Manager

Alright, let's do this!


### Step I

Head over to the [firebase](https://firebase.google.com/) website and sign-up/log in using your Gmail account. Once you've signed up, click on the 'console' button at the top right-hand corner of the navigation bar. Click on the 'Add project' card and give your project a name. Once you created the project head over to the terminal.

![Imgur](https://i.imgur.com/b2Dp6AH.png?1)

### Step II

Now we need to install two packages. The first is the `firebase-tools` package, which needs to be globally installed. In the terminal run,

`yarn global add firebase-tools`

Great! Now we have access to the Firebase CLI. The next thing we need to do is add the `firebase` package as a dependency in the directory of the project we want to host. Double-check you are in your project root directory, and then in the terminal run,

`yarn add firebase` 

Excellent job, team! We have everything we need at this point. Now we need to get the project ready. Firebase needs our `build` folder to host the app. So if you haven't already, create a build folder in the terminal.

`yarn run build`

### Step III

Now that our application has the packages and build folder ready to go, we need to connect to our Firebase project we created when we signed up. In the terminal run,

`firebase login`

Your terminal will redirect an open web tab where we need to confirm our email and password.

![Imgur](https://i.imgur.com/GJfm7ZJ.png)

Next, we need to initialize Firebase to our React app, by running,

`firebase init`

![](https://media.giphy.com/media/5Ys2bm1nW4kqRpRynQ/giphy.gif)

### Step IV
Firebase will start to prompt us with questions about configuration options. The first one is:

* `Which Firebase CLI features do you want to set up for this folder?` --> Use the *spacebar* to toggle down to ***Hosting: Configure and deploy Firebase Hosting sites.***
 
 
* The second prompt asks us to select an option. --> We want to choose ***Use an existing project***.

* Next, Firebase asks which Firebase project we want to associate with this directory.  --> Select **the project name we created on the Firebase website** and hit enter.


The next few questions ask us how we want to configure the web app. 
1. What do you want to use as your public directory? 
  * As mentioned above, we want to tell Firebase to use the `build` folder.
2. Configure as a SPA? 
   * All-day, every day. **Yes**
3. File public/index.html already exists. Overwrite?
   * **No** 
   * With SPAs, we want the user redirected to the `index.html` file. Then, our `index.html` file can pass the bucket to React Router.

### Step V
Firebase will create two new files in your project directory, `firebase.json` and `.firebaserc`.

Let's check and make sure we have done everything right up to this point. Open `firebase.json`; the file should be a mirror image of the one from my project;

 ```
{
  "hosting": {
    "public": "build",
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ],
    "rewrites": [
      {
        "source": "**",
        "destination": "/index.html"
      }
    ]
  }
}
```

Then over in `.firebaserc` we should see an object with a key-value pair of `projects` and another object with a key-value pair of `"default": "name-of-our-app"`

```
{
  "projects": {
    "default": "kalfas-portfolio"
  }
}
```

If everything looks correct, go ahead and commit to Github, to make sure we are tracking the new packages, build folder, and the two auto-generated Firebase files.


### Step VI

The last step is the simplest. All we need to do to deploy the application is run the command,

`firebase deploy`

Once the terminal stops running, Firebase returns a URL telling us where the app deployed. That's all there is to it! Firebase is the fifth different hosting service I have used, and I have to say, Firebase is the new king of hosting at my house.  

![](https://media.giphy.com/media/3KVcFEmdDl9NYaFTtx/giphy.gif)



