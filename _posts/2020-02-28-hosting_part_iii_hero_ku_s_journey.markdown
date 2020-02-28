---
layout: post
title:      "Hosting Part III: Hero(ku)'s Journey"
date:       2020-02-28 16:17:08 +0000
permalink:  hosting_part_iii_hero_ku_s_journey
---


If you thought my hosting series was over in part 2, think again! Like all good series, the final chapter is part III. This walkthrough covers hosting a FULL-STACK web app on Heroku. This post is my most substantial hosting undertaking yet, my Return of the Jedi, if you will.

![](https://media.giphy.com/media/3oeSAz6FqXCKuNFX6o/giphy.gif)

Let's map this bad-boy out before we dive-in.

For this walkthrough, I am going to use:
* Rails API with Postgres as a backend.
* Create React App to handle client/UI on the frontend.  
* A 'trick' that makes Heroku think you're only using one repo on GitHub to serve both ends of the app.

**SET UP RAILS API**

**Pre-Configurations** 
1. Make sure you have Rails 5 by running: `rails -v`
2. You want to be at least at `Rails 5.2.0`
3. Create an account with Heroku and follow the instructions to install it to your computer.

Now we're ready to climb. In the terminal, create a new folder for your web app and then change into that directory. Now, open your favorite text editor.

![](https://media.giphy.com/media/3o7TKUM3IgJBX2as9O/giphy.gif)

1. To create Rails in API mode, you run: `rails new . --api --database-postgresql`
2. Once installed, check to make sure you're on rails. In the terminal, run: `rails s -p 3001`

Look at us go! Before we celebrate, now comes the 'tricky' part. Not tricky for us, tricky for Heroku.

**CREATE REACT APP**

1. As soon as Rails finishes installing, type in the *same*  terminal: `create-react-app client`
2. While React is creating a new application head over to GitHub and create a new repository and follow the directions to add a remote to your local application.
3. Refresh your Github Page, and you should have your single repository with both your Rails API and React client.

![](https://media.giphy.com/media/gHcIlrz5bbD5S/giphy.gif)

**MAKE YOUR APP HEROKU READY - PART I (DEVELOPMENT)**

1. Once React finishes installing, go to `index.js` in the source folder and delete the lines of code related to the service worker. Using the service worker confuses Rails.

```
import registerServiceWorker from './registerServiceWorker';
registerServiceWorker();
```

2. Now we want to test out our React app. However, we can't run yarn start or npm start as we in the main directory of the entire application. We only want to run the client.  So, in the terminal run: `yarn --cwd client start`
3. Check your browser to make sure React is running. 
4. Next, we need to take advantage of Rails and React working together to automatical proxy our API calls to the right port. Open the `package.json` file in your client folder.
5. Below the private property and above your dependencies type: ` "proxy": "http://localhost:3001",`. We are proxying to port 3001 because React is already on port 3000.
6. Then we need to create a `Procfile.dev`, so we serve our client and API while we are in development. In the terminal type: `touch Procfile.dev`
7. Copy and paste these two lines into the file: 
```
web: PORT=3000 yarn --cwd client start
api: PORT=3001 bundle exec rails s
```
8. Run, `heroku local -f Procfile.dev`, and in the terminal, you should see both ends of your application working!
9. To make development a little easier, I would recommend creating a rake.start file in your tasks folder. Rake can manage this process faster than you. Copy and paste the snippet below into your new file.

```
namespace :start do
  task :development do
    exec 'heroku local -f Procfile.dev'
  end
end

desc 'Start development server'
task :start => 'start:development
```

Now you can type: `rake start` to get your application running.

**BUILD YOUR APPLICATION - INTERMISSION**

At this point, save the rest of this blog until you finish building your application. You can build your application without any more Heroku configurations until you're ready for deployment. 

![](https://media.giphy.com/media/daOuWzPJ4wuXCgNr28/giphy.gif)

**MAKE YOUR APP HEROKU READY - PART II (HEROKU PRODUCTION)**

1. Create a package.json file by typing in the root of your application: `touch package.json `
2. Copy and paste the code below into package.json

```
{
  "name": "name-of-your-app",
  "license": "MIT",
  "engines": {
    "node": "10.15.3",
    "yarn": "1.15.2"
  },
  "scripts": {
    "build": "yarn --cwd client install && yarn --cwd client build",
    "deploy": "cp -a client/build/. public/",
    "heroku-postbuild": "yarn build && yarn deploy"
  }
}
```

3. Change the name property to the name of your application. Also, make sure to change the 'node' and 'yarn' properties for the version you are running. You can check this with: `node -v` & `yarn -v`. 
4. Next, we need a `Procfile` in the root of our application's production build. Create a Procfile (just the word '*Procfile*'), and this file tells Heroku how you want your Rails app to run. Add the following code.

```
web: bundle exec rails s
release: bin/rake db:migrate
```

**CREATE HEROKU APP**

Now we are ready to turn our local application into a Heroku application and call it a day! Let's do this!

1. In the terminal run: ` heroku apps:create name-of-your-app`
2. Head back over to Heroku's dashboard, and you should see your application! Huzzah! 
3. Now let's add some buildpacks. Buildpacks are the instructions for Heroku to run your code. Think of buildpacks as Ikea instructions. They tell you how to build your dresser, and they also tell the *order to assemble it.* We need to tell Heroku to execute our front end first, so when it serves the backend, the front is ready to be hosted by Heroku.

First run, `heroku buildpacks:add heroku/nodejs --index 1`

Then, `heroku buildpacks:add heroku/ruby --index 2`

4. Now it's time to deploy. Commit the changes to GitHub and run, `git remote -v`. You'll see you have two different branches, `master` and `heroku`. Now run the line: `git push heroku master`.
5. Last Step. In the terminal, run: `heroku open`


And there you have it. A hosted full-stack single page application.


I would like to thank you for sticking out this three-part blog with me. I find that blogging about what I am currently working on is the best way to solidify concepts for me. Hosting intimidated me, and now three weeks later, I feel like I have a new skill on my resume. You and I have now hosted four web applications through four different services. That is worthy of celebration. Go, team!

![](https://media.giphy.com/media/bg1MQ6IUVoVOM/giphy.gif)



