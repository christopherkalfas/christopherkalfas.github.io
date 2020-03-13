---
layout: post
title:      "Is it Secret, Is it Safe? - (How to Hide API Keys)"
date:       2020-03-13 10:02:15 -0400
permalink:  is_it_secret_is_it_safe_-_how_to_hide_api_keys
---

![](https://media.giphy.com/media/ViLImh6wbZcJy/giphy.gif)

As the Grey-wizard once lamented to Frodo, the ring of power must be hidden from the ever-watching evil-eye of Sauron. If Sauron obtains the ring of power, Middle-Earth will plunge into darkness for a millennium.  Just like how the ring of power must remain hidden from Sauron, we, as programmers, have to keep our API keys secret from internet ne'er-do-wells. Hackers can use your API key and rack-up huge charges billed to you!

![](https://media.giphy.com/media/ds2i5FmotMuWI/giphy.gif)

For this blog, I show you how to hide your API keys for a JavaScript web app using `.gitignore` and a Javascript package called `dotenv`.
### `.gitignore`
In your source folder, add a file, you can name it anything you want. A standard convention is to name the file ***apikeys.js.*** You want to create an object that holds the key. You can name the key anything you want, but *the value should be your API key in a string*. 

``` module.exports = {
   "apikey": "Your_API_Key",
}; ```

If you used `create react app`, you'd see a file in your tree called `.gitignore`. This file will not show up on your GitHub commits, just as the name implies. Open that file, and at the top of the file add the line:

``` apiKeys.* ```

Now, in whatever file you make a fetch request to the API, we need to import the API key objects.

``` import apiConfig from './apiKeys' ```

You can now use the API key object in your fetch requests, with GitHub **not** posting the key.

``` const fetchURL = `http://api.exampleapi.org/example/data&APPID=${apiConfig.apikey}` ```

![](https://media.giphy.com/media/TGvHZanK0Y8poe2lnA/giphy.gif)

### ANOTHER ONE - `dotenv`

Another option is a JavaScript Package called `dotenv`. This package is very straight-forward. It can load-in environment variables from a special file called `.env`.

In your application's parent node you need to require and configure the `dotenv` package, with the line:

``` require('dotenv').config() ```

Then, create a `.env` file and add your application's environment-specific variables, following the naming conventions of ***KEY=VALUE***. Note, we are not declaring an object or exporting the same way as we did with `.gitignore`. 

`API_KEY=42is35not853a21real83key`

Back in your parent node console log `process.env` to make sure you are returning your key. Now you can declare a constant variable that holds the value of `process.env.API_KEY` .Now you can string interpolation to use your API key in your fetch request.

`const api_key = process.env.API_KEY`

And there you have it! Two different approaches to hiding your API keys from GitHub. Middle-Earth and your web application are safe; for now.

![](https://media.giphy.com/media/iofbYa67AbBg4/giphy.gif)
