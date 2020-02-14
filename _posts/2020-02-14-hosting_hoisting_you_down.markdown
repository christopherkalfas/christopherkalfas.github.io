---
layout: post
title:      "Hosting Hoisting you Down?"
date:       2020-02-14 16:51:53 +0000
permalink:  hosting_hoisting_you_down
---


So, you've done it. You have built a world-changing React application, and you can't wait to share it with the world! But, hold-up. How do you share it?

![](https://media.giphy.com/media/cwTtbmUwzPqx2/giphy.gif)

There are a ton of different hosting websites programmers can use to share their projects from the world. Github Pages, Now, Netlify are some popular options for React Developers. For this blog, I wanted to work through using Github Pages, since most programmers already have a GitHub accounts.

First things first, GitHub Pages as a few different options for hosting various web apps. You can have one site per GitHub User account or organization, BUT you have access to unlimited project sites. ***This walkthrough focuses on project pages.*** Additionally, GitHub Pages is free and a great option if you want to feature portfolio projects to potential employers. 

![](https://media.giphy.com/media/PLHdpauwfN2MvHcHxL/giphy.gif)

Before we get started, this walkthrough utilizes ***yarn*** for dependency management.

**CREATING A PRODUCTION BUILD**

Essentially a production build is a separate configuration for your app that optimizes download speeds and allows it to run in a browser. 	The great thing about React is the build tools are built-in and automatically handled for you!	

In the terminal, run the command `yarn run build`. Behind the scenes, React generates a 'build folder.' This folder holds all the static files need for a webserver production that is streamlined into one file to reduce the time it takes to download. 
 
Now let's say you want to view the production build of your application. Since the app still needs a server to run on, you can use another hand React/Yarn tool. In the terminal, run the command `yarn global add serve`. Once 'serve' has been installed, run `serve -s build`.

The production build can be view locally on port 5000. Anytime you make a change to the app and want to preview the production build again, *you have to rebuild the app with the build command for it to track the changes*.

Great Job! You are halfway home!

![](https://media.giphy.com/media/iIGKBnRBsZ9WEfCXXt/giphy.gif)

**DEPLOYING TO GITHUB PAGES**

After you run the build commands, the console comes back to you with a notification that you can pick what URL takes users to your page. 

To set this up, open package.json and right above where your dependencies are listed, add the following line:

		"homepage": "https://yourname.github.io/myapp",
		
Substitute '*yourname*' for your Github username and '*myapp*' for whatever the name of your app is.

Next, you need to install the GitHub Pages package called 'gh-pages.' The package creates a branch that is exclusively compatible with GitHub. In the terminal, run the command, `yarn add gh-pages`. So now, anything you push to that branch, it will show up on your project page.

Once the package is installed open package.json file and inside of the script object, add these two lines:

```
"predeploy": "yarn run build",
"deploy": "gh-pages -d build",
```
*Remember, "predeploy" comes before "deploy." You want to create a production build than deploy it. Also, don't forget the commas at the end!*

![](https://media.giphy.com/media/st6uhotBKjgR2/giphy.gif)

Next, run `yarn run deploy`. You'll have a new build folder, and your console will let you know your project page is published.

Lastly, to confirm your project page is working as expected, go to the settings tab of your project repo and scroll down the GitHub pages section. You should see a message telling your project was published with a link to the URL, and *under Source, your project page should be set to build from 'gh-pages branch.' *

You did it! Now the world can see your programming skills. A final thought, lots of the documentation I followed said it takes about ten minutes for you to see your project. In my experience, it was more like a couple of hours. I thought I had made a mistake, but I just lacked patience. 

I hope you found this walkthrough useful. And I can't wait to see how your app changes the world!

![](https://media.giphy.com/media/2episNCOtIW7S/giphy.gif)
