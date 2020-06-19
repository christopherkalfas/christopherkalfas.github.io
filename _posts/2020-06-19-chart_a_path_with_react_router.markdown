---
layout: post
title:      "Chart a Path with React Router"
date:       2020-06-19 13:52:40 -0400
permalink:  chart_a_path_with_react_router
---


Hello, everybody! This week I wanted to talk to you about one of my favorite React Libraries, React Router.  React applications are shine as Single Page Applications. If you are new to React Router, I hope you find yourself wondering why I need to router for users if my application always stays on the same page?


Great question! Let's discuss this. 

![](https://media.giphy.com/media/Kx7HO28xRu1cG8S3GB/giphy.gif)


### Single Page vs. Multi-Page

I find it easier to explain what a Single Page App is by first thinking about what a Multi-Page application is.  Multi-Page apps work like how most people's imagine a 'traditional' website. When a user makes a change, a POST request sent to the server, and once the server accepts the change, the user is redirected to a different page. 

For example, if a user is creating a new profile, they click on the 'Sign up' button on the 'home' page. That click would route them to a different URL where they can fill out the user profile form. Upon submitting their input, the data is sent back to the server, and the user is redirected to the user index page. So for that one user story, the user is being taken to three different pages. The downside of Multi-Page apps can make the user experience slow and cumbersome. If your website is slow, users won't keep using it.  

![](https://media.giphy.com/media/bMdZu3fG2ZEBO/giphy.gif)

Thanks, Gloria! I bet she would like the app if it used the more modern convention of SPAs. See what I did there? 

So now that we see how a Muti-Page app works, we can talk about SPA's. 

SPA's are designed to work inside a browser, and they don't need to reload pages during user interaction. These are applications we consider to be more 'modern.' For example, GitHub, GoogleMaps, and Facebook are SPA's. The primary objective of a single page app is *speed*. SPAs are a combination of HTML, CSS, and Scripts. These resources only get loaded once during a user's interaction. Only the data being updated or rendered will change. A SPA will only update the part of the DOM that has changed and leave everything else on the page. The SPA only has to evaluate the change and not the entire page. 

![](https://media.giphy.com/media/lCbSAbRrFEfkY/giphy.gif)

Awesome! We can see the benefit of the SPA, but that still doesn't explain React Router. 

The Router allows users to 'link' to specific URLs or components; however, The Router is playing a hide-in-seek game with different components based on the 'link.' 

If I navigate from the home-page to the form-page and then the profile page, React Router, hides the home component, renders and replaces it with the form. Upon submitting, React Router then hides the form and renders the all-users page. In the browser URL, you see this 'navigation.' 

Example:

* Home Page - `https://www.my-app.com/`

* Form Page - `https://www.my-app.com/users/new`

* All-Users Page - `https://www.my-app.com/users`


Pretty cool, right? Alright, before we wrap up this blog, let's walk through a quick practical example. 

#### Home-Page Routing

![](https://media.giphy.com/media/llmrnMkLqcssM6sYG7/giphy.gif)

In our index Page, we want to import React Router to gain access to its functions. In this case, the Router and Route.


``` 
import React from "react"
import ReactDOM from "react-dom"
import { BrowserRouter as Router, Route } from "react-router-dom"
```

Next, we will define a functional Home component. 

```
const Home = () => {
	return(
		<div>
			<h1> Welcome Home! </h1>
		</div>
	)
}
```

Then, we need to declare where we want to use the Router. The Router is the parent element of the Route element and needs to be nested. 

The Router contains the Routes, and the Route, takes two props; `path` and `component.` The Route's job is when a URL matches a specific path, I'm going to render that specific information.

```
ReactDOM.render((
	<Router>
		<Route path = "/" component={Home} />
	</Router>),
	document.getElementById('root')
);
```

Boom! That's all there is to it!


One last point of importance with `<Router>` is that it can only have one child. So as you continue to add additional routes, remember to wrap them in a `div`. 

```
ReactDOM.render((
    <Router>
	<div>
          <Route path = "/" component={Home} />
		  <Route path = "/login" component={Login} />
		  <Route path = "/users" component={Users} />
	</div>
    </Router>),
    document.getElementById('root')
);
```

Okay, now I'm done. Go forth, navigators, and create a beautiful UX and astound Users with its lightning-fast 'navigation.'

![](https://media.giphy.com/media/xULW8hMSH4DocTpqko/giphy.gif)
