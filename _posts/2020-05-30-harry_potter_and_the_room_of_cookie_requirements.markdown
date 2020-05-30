---
layout: post
title:      "Harry Potter and the Room of Cookie Requirements"
date:       2020-05-30 18:02:30 +0000
permalink:  harry_potter_and_the_room_of_cookie_requirements
---



I've spent a lot of time recently working on authentications for various web apps.   While I have a strong understanding of how tables relate to each other, when I add authentication to the mix, it makes my head spin.

![](https://media.giphy.com/media/AavShiUVw7QmQ/giphy.gif)

So this week, I figured I would sharpen my understanding of one of the critical elements in authentications...Cookies. 

### What is a Cookie?

Cookies are like secret handshakes. A cookie is a small piece of data that the User's browser stores. This little piece of data is sent to the server to allow a user to access their data at a later time. Cookies are a cog in the HTTP State Management Mechanism. The documentation says:

*"To store state, the origin server includes a Set-Cookie header in an HTTP response. In subsequent requests, the user agent returns a Cookie request header to the origin server. The Cookie header contains cookies the user agent received in previous Set-Cookie headers. The origin server is free, too...use its contents for an application-defined purpose."*

That is super boring, and if you are anything like me, it took three tries to understand what that is saying. That's not efficient at all. So let's use an example more of us can relate with. 

### Why is it like a secret handshake?

Think of it like this: In "Harry Potter and the Deathly Hallows", The Order of the Phoneix is worried about the Death Eaters using Polyjuice Potion to impersonate other members of the Order. Obviously, this a legitimate problem as a Death Eater can relay secret information of the Order's plans to *He-who-must-not-be-named*.

![](https://media.giphy.com/media/fSvtd1UUf8Ot2/giphy.gif)

So to protect themselves from infiltration, two members of the Order, Kingsley Shacklebolt and Remus Lupin, come up with an idea that equates to a *Wizard-cookies-requirued-authentication*.

Whenever two members of the Order meet, they hold the other at wand-point and ask the other member a question that only that real wizard know and stump an imposter.
For example, after the Death Eaters foil the Order's plan to sneak Harry out of #4 Privet Drive, Lupin and Kingsley are two of the first to make it back to Burrow. Upon seeing each other Kingsley point his wand at Lupin and asks him:

![](https://media.giphy.com/media/13CK4GhUKP9x3q/giphy.gif)

Remus replies,

*"Harry is the best hope we have. Trust him."*

No pressure, Harry.

![](https://media.giphy.com/media/Gn9hk1Pi8mr3a/giphy.gif)

That is the essence of a cookie. This one piece of data is transferred between two sources. The result, the server/Kinglsey, knows he is interacting with the real user/Lupin. The benefits of this are that the two wizards can quickly and efficiently verify who they are and get back to taking down Voldemort.  


So let's briefly leave the wizarding world and speak more practically. Let's say you run a grocery delivery web application, and you want to use cookies to verify the User attempting to view the cart. When a user creates a grocery cart the server assigns a cookie through the `Set-Cookie` header:

#### Server to User: 

```Set-Cookie: cart_id=42```

The id number is assigned when a User adds an item to an empty cart.

#### User to Server:

```Cookie: cart_id=42```

Later on, when a User comes back to the web app that id number is a part of their GET request the server.

One last thing is to talk about before we leave this analogy. Cookies are stored as plain text that shows up in a user's browser when they make a GET request. That means the id is visible to the User. Now let's say you are on a community wifi network in a coffee shop. Since your cookies are stored locally and appear in the browser, a coding ne'er-do-well can potentially also see your cookie id. Ruby on Rails gives users and servers a solution that's way better than some protection charm to address this vulnerability. 

### The Session Method

![](https://media.giphy.com/media/3o7525qDu9KTSMERmo/giphy.gif)

The session method is no mere protection charm but rather think of it as the Room of Requirement. The Room of Requirement is a magic room at Hogwarts that when a student needs something, say a private place to practice spell work, the room appears and is filled with the items required for their activity. It doesn't matter what you need; the room will provide it. Also, the room will remain hidden from those wizards you want to hide from. So when Harry and the DA are practicing Defense Against the Dark Arts spells, Draco, Umbridge, and Snape can't find the room. That's the session method; it stores anything you want even if your application doesn't have a model for it. The session method hides the cookie from everyone you don't want to see it, only becoming visible to the required parties.


``` session[:cart_id] = @cart.id```

This is placing the id inside of the 'square brackets of protection.'

``` @cart= Cart.find(session[:cart_id] ```

This loads the cart_id that was referenced in the session and assigns it to an instance of the cart. 

I know that is a bit of a story for some context, but to understand how programming works, we first have to find parallels to our experience. The subject of cookies is essential in modern web development. We all use them every day, whether we are ordering a cart of items on Amazon or posting the next chapter of our Harry Potter Fanfiction series. 

![](https://media.giphy.com/media/q6DyfZvLq07IY/giphy.gif)



