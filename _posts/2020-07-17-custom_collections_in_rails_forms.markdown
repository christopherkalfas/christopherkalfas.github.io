---
layout: post
title:      "Custom Collections in Rails' Forms"
date:       2020-07-17 12:50:41 -0400
permalink:  custom_collections_in_rails_forms
---


Hi everybody! This week I'm going to talk about customizing the `collection_select` input field in a `form-for` in Rails. 

If you read my blog last week, you'll notice that I often get annoyed with lousy documentation. The Rails Docs, in my experience, are very hit or miss. The explanation of `collection_select` is pretty rough. 

![](https://media.giphy.com/media/2w6I6nCyf5rmy5SHBy/giphy.gif)

Before we dive in, let's set up our sandbox with some example models.


* **User**
 
 *has_many* :memberships
 
 *has_many* :groups, *through*: :memberships
 
 *has_many* :owned_groups, *foreign_key:* 'owner_id', *class_name:* 'Group'


* **Group**

 *has_many* :memberships

 *has_many* :users, *through:* :memberships
 
 *belongs_to* :owner, *class_name:* 'User', *foreign_key:* :owner_id


* **Membership**

 *belongs_to* :user

 *belongs_to* :group 
 
 
 
 **NOTE** 
Also, only group **OWNERS** can add/remove another member of the group. A new user *can't* join an existing group. 


![](https://media.giphy.com/media/3owzWl78kny9s2GOvC/giphy.gif)

Here is an example of a membership `form_for` with `collection_select`.

```
<%= form_for @membership do |f| %>
	 <%= f.collection_select :group_id, Group.all, :id, :name %> 
	 <%= f.collection_select :user_id, User.all, :id, :name %>
	 <%= f.submit %>
<% end %>
```


Let's break this down.

This form will work but isn't what we need. Anytime a group owner wants to add someone new, they will have access to add a member to ANY group, not just the ones they own. No good!

Also, the collection of users accesses all users, *including* the group owner and every current member of the group.  That is really no good! So it looks like we need to customize the arguements of `collection_select`.


Let's see what the [Ruby docs](https://apidock.com/rails/ActionView/Helpers/FormOptionsHelper/collection_select) say about how to acomplish this.

```
collection_select(object, method, collection, value_method, text_method, options = {}, html_options = {})
```

I mean, come on y'all. All I get from this is the `collection` argument is the one we need to change. But it doesn't really explain how. 

![](https://media.giphy.com/media/kQOxxwjjuTB7O/giphy.gif)

Looks like we are on our own. 

The boilerplate gives us a varibale of `collection` and we need to assign it to an array of group instances. We can use the `:owned_groups` relationship-alias and the `current_user` method from our authentications(bcrypt, devise, etc...)


For a group owner to only have a collection of THEIR owned groups, I passed `current_user.owned_group` as the collection and left everything else the same. 

`<%= f.collection_select :group_id, current_user.owned_groups, :id, :name %>`

This works great, but we can take it one step further. What if I only want the owner to add a member to the group they are currently associated with? 

Rails makes that super easy to accomplish with associations. Instead of having a separate form for membership, I moved the logic into the *groups form*.

To get the *controller* working, we need to add one line of code to the `edit` method, and two code lines to the `update` method.

```
    def edit 
   	 @group = Group.find(params[:id])
   	 @users = User.all <--- new line
    end 

    def update 
        @group = Group.find(params[:id])
        @user = User.find(params["user"]["id"]) <--- new line
        @group.users << @user <--- new line 
        if @group.update(group_params)
            redirect_to group_path(@group)
        else
            render :edit
        end 
    end 
```


Now, when we update, we can use the user instance variable to grab the user's id and *push* them into `@group.users`.  No need to put this in the membership controller. And we don't have to account for the `group_id` in our views. 


![](https://media.giphy.com/media/7pLv68ItwBaHS/giphy.gif)


Now, let's talk about how to give `collection_select` a collection of users who are **NOT** in the group. That means we need to remove the users who are *already in the group*. 

In the group model, we can write a custom instance method to return an array of users, NOT in this group. 

```
def not_in_group
   User.select {|user| user.groups.pluck(:id).exclude?(self.id)}
end
```

Let's break this down. If you aren't familiar with `pluck()` now is your chance. `pluck()` is a select shortcut that can grab one or more instance attributes without the server loading a bunch of data you don't need. 


Just like before with `@group.users`, we can can  `user.groups`. We can pass `pluck()` the `:id` attribute. This gives us an array of just the `group_id`s associated with users. Then, we can chain `exclude?()` to the end. 

Remember that in Ruby, *defining a method that ends in a `?` means it returns a **boolean***. That means if the group instance does see another instance of itself(`true`) in `user.groups`, it can *exclude* that instance of user from the returned array. If the group instance doesn't see its self(`false`) in `user.groups` it ** WILL** add that user to the selectable collection of users.

That was a lot of logic in one line of code. Ruby is the coolest.

Now we can just add that custom instance method as the `collection` argument in group form.


```
<%= collection_select(:user, :id, @group.not_in_group, :id, :name) %>
```

![](https://media.giphy.com/media/vN3fMMSAmVwoo/giphy.gif)

There are several other ways we could have accomplished this.  Maybe some that are much easier to implement than what we just did? I have no idea because this stuff isn't well documented.  If you know of other ways to accomplish this, please shoot me a note on [LinkedIn](https://www.linkedin.com/in/christopherkalfas/) and impart your wisdom upon me. 


 
