---
layout: post
title:      "Remember Me!! Rails authentication with Cookies"
date:       2020-06-13 16:16:59 +0000
permalink:  remember_me_rails_authentication_with_cookies
---


Hello again! I have written several blogs about my fitness-charity Rails app, SweatClause, and this week I will cover an issue I ran into while testing my app live with some users. The day after I had some of my friends start using the app, my buddy Stephen called me and asked me a question that hadn't crossed my mind during development: "Can you make it so I don't have to login every time?" 

![](https://media.giphy.com/media/l4ik5ArIwSuq9stOrm/giphy.gif)

I said, give me a few days and went to work. Here's what I did:

This blog assumes you are using `bcrypt`. 

Check out this [blog](https://christopherkalfas.github.io/rails_authentication_this_isnt_my_data) to see how I set up my sessions controller in more depth.

In my sessions controller, I am creating a session when a user logs in and destroying it when they log out. It works great, but the temporary nature of the Rails sessions don't work for a remember me feature. 

`session[:user_id] = user.id`

`session[:user_id] = nil`

Instead, we will use cookies!

For a brief look at cookies, please take a look at my previous blog post. 

[Harry Potter and the Room of Cookie Requirements](https://christopherkalfas.github.io/harry_potter_and_the_room_of_cookie_requirements)

Like the wizards in my last blog, we want a permanent and unguessable 'handshake' or 'token' that we can store in a cookie. Also, we want each user to have their unique handshake with the app. 

![](https://media.giphy.com/media/T9JPznkGDAxYC8m7yC/giphy.gif)

So let's add a column for an authentication token to our User model. 

`rails g migration add_authentication_token_to_users authentication_token:string`

Great! Before we move forward **remember to migrate your database** to include the new column

`rails db:migrate`


Next, head over the User model. We need to write a method that generates a random token for a user. I used this template I found on [RailsCasts](http://railscasts.com/episodes/274-remember-me-reset-password). 

```
def generate_token(column)
    begin
        self[column] = SecureRandom.urlsafe_base64
    end while User.exists?(column => self[column])
end 
```

Let's break that down: 

* The method takes a variable with the name of `column`, which helps when you want to add multiple tokens down the road. 

* Then the `SecureRandom` method generates a random string to assign to the column variable, which is a part of ActiveStorage. 

* Next, the `end while User.exists?` says if the random string is the same as another user's token, run the random string block again. 

The last thing we need to do in the User model is to add a `before_create` method to implement the token.

` before_create { generate_token(:authentication_token) }`

Great job! Now we want to update the sessions controller to use our tokens *instead* of the session's user-id. We are making changes in the `create` and `destroy` methods.


* Create method before: 
`session[:user_id] = user.id`

* Create method after:
`cookies.permanent[:authentication_token] = user.authentication_token`

* Destroy method before:
`session[:user_id] = nil `

* Destroy method after:
`cookies.delete(:authentication_token)`

Technically we are done, but there's one more thing to consider. Our `remember_method` should be *conditional*. If a user is logging in on a shared computer, we don't want to rely on a user logging out of the app before they stop using the computer. So to remedy this, let's add a checkbox to the login form.

```
<div class="form-field>
	<%= label_tag :remember_me %>
	<%= check_box_tag :remember_me, 1, params[:remember_me] %>
</div>
```
**Note**: the `1` in the `check_box_tag` means the checkbox *has* been clicked.

Now we need to reflect the checkbox logic in the sessions controller. If the `remember_me` params exist, then checkbox is filled, and the cookie is permanent. Else, the cookie is temporary for this session.

```
if params[:remember_me]
    cookies.permanent[:authentication_token] = @user.authentication_token
else 
    cookies[:authentication_token] = @user.authentication_token
end 
```

The final piece of this feature is refactoring our `current_user` method in our Application Controller to utilizes our cookies.  

We need to change:

```
def current_user
	@current_user ||= User.find(session[:user_id]) if session[:user_id]
end 
```
to:

```
def current_user
   @current_user ||= User.find_by_authentication_token!(cookies[:authentication_token]) if cookies[:authentication_token]
end
```

And there you have it, folks! Now, your web application can save users the time and effort of remembering and typing in your password. 

![](https://media.giphy.com/media/dWBMD6TlccykkD65BV/giphy.gif)



