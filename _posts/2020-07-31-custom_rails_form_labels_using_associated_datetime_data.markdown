---
layout: post
title:      "Custom Rails Form Labels Using Associated Datetime Data"
date:       2020-07-31 21:09:22 +0000
permalink:  custom_rails_form_labels_using_associated_datetime_data
---



Hi, everybody!

A few weeks ago, I wrote a [blog](https://christopherkalfas.github.io/custom_collections_in_rails_forms) about customizing `collection_select` in a Rails form. This week I'm going to write about more ways of customizing Rails forms. 

This time, we will cover how to **render custom labels for a child-model's form based on its parent's attribute values**. There is lots of documentation about nested forms and attributes examples; where a developer needs the child model information to render inside the parent's form. So, I figured it would cool and helpful to show how to do it the opposite way. 

![](https://media.giphy.com/media/idw3dW74u7VT9EfO4e/giphy.gif)


Before we dive in, here's some context. A Tracker is the join model between a User and a Challenge.

![](https://i.ibb.co/RY3dfTx/Sweat-Clause-Schema.jpg)


While working on [SweatClause](http://radiant-wave-27873.herokuapp.com/), my fitness based charity-donation app, my buddy asked if I could format the fitness Tracker's form labels to match the days in the Challenge.

When I originally built the app, Challenges had to start on Sundays and end Saturdays. That way, I could 'hard-code' the form label with the corresponding days of the Challenge. 

```
<%= form_for(@tracker) do |f| %>
    <div class="form-group pt-2">
        <%= f.label "Sunday: "%>
        <%= f.number_field :sunday_reps, maxlength: 10%>
    </div>
    <div class="form-group">
        <%= f.label "Monday: "%>
        <%= f.number_field :monday_reps, maxlength: 10%>
    </div>
```



![](https://i.ibb.co/jZMBZbk/trackerformhardcode.png)

However, as the app has evolved, I redesigned the Challenge to start any day of the week. 



So now we need to figure out how to use the Challenge dates in the Tracker form. 

We will walk through how to implement this following Rails MVC.


### Model

For starters, we need to define an instance of a Tracker to `accepts_nested_attributes` for `:challenge`.

**NOTE** since we are going the reverse-path up to the parent, the parent model is the *singular tense.*

In `tracker.rb`, we need each instance of a Tracker to return the `:start_date` from the Challenge associated with it. We need to do this for *each* day of the Challenge.

```
    def challenge_start_date
        self.challenge.start_date.strftime("%a #{self.challenge.start_date.day.ordinalize}")
    end
```

Breaking this down, we can see an instance method, which calls the Challenge's `:start_date` attribute for *itself*. Then using the `strftime()` method, we format the returned day value.

In Rails, `datetime` is stored in the database with the following formatting, 

`"YYYY-MM-DD HH-MM-SS"` 

We want the day of the week and the day of the month.

`.strftime("%a #{self.challenge.start_date.day.ordinalize}")`   

So, `2020-07-27 04:00:00` becomes `Mon 27th`. If you aren't familiar with `datetime` formatting, here is a great [cheat sheet](https://www.shortcutfoo.com/app/dojos/ruby-date-format-strftime/cheatsheet). 



In the argument of `strftime()` we are passing in just the `day` of the `start_date`. Then we are using the `ordinalize` method to add the appropriate day suffix, i.e. "st," "nd," "rd," and "th."

Now we need to do this for the next six days of the Challenge. Pulling this off is barely an inconvenience with the help of the `next_day()` method. 

To get the second day of the week formated, we simply pass in how many days we want 'next-ed.' So for the "Tue 28th." 
```
def challenge_day_two
    self.challenge.start_date.next_day(1).strftime("%a #{self.challenge.start_date.next_day(1).day.ordinalize}")
end
```

It's the same thing as above, but we replaced `day` with `next_day(1)`.  Then we repeated that method for the remaining days of the Challenge. 

Pretty cool, right?

![](https://media.giphy.com/media/W038TiB3SHLIBAnkYM/giphy.gif)

The last step in the model is optional but suggested to make the controller logic more straight forwards. We need to define a method that calls the individual instance methods for each day of the week. 

```
def challenge_info
    challenge_start_date
    challenge_day_two
end 
```

Great, now let's move the `trackers_controller` logic.

### Controller

We need to add the `challenge_info` methods to the `:new` and `edit` methods, so the tracker form as access to those methods *before the form is created or updated.*

```
    def new
        @tracker = Tracker.new(challenge_id: params[:challenge_id])
        @tracker.challenge_info
    end

    def edit
        @tracker = Tracker.find(params[:id])
        @tracker.challenge_info
    end
    
```

See why we wrote the `challenge_info` method now? We are all done here. So let's move to the last component, the View. 


### View

In `_form.html.erb` in the Tracker's folder, we are going to replace,

`<%= f.label "Monday" %>`

with...

`<%= f.label @tracker.challenge_start_date %>`

Then we can repeat the process for the following days. 

![](https://i.ibb.co/h84kyyg/trackernestdataform.png)

Boom! Looks beautiful! Well, it isn't very D.R.Y, but it works! 

![](https://media.giphy.com/media/7EeREHnUCOoUZMjTGO/giphy.gif)

Maybe that will be next week's post. 
I hope you found this helpful in your efforts!
