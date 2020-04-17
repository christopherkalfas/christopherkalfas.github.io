---
layout: post
title:      "Python Basics: Why'd it have to be snakes?"
date:       2020-04-17 14:38:08 -0400
permalink:  python_basics_whyd_it_have_to_be_snakes
---

![](https://media.giphy.com/media/xUPGchE5UWpMeWJlvO/giphy.gif)

As I have been looking for a job, I have talked to several recruiters and hiring managers about the technical skills they value most. For the front-end, JavaScript/React has been the most prevalent. Python seems to be the most pervasive backend language the recruiter I've spoken to. So, I figured I'd start learning it. 


A lot of Python videoes and courses gear themselves toward people who are picking up their first language. When I was learning Ruby, I needed a course that was geared that way, but now that I have a solid understanding of object-orientated programming, I found that the Python basics were slow. So I figured I'd try to offer a launching-off point for other developers who are new to Python but have OOP experience. 

 ![Here we go!](https://media.giphy.com/media/uELDhoOZdSnUk/giphy.gif)

## WHAT IS PYTHON?

Python is a *general-purpose language*. This type of language can be used for pretty much anything. Python is used by some of the biggest companies on the planet. To name a few:

* Google
* Facebook/Instagram
* Netflix
* Reddit
* Spotify
* OkCupid
* Disney/Pixar/Lucasfilm
* The Onion
* The US Government



That's crazy! All those companies/entities offer completely different services to users, but Python's flexibility has mass appeal to developers. 

![](https://media.giphy.com/media/l1KuhBCqxOoJyr0m4/giphy.gif)

#### **File Structure** 
* Files are saved using `.py` 
* *Example:* `hello_world.py`
	
####	**Python Shell** 
* From the terminal, run `python` to open a *REPL* or the *Python Shell*. The REPL allows you to 'try-out' code snippets without running the entire file. 
* Similar to the way you'd open the Rails console with `rails c`.
	
	
#### **Running Scripts** 
* From the terminal, run `python hello_world.py` to run our file through the Python interpreter.

#### **Naming Conventions** 
* Python uses *snake_case*, which you probably could have guessed.

![](https://media.giphy.com/media/Lndtxw3ztLhNC/giphy.gif)

#### **Shell Output** 
* For the interpreter to output data to a user, Python uses `print()`.
* *Example:* `print("Hello, world!")`
 
#### **Variables** 
* Declaring and defining variables in *Python are very similar to Ruby*. 
* Variable names can use letters and numbers but should begin with a lowercase letter or an underscore. 
* There is no need to define a variable with a `var` or `let` like in JavaScript.
	
	 *Example:*
     * Ruby:  `greeting = "Hello, World!"`
     
     * JavaScript:  `let greeting = "Hello, World"`
     
     * Python:  `greeting = "Hello, World!"`

* Now, you can pass the greeting variable to the print method.
* *Example:*  `print(greeting)`

#### **String Interpolation** 
* Python allows a few different ways to customize strings. When using the print method, a comma can be used to separate the reusable part of the string from the part we want to be interpolated.
* *Example:*
```
name = "Bob"
print("Hello, ", name)
```

*ALSO*
* Python also utilizes curly brackets for interpolation with a format method, that is called at the end of the string. **NOT** the end of the print function
* *Example:*
```
name = "Bob"
print("Hello, {}! Welcome to Python!".format(name))
```

#### **User Input** 
* Outputting relevant information is essential to creating an application, but how do we handle gathering information from the user? Python's ease of use shines using the input command.  Whatever the user inputs is then output through the shell. If we want to reuse the user input, we can store the input function to a variable.

* *Example:*
```
user_name = input("What is you name? ")
```


*ALSO*

* Whatever the user types as a response to the question, returns as a **STRING**. If you need a different data type, like an integer, you need to *coerce* it. 

* *Example:*
```
user_age = input("How old are you? ")
```
*returns* **"29"**
```
user_age = input("How old are you? ")
int(user_age)
```
*returns* **29**

Whew, that was a lot of streamlined information we covered, so I would advise you to take a break and practice utilizing these tools. 

Next week, I'm going to talk about arithmetic, booleans, conditionals, and comparisons.

Also, I wanted to share one more fun fact about Python. I **hate** snakes, I love animals more than people, but snakes are the worst animal on the planet. I know how important they are to ecosystems and all that, but they nasty. 

![](https://media.giphy.com/media/H4wUvhRHnb2TK/giphy.gif)

I haven't wanted to start picking up the language because I have such a strong aversion to snakes. However, much to my relief and joy, Python wasn't named for snakes; it was named for Monty Python.

As a former actor and comedy writer, I love Monty Python as much as I hate snakes. The best part of reading documentation has been the replacement of 'foo' and 'bar' with 'spam' and 'eggs.'

![](https://media.giphy.com/media/3s0QuxoSX6DgdnGFoE/giphy.gif)

Gotta love developers!





