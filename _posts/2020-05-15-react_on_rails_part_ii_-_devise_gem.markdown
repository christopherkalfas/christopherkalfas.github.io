---
layout: post
title:      "React on Rails Part II - Devise Gem"
date:       2020-05-15 17:39:06 +0000
permalink:  react_on_rails_part_ii_-_devise_gem
---


Hello again! Last week I talked about configuring a Rails/React application using the webpacker gem. When we wrapped up part one, we successfully ran our Rails backend and our React-client frontend and created a beautiful pipeline that connects them. 

![](https://media.giphy.com/media/REiJphYIQy13i/giphy.gif)

If you missed last week's blog, here is the link:

[Part I](https://christopherkalfas.github.io/react_on_rails_-_webpacker_configuration)

At this point, you can build out your application to your heart's desire. BUT WAIT! It's dangerous to build a web app without some security. Let's build some authentications by adding logins/logouts to make sure some internet ne'er do well can't wreak havoc. 

![](https://media.giphy.com/media/26uflFzANm3yyJCKc/giphy.gif)

### WHAT IS DEVISE?

Devise is an authentication gem for Rails. Devise is fully compatible with the Rails MVC convention.

### INSTALLING DEVISE 

Just like we did with the webpacker gem, let's add `gem 'devise'` to our Gemfile. The documentation is excellent and even has a section about configuring the gem to work with Heroku. 

Here is the link: [Devise](https://github.com/heartcombo/devise)

Now to install the gem, we run `bundle install` in the terminal. Once this is complete, we need to run the 'devise' installer. 

In the terminal run: `rails generate devise:install`

### DEVISE CONFIGURATION

In the console, you should see a list of configuration requirements. We need to configure the default URL options for our 'mailer' in our development and production environments. That's right! We are going to have a 'mailer.' Get excited!

![](https://media.giphy.com/media/26FeWNsNqHq2nRhC0/giphy.gif)

Open the `development.rb` file in the `config/environments` path. We need to add:

`config.action_mailer.default_url_options= { host: 'localhost', port: 3000 }`

Nice work! Now take a few minutes and read through the 'devise' initializer. You'll see the different configuration options devise offers.

### IMPLEMENTATION

Now we are ready to create a model that configures the Devise defaults. As an added kicker, the following generator command will create our set routes in `routes.rb`.

For most web applications, we will need a User model, that would be the most logical model to configure to devise. In the terminal run: 

`rails generate devise User`

### DEVISE VIEWS & NOTIFICATIONS

Devise takes advantage of flash messages to tell users if they are signed in or signed out. Since we want these flash messages throughout our application, we need to define the flash messages in our application layout. 

Navigate to your `app/views/layouts/application.html.erb` file and add these two `<p>` tags:

```
<p class="notice"><%= notice %></p>
<p class="alert"><%= alert %></p>
```

Also, last week we already defined the root route, and we don't HAVE to do that again. However, if you want to customize the views for logins/sign-ups, run:
 
`rails generate devise:views`

For the sake of keeping this blog concise, I'm not going to talk about these view's custom configuration, but here is the link from the devise documentation. [Configuring Views ](https://github.com/heartcombo/devise#configuring-views)

As per usual, we need to migrate our table to our database before we fire up Rails. Run:

`rails db:migrate`

Before we test our authentications, we need to have some way users can navigate our application and sign-up/login pages. Open the `home.html.erb` in our welcome view's folder we created last week. 

You can set this up any way you like, but are some devise helper methods you can utilize:

* `user_signed_in?`  - Verifies if a user is signed in
* `current_user` - Which user is currently signed in
* `user_session` - Gives you access to the session's scope.

Here is a template that I used during my initial build. 

![Imgur](https://i.imgur.com/7eZK56k.jpg)

Great work so far, we only have one more step before we can test our authentications. Let's check to see if a user is signed in before we let users view our React app. In the welcome controller, we build last week to declare a home and app method.
Right below the class declaration, we need to a 'before-action.'  We want to authenticate the user *before* they travel to the app, but we don't want to verify on the Rails home page, because no new users could sign up. Here an example of how to do this.

`before_action :authenticate_user!, only [:app]`

Now to make sure everything worked in one terminal run: `rails s` and, then in **ANOTHER** terminal run:

`./bin/web-pack-dev-server`

#### Huzzah! 

![](https://media.giphy.com/media/Ymi6EjgBubhPBhNZn7/giphy.gif)

With everything purring like a kitten, if a user tries to navigate to the app from the home page, a flash notification appears telling users they need to be logged in to do that. Once they sign-up and then log in, we'll see another flash message telling the user they have signed in successfully before navigating to our React app.

Over the last two weeks, we built a pipeline between our Rails server and the React client app. AND THEN we protected it! You should be feeling pretty good about your skills. 



 



