---
layout: post
title:      "Hooks Part: II The Sequel We Deserve"
date:       2020-03-20 18:16:01 +0000
permalink:  hooks_part_ii_the_sequel_we_deserve
---


If you clicked on this blog because the title deceived you into thinking this was about a live-action return to Neverland, I apologize. What I offer you as compensation is almost as good. 

![](https://media.giphy.com/media/SvOrq4OA7TQTC/giphy.gif)

In a blog post from a few weeks ago, I wrote about using Hooks in React and discussed how hooks allow you to keep your component's state-flexible and remove unnecessary logic from life-cycle methods. For this blog, I wanted to talk about using React Hooks, and how much more accessible it is to make fetch-requests to APIs. 

Part I: [Because the Hook Brings You Back](Because the Hook Brings You Back)

### CONTEXT

I am using the 'OpenWeather' weather API to create a single-page React application.

Here is a link to API: [OpenWeather](https://openweathermap.org/api)

![Because the Hook Brings You Back](https://media.giphy.com/media/67XNScEjAgtBS/giphy.gif)

You'll need to sign-up for an account and request an API key. Remember to hide the API key if you plan on connecting the application to GitHub. If you are not familiar with how to do that, check out my blog, where I hide my API keys in two different ways.

[Is it Secret? Is it Safe? - (How to Hide API Keys)](https://christopherkalfas.github.io/is_it_secret_is_it_safe_-_how_to_hide_api_keys)

Also, our application allows users to search for current weather in a city of their choice.


### IMPLEMENTATION 

Since we want users to be able to input a city's name and return the query's data, we need to have two state functions; since we need to manage two values. Remember, the `useState()` method allows us to *manage state locally.*

``` const [ query, setQuery ] = useState("")```

``` const [ weather, setWeather ] = useState({})```


**NOTE**: Query's initial state is set to an empty string, and the input field renders as blank. Weather's initial state is an empty object which holds the query's request.

Now let's add the input field for the search bar, button, and add an *OnClick event *to it.

``` 
<div className="search-box">
        <input 
           type='text'
           className="search-bar"
           placeholder="Search for Forecast"
           onChange={ e => setQuery( e.target.value ) }
           value={ query }
         />
        <button 
	         type="button"
	         onClick={ searchCity }
        >Search</button>
 </div> ```
 
**NOTE:** We are passing the event and the `setQuery` method to an anonymous function on the `onChange` event. Also, we need to define a `value` property to the input field and set it to our query variable. In our `onClick` event, we need to pass it out search variable so we can interpolate it into our fetch-request. 

Then, we are going to define a search method that fetches the requested query's data. This method should look similar to fetch-request you might have made in the past, but you'll notice we are using our `setState` methods in our request. 

```
const searchCity = e => {
            fetch(`${baseURL}weather?q=${query}&units=Imperial&APPID=${apiConfig.apikey}`)
            .then(response => response.json())
            .then(data => {
                setWeather(data)
                setQuery('')
            })
    }
```

**NOTE:** The Query is interpolating into the URL address, and we pass the return data to our `setWeather` method. And that's it!

![](https://media.giphy.com/media/8hxcSjDr51mes/giphy.gif)

Now in our return statement, we can call any property in our return data set. How easy is that?

Well done everyone, I hope this post helped hook-up your React components!  

See ya next time!

![](https://media.giphy.com/media/bOjatt5T6cKyI/giphy.gif)

