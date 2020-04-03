---
layout: post
title:      "Rails Generator Commands - rails generate blog"
date:       2020-04-03 16:16:44 -0400
permalink:  rails_generator_commands_-_rails_generate_blog
---

![](https://media.giphy.com/media/26BRuo6sLetdllPAQ/giphy.gif)

While Mother Earth has recently grounded all her children and sent us to bed without dinner or toilet paper, humanity must press on. My contribution to fight the stuck-at-home blues has encouraged me to host a web app I made months ago. Sweat Clause is the brainchild of my friend Stephen. Stephen has been organizing a push-up competition among our circle of friends on Google docs. As I am not a doctor and my medical knowledge was acquired exclusively from House MD, I have been thinking, how can I help combat COVID-19.

![](https://media.giphy.com/media/63VH5uoslatcA/giphy.gif)

As a web developer, I can use my technical skills to help my circle of friends stay in shape. And since we are all home-locked, I told Stephen I would turn the Google doc into a hostable web app. 


While building out the app and shaking off the rust on my Rails skills, there was one tool I was continually looking up for syntax. Rails has command line generate tools that allow developers to build the basics of their app quickly and lets them focus on the specifics of their application. There are a lot of CLI guides, but not many that are a "one-stop-shop." So, the light bulb for my next blog post materialized before me.

![](https://media.giphy.com/media/Mjq9vmDuJlBKw/giphy.gif)


### BASICS

Rails has all its functionality and helpful information built inside of it. You can run `rails generate` in the terminal, and Rails will output a list of ALL available generators options. 

Running, `rails generate GENERATOR --help`, will return all the options that can be *passed to the generator*.

Also, you can use an *alias* for the generator, substituting the word 'generator' for the letter 'g.'

`rails g --help`

### CONTEXT
When I learned how to use Rails, I followed a useful convention called "MVC." **Model-View-Controller**. Rails generator commands also utilize this convention, and as a developer, we can decide how much of our web app we want Rails to build more use. I'll start with the least amount of work for Rails and finish with Rails, basically making the whole app.

#### *MODEL*
We can build our models and include their attributes and associations using the model generator commands. The controller and views folders are completely omitted. 

`rails g model User name:text age:integer`

#### *CONTROLLER*
This generator includes everything above plus the corresponding controller file, which has no methods inside of it. 

`rails g controller user`

#### *RESOURCE* 
In my opinion, this is the most practical level of building for Rails.  You use the name of the resource you want to create, as well as including model attributes, associations, controllers, routes, and empty view folders for the resource. 

`rails g resource user name:text age: integer group:references`

#### *SCAFFOLD*
Lastly, when using the scaffold generator, be sure to remember the words of Uncle Ben. "With great power comes great responsibility." The scaffold command creates the ENTIRE resource. It creates the:

* migration
* model
* controller with actions
* views with basic UI
* RESTful Routes

In my experience, the scaffold generator does too much and requires you to refactor your starting code. I would recommend using the scaffold generator as an exploratory tool, not something that should be in your everyday arsenal.

`rails g scaffold user name:text age:integer group:references`

![](https://media.giphy.com/media/FUNDvNuzqdKTu/giphy.gif)

#### *OTHER IMPORTANT STUFF YOU SHOULD KNOW*

#### **NAMING CONVENTIONS**
***MODEL***
* Written in *CamelCase*
* Written in the *singular  tense*
* Columns are written in *snake_case*


***CONTROLLER***
* Written in CamelCase
* Written in the plural tense
* Actions or methods use *snakecase*


***RESOURCE***
* Written in *CamelCase*
* Written in the *singular tense*
* Columns are written in *snake_case*



***SCAFFOLD***
* Written in *CamelCase*
* Written in the *singular tense*
* Columns are written in *snake_case*


#### **COLUMN TYPES:**
* :binary
* :boolean
* :date
* :datetime
* :decimal
* :float
* :integer
* :primnary_key
* :string
* :text
* :time
* :timestamp

Whew, that's a lot of information, but there are many more tools available. Rails allows you to generate your migrations, helpers, views, mailers, observers, integrations, features, and jobs.  I encourage you to take an afternoon and explore these other generators. And remember to use your new powers for good and maybe a little self-gain.

![](https://media.giphy.com/media/ek4CUx2FONgHaMz9V5/giphy.gif)




