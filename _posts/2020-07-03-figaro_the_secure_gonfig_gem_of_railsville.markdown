---
layout: post
title:      "Figaro, the Secure Config Gem of Railsville"
date:       2020-07-03 17:58:07 -0400
permalink:  figaro_the_secure_gonfig_gem_of_railsville
---

![](https://media.giphy.com/media/l0HU20BZ6LbSEITza/giphy.gif)

Hi everyone! This week I'm going to talk about a speed bump I encountered while adding a Gmail account to my Rail apps' action mailer. Setting up the mailer is straightforward. In a nutshell, you need to configure the mailer to use a Gmail account to send out emails. To do that, you have to create a custom security measure using a two-step password that tells Gmail; the app is allowed to send an email. Gmail gives you an app password that replacing the stand email login password that you will set as a production configuration variable to your Rails app. 

Since we don't want the Gmail credentials visible on GitHub but need to the file to be usable, we need to create a secret configuration that handles the configuration variables.  In development, I used the `dotenv` gem, and it worked like magic, but when I moved to production, the mailer stopped working. I tried EVERYTHING. I tried resetting the app password. I checked my production file to make sure I formatted the default options correctly, and nothing worked. I spend the better part of four days looking for an answer, and I couldn't find anything. 

![](https://media.giphy.com/media/GyLc9e3hTYFWw/giphy.gif)

I still can't explain why and haven't found a good explanation on Google yet.

One thing I did see what another gem called [Figaro](https://github.com/laserlemon/figaro), so I figured I would check it out. When I used `figaro`, it just worked. I'm sure there is a way to  get `dotenv` to work, but `figaro` was much easier, in my humble opinion. So here a quick walkthrough of how to add `figaro` to your project. 


Add the `figaro` gem to your Gem file and `bundle install` to install it.

`gem 'figaro'`


OR install in the gem through your terminal.

`bundle exec figaro install`

This command creates a new file in your directory's configuration folder, called `application.yml`. The gem should also add that file into your `.gitignore` file. 

**DOUBLE CHECK** before moving forward. 

Inside of `application.yml` is a commented-out template for adding configuration variables. Just add the keys of `GMAIL_USERNAME` and `GMAIL_PASSOWRD` with their respective values under the `production:` key. 


```
production:

   GMAIL_USERNAME: "yourusername@gmail.com"
   GMAIL_PASSWORD: "yourgmailapppassword42"
```

If you are hosting on Heroku, you need to set the values of your configuration through their CLI as well. Figaro as a built-in command just for Heroku to accomplish this, and it's beautiful. In the terminal run:

`figaro heroku:set -e production`


That's it!

You are ready to go. Once you commit to GitHub, **TRIPLE CHECK** and make sure `application.yml` was picked up by `.gitignore.` You'll know it's right if you dont see it. Then push your app to your host service. 

![](https://media.giphy.com/media/SjJtvObPvnTeE/giphy.gif)

I hope this helps you host a fantastic and secure application!

To the first person reading this that can figure out the reference I allude to in the title; I will donate $20 to a charity of your choice. Reach out to me on [LinkedIn](https://www.linkedin.com/in/christopherkalfas/).

That's all for this week!

Time to Say Goodbye






