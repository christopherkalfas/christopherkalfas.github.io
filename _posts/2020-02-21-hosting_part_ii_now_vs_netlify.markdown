---
layout: post
title:      "Hosting Part II: Now Vs. Netlify"
date:       2020-02-21 20:52:17 +0000
permalink:  hosting_part_ii_now_vs_netlify
---


Okay, so you've successfully hosted a React application using GitHub Pages. The world can see witness your brilliance, and you start to wonder, 'Is this it? Have I reached the mountain top?'

![](https://media.giphy.com/media/xT4uQvE6Dm6go7psJ2/giphy.gif)

Sorry to bring you down, but you merely have climbed one peak of hosting-greatness. Any great climber will tell you; it's about the next climb. So, I, your hosting guide, challenge you to begin new ascents. Next up is '**Now**'

![](https://media.giphy.com/media/ORiw3L43P6vctTWXT2/giphy.gif)

Once again, this walkthrough utilizes ***yarn*** for dependency management.

**NOW: THE SEVERLESS SOLUTION** 

Now is a great hosting site that lets developers skip cloud configuration and quickly deploy their applications.

1. Head over to [Now - zeit.co](http://zeit.co ) and continue with GitHub using your GitHub account.
2. Now also has a CLI if you're into that sort of thing. In the terminal run, `yarn add global now` to install Now.
3. Once your app is complete, create a file called ***now.json*** in the *root of the project*. This file's purpose is to define the version of Now we want to use in our build. Below is a template you can use for the file. Set the name to match your app's name. Behind the curtain, Now is creating a build folder to handle entry points and routes while you back and enjoy a Pina Colada. 

```
{
  "version": 2,
  "name": "mdx-deck-advanced",
  "builds": [
    {"src": "package.json", "use": "@now/static-build"}
  ],
  "routes": [
    { "src": "^/images/(.*)", "dest": "/images/$1" },
    { "src": "^/snippets/(.*)", "dest": "/snippets/$1" },
    { "src": "index.html", "dest": "/index.html" }
  ]
}
```


4. Open your* package.json* folder and include the following in your scripts object at the key** now-build**. This script passes the static files to the distribution folder. Once this happens Now recognizes this folder as a static folder.

```
"scripts": {
  ...
  "now-build": "react-scripts build && mv build dist"
}
```

5. Ready to deploy, Captain? In the terminal, run `now`, or `yarn now`, depending on how you're set-up.  Let Now do its 'thing' and boom! You should see a URL in the console linking to your hosted website.
6. Last Step. Head back over to your Now dashboard, and like magic, you'll see your deployment in all its glory. 

![](https://media.giphy.com/media/YlPeYXasYEPpC/giphy.gif)

Look, in no time at all, you hosted yourself up to another mountain peak. Before you pack and head home, I wanted to offer one last option for hosting. Personally, this one was my favorite and my top choice moving forward. 

**NETLIFY**

I've spent the last few weeks trying out different hosting options, and I have to say, Netlify is hands down the easiest hosting option to use. 

1. In the terminal of your completed application run, `yarn run build` to make a build folder. You're halfway there already!
2. Go to [Netlify](https://www.netlify.com/) and sign-up with your GitHub information. Once you land on your dashboard, drag and drop your build folder into their app. AND THAT'S IT!

![pic](https://i.ibb.co/9W4hbxy/Image-2-21-20-at-2-37-PM.jpg)


WOW, I'm so impressed! A thousand words ago, you had no idea how you share your life-changing application with the world and now look at you. Not only do you currently have three options to share your next project, but you have an opinion that is much more valuable. So when you are showing off your knowledge of hosting at a coding meet-up, wowing potential employers, think of me and try to hook your boy up with an interview as well.

![](https://media.giphy.com/media/TjKpOwBLyN2ZW/giphy.gif)

