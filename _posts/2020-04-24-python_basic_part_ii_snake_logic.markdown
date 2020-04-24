---
layout: post
title:      "Python Basic Part II: Snake Logic"
date:       2020-04-24 13:04:33 -0400
permalink:  python_basic_part_ii_snake_logic
---


Hello, to my loyal followers. As promised, here is the follow up to last week's blog on Python Basics. In this entry, I'm going to cover arithmetic, string methods, comparisons, booleans, and conditionals. 

![](https://media.giphy.com/media/3s976LBmflJ17QqV7M/giphy.gif)

#### ARITHMETIC
Python's round method takes the decimal and rounds down or up to the nearest whole number.
* Example: `round(2.4)` returns `2`
* Example:  `round(2.6)` returns `3`

Python follows standard Order of Operation - PEMDAS. For those who don't remember what means:

* "Please, excuse my dear aunt Sally."
* Parenthesis - Exponents -Multiplication - Add - Subtract

**Integers & Floats** - Python allows data type coercion using the integer, float, and string methods

* Example: `int("7")` returns `7`

* Example: `int(7.8)` returns `7` ;  **NOTE** using the integer methods on a float will *ALWAYS* round **down.**

* Example: `float(7)` returns `7.0`

* Example: `str(42)` returns `"The Meaning of Life"`; actually, it doesn't, but that would be cool. this method actually returns `"42"`.

#### BASIC METHODS
**Length** - Python's length method can be used on strings to count the number of characters
* Example: `len("Chris")` returns `5`

**Upper & Lower Case Coercion** - The upper and lower methods coerce a string's value to all upper or lower case, respectively.

* Example: `"Chris".upper()` returns `"CHRIS"`

* Example: `"Chris".lower()` returns `"chris"`

**Title** - Python's title method is my favorite method so far because it doesn't exist in the languages I know. I am used to splicing and slicing arrays at the first index and calling the upper or lower case methods and building a new array. Now that I have seen the title method, I'm almost wholly 'sold' on why this is such a popular language.
* Example: 
```
"the lord of the rings: the fellowship of the ring".title()
``` 
* returns 
```
"The Lord Of The Rings: The Fellowship Of The Ring"
```

HOW FREAKING COOL?!

![](https://media.giphy.com/media/7WYXwywbv7fig/giphy.gif)

**List of all methods** - Python's help methods return a list of available methods for the data type you pass to it.
* Example: `help(str)` 

#### COMPARISONS

Python's comparison logic is similar to Ruby's and JS's.
* A single equals sign "=," assigns a value to a variable

Example: `name = "Chris"`

* A double equals sign "==," compares the equality between two objects.

Example: `"Chris" == "Bob"` returns `False`

* The Bang operator functions the same

Example: `"Chris" != "Bob"` returns `True`

* The greater-than and less-than logic is also the same.

Example: `4 > 10` returns `False`

Example: `4 >= 4` returns `True`

* String comparison uses alphabetical order, so "b" comes after "a" and therefore is 'greater' than "a."

Example: `"banana" > "apple"` returns `True`

![](https://media.giphy.com/media/icJA0VF7ntoEL18Jez/giphy.gif)

#### BOOLEANS

Python's conditional logic is the same as in JavaScript and Ruby. The syntax for chaining logical is a little different. 
* Ruby Example: `true && true` returns `true`

* Ruby Example: `true || false` returns `true`

* Python Example: `True and True` returns `True`

* Python Example: `True or False` returns `True`

Python's syntax reads more like English than Ruby's! 

#### CONDITIONALS

**If, Else, and Elif** - One of the most significant differences between Ruby and Python is that when we write a conditional statement in Python, the **indentation MATTERS**. 

The 'if' statement is followed by the expression we are evaluating, followed by a **colon**. The block of code we want to run if the condition is met, must be indented or tabbed. If we don't do that, then that block is not attached to the evaluated expression.

The 'else' statement is similar to Ruby and JS as well. If the 'if' statement expression is not met, run the 'else' statement block.

In Python, the keyword 'elif' is a replacement for Ruby's 'elsif' and JS's 'else if.'

Example:
```
if name == "Chris":
    print("Hi, {}! Awesome name!".format(name))
elif name == "Bob":
    print("Howdy, {}! Your name is almost as cool as the name, Chris.".format(name))
else:
    print("Hello, {}. Have you thought about changing your name to Chris?".format(name))
```

![](https://media.giphy.com/media/tZ6zAdNZbWOhq/giphy.gif)

And there you have it! I hope that these blogs are helping turn on some lights and showing you how easy it is to pick up a new language once you have others under your belt. Take another break and get comfortable with these concepts. I think it becomes exponentially more comfortable to learn new things once you have something to compare it to. Next week I'm going to wrap up my Python basics series by covering functions and loops.
