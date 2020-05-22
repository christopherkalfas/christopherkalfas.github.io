---
layout: post
title:      "Rails Authentication: This isn't my data!"
date:       2020-05-22 16:25:53 +0000
permalink:  rails_authentication_this_isnt_my_data
---


Hi gang! This week I wanted to take a more focused approach to a topic that, frankly, has kicked my butt. It's a little embarrassing with how many backend projects I've worked on that I couldn't figure this out. But hey, as Hugh Jackman once said, "This is me!"

![](https://media.giphy.com/media/l4FGD5KYukbHukdG0/giphy.gif)


I mentioned a few weeks ago that I have been working a project for my friend, Stephen. He has been running a push-up competition between a group of our high school friends in a Google Doc. So I have challenged myself to build it out. 

The issue was not allowing Users to edit the fitness tracking numbers of other competitors. I thought first about only rendering the current User's data to the view page. But there was another problem. To make the application feel competitive, I wanted to have the other challengers' data rendering with current User's trackers. So, everyone in the competition can see where they are goal wise versus their competitors. The overarching problem was once a User had the scoreboard rendered to the DOM, they could change a User's stats. I already had a before action to authenticate that they are part of the Group competing I was missing the need for another authentication check if the object they were changing was theirs.

![](https://media.giphy.com/media/Wt0I5MEACAFb4SAOsV/giphy.gif)

A few things about this project to note:
* Built on Rails

* Utilizing `bcrypt` gem

* User authentication is handled by a 'Sessions' Controller

* The table relations relevant to this blog are:
         1. A User has many Trackers
         2. A User belongs to a Group.
         3. Tracker belongs to a User and a Challenge.
         4. A Challenge belongs to a Group.


So before I walk through this, here a quick summary of what we are going do work towards. 

Our end goal is to create a `:correct_user` helper method to check *if the current User the owns the tracker object they were attempting to modify*. We are going to accomplish by modifying two of SweatClause's controllers.

* Application Controller

* Trackers Controller

#### Application Controller
Our application's first step to check if the current User is the correct User; we need to determine who the current User is.
 
```
def current_user
    user_id = session[:user_id]
    user_id && User.find(user_id)
end
```
 
 Let's break this down. We are assigning the User id that belongs to the current session to a variable called `user_id`. Then we are using a double ampersand(`&&`), which causes the method to return `true` if both conditions are valid or `false` if either condition is invalid.
 
![](https://media.giphy.com/media/l41JQAOSwDqTAi54A/giphy.gif)

The last thing we need to do in this controller is 'export' our method by defining it as a `helper_method`.

`helper_method :current_user`

Boom! Moving right along.

#### Trackers Controller

We need to create a `private` method called `correct_user`, which handles the logic of the authentication and a `before_action`, that tells Rails which routes it need to check who the User is before fulling the request.

```
def correct_user
    @tracker = Tracker.find(params[:id])
    unless @tracker.user == current_user
         redirect_to challenge_path(@tracker.challenge), notice: "Not your tracker, bro!"
    end
end
```

First, we are assigning an instance variable to the `find()` method passing the instance's id. We use conditional logic to say that ***unless*** this instance's `user_id` is equal to the current User, redirect them away from the 
form. 

![](https://media.giphy.com/media/3otPoFUhO2Z9uG1Qvm/giphy.gif)

**NOTE:** We can call the `current_user` in `trackers_controller.rb` method because we defined it as a `helper_method` in our Application Controller. 

The last thing we need is the `before_action` and which routes we want to call the action on.

`before_action :correct_user, only: [:edit, :update, :destroy]`


We are only running the authentication when a User tries to edit, update, or destroy another User's data. We want them to be able to see the other User's data. We don't need to worry about `:new` either, as a tracker can only be created with the id of the currently signed in User. 

And there you have it, folks! Now, a User can see other competitors' data, but when they try to make a change to it, it shuts them down! Now my friends from high school have no excuse not to get in shape! 

![](https://media.giphy.com/media/Uno27COfoYlH2/giphy.gif)
