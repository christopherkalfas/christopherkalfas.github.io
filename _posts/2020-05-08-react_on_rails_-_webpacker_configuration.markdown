---
layout: post
title:      "React on Rails - Webpacker Configuration "
date:       2020-05-08 17:40:39 +0000
permalink:  react_on_rails_-_webpacker_configuration
---


Throughout my coding education, I got a lot of practice in different languages using loops, iterating through nested objects, string manipulations, and so on. I did NOT get a lot of practice at tying everything together. Don't get me wrong I've built several full-stack applications at this point, but the biggest struggle I have had is in the configuration. I find that the errors are debilitating, and looking on google is hard because the nature of the questions is specific to your project and not the post on Stack Overflow with that magical green checkmark.

![](https://media.giphy.com/media/5wFkqt6A8R4qAqGIFQ/giphy.gif)

So for this blog post, I wanted to talk about the configuration 'nitty-gritty' for tying React to Rails. There are a ton of gems and different paths to hook up Rails to a React UI. 
In previous blogs, I've talked about hosting a full-stack app on Heroku using Rails as an API, and within the Rails app, so I will skip that and focus on turning Rails into an API **AFTER** creating a rails app. I am also going to talk about using the `webpacker` gem, and next week I'll cover the `devise` gem. 

### INITIAL SET UP

As I mentioned before, we are not going to use the `--api` tag on our rails app and create it using:

	 `rails new my-app --database=postgresql`

Go ahead and create the database to make sure you Rails app set up correctly. Remember you need to run:

`rails db:create`

then run...

`rails s`

### UNPACKING WEBPACKER

![](https://media.giphy.com/media/jx3VWe9xhX6Y8/giphy.gif)

Webpacker is a popular Rails gem that makes it simple to use JavaScript's bundler to manage JavaScript support in your Rails application. While 'webpacker' CAN be used for CSS and other styling components, its *primary purpose to assist JavaScipt to run inside of Rails*.

Here is a link to the Webpacker documents: [Webpacker](https://github.com/rails/webpacker)

### INSTALL WEBPACKER

First, add the 'webpacker' to your gem file.

`gem webpacker`

Next, run `bundle install` to embed the gem in your app.

Then we can access the configurations of webpacker for React by running:

`rails webpacker:install:react`

![](https://media.giphy.com/media/LtcuAIzPqlTnW/giphy.gif)

Boom! Nice work! We've got half of the pipeline built! Now let's create of front end React app. In the terminal, run:

`create-react-app client`

Once the application finishing building, open the `index.js` file and delete the 'service-worker' code. Optionally you can add the client node modules in your `gitignore` file. 


### HOOK UP WEBPACKER TO REACT

Now we get to the fun part—the first step to getting the client to talk to the webpacker. We need to make some changes in our `webpacker.yml` in the Rails `config` folder. Once we are in the file, we need to change where the application looks for the *source path*.

**BEFORE**
```
	default: &default
		source_path: app/javascripts
		source_entry_path: packs
```
**AFTER**
```
    default: &default
        source_path: client
        source_entry_path: src
```

Look at you go! Our pipeline is hooked from front to back! Our Rails application will now look for the client folder and then follow the 'src' or source folder.

![](https://media.giphy.com/media/XdE6xmmh80kUyoyxAO/giphy.gif)

### ADDING ROUTE TO MOUNT  CLIENT

Now we are ready to build the React mount. To do this, *we need to create a landing or welcome page*. To create the UI for this, we first need to create a controller for it. In the rails terminal, we utilize the rails generator command to accomplish this.

`rails g controller welcome --no-assets --no-helper`

In our new controller, we need to define a `home` and `app` method.

```
class WelcomeController < ApplicationController

  def home
  end

  def app
  end
end
```

Next, we need to define our initial routes. In our routes file, we need to establish our 'GET' logic with a little bit of customizing.

```
Rails.application.routes.draw do
	get 'welcome/home'
	get 'app', to: 'welcome#app', as: 'app'
	root 'welcome#home'
end
``` 

![](https://media.giphy.com/media/W6Qnz0gapxYCtLxzEQ/giphy.gif)
### FINAL STEP!

The last step in setting up this connection is to tell our *Rails app to link our to React through the views folder*.  In the view's welcome folder, we are going to open `home.html.erb`.

```
<h1>Welcome#home</h1>
<p>Check out our application <%= link_to "here", app_path %></p>
```
Then in the welcome folder, open the `app.html.erb` file, we are passing in our div tag with the root id. On the next line, we are going to use our 'Squids and Icecream cones' to interpolate the index of the app through to the javascript_pack_tag,

```
<div id="root"></div>
<%= javascript_pack_tag 'index' %>
```

 Now we can test that our pipeline is flowing by firing up the rails server. Once it loads up, ***in another terminal run *** 
 
`./bin/web-pack-dev-server`


This command fires up the client's side. Little side note, once you run the development server command, **wait!** The terminal will output information like:

![Imgur](https://i.imgur.com/yfJ6Exk.jpg)

#### CONTINUE WAITING 

![](https://media.giphy.com/media/hCiQVo1dzVwPu/giphy.gif)

The client-side isn't fully loaded until you see a table referencing the app's assets, size, chunks, and chunk names.  The first few lines look like;

![Imgur](https://i.imgur.com/1pIXzf9.jpg?2)

**Huzzah!** Now if you go to `localhost:3000`, you should see a welcome page with a link that takes you to our React app.

Holy cow! That was a lot of configuration! I recommend taking a break and configuring yourself a sandwich. Next week I'm going to continue this tutorial by added the 'devise' gem for authentications. 

![](https://media.giphy.com/media/Km44L0dd839bG/giphy.gif)



