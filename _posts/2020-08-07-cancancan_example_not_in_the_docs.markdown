---
layout: post
title:      "CanCanCan Example Not in the Docs"
date:       2020-08-07 11:46:10 -0400
permalink:  cancancan_example_not_in_the_docs
---


![](https://media.giphy.com/media/3oxHQxjLr5hYZ83ztC/giphy.gif)

This week we are going to talk about the authorization gem `cancancan`. I imagine most Rails developers have used this gem before, but I wanted to share a usage case that I didn't find in the documentation. 

I've written about my Rails fitness-donation based app, SweatClause, many times because developing it has forced me to push my understanding of Rails, and I'm learning more advanced concepts. This week is no different. 

"[CanCanCan](https://github.com/CanCanCommunity/cancancan) is an  authorization library that restricts what resources a given user is allowed to access."

Easy enough concept to understand. If an object doesn't *belong* to a User, they cant write over it.  If you aren't picking up what I'm putting down, the rest of this post will lack context. I'd recommend checking the basic example in the README. 

In [SweatClause](http://radiant-wave-27873.herokuapp.com/), I wanted my Group model to have a 'commissioner' or 'owner.' This commissioner would be responsible for managing all aspects of the Group, from adding new members to starting new fitness challenges. The issue I ran into was that all the group members have access to the Challenge since a Challenge belongs to the Group. CanCanCan makes this simple if you're great at inferring technical documents.

![](https://media.giphy.com/media/e3X9ZcuLp1QgE/giphy.gif)

If not, I hope this example helps you better understand the flexibility of CanCanCan's abilities. 

Here's a little context before we dive in.

![](https://i.ibb.co/RY3dfTx/Sweat-Clause-Schema.jpg)

A Group:
```

	has_many :users, through: :memberships
	
    belongs_to :owner, class_name: 'User', foreign_key: :owner_id
	
	has_many :challenges
	```
	

In the second line, I am "aliasing," an instance of a User as an owner. User's `has_many :groups` so the alias distinguishes the User who creates the Group as its `:owner`.

```
      def initialize(user)
          ...
	       can :update, Group do |group|
           group.owner == user
         end
         can :destory, Group do |group|
           group.owner == user
         end
      end  
```


How cool is that?

![](https://media.giphy.com/media/tgyvnnF5AYi9a/giphy.gif)

We need to add an "ability check" that encapsulates the Group#Update/#Destroy links over on the Group#show page. 

```
....
<% if can? :update, @group %>
	<h4>Commissioner Tools</h4>
	<%= link_to("Add New Member", edit_group_url(@group)) %>
	<%=link_to("Add New Challenge", new_challenge_url(group_id: @group.id))%>
  <%= button_to("Destroy Group", @group, class: "btn btn-warning", method: :delete, data: { confirm: "Are you sure?"}) %>
<% end %>
```

That's all there is to it. I wish the documentation would show more examples that are simple, like the one I just shared. I think these gems would get even more usage from newer-programers that might otherwise be intimidated.  



