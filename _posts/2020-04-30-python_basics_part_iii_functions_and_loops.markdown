---
layout: post
title:      "Python Basics Part III: Functions and Loops"
date:       2020-04-30 19:12:25 +0000
permalink:  python_basics_part_iii_functions_and_loops
---


![](https://media.giphy.com/media/poC8TZpAocrKg/giphy.gif)

Thanks, Matthew. This week I am going to conclude my Python Basics series by covering functions and loops. Once again, I'm going to help explain how these concepts work by comparing them against my existing technical knowledge of Ruby and JavaScript.

Here are the links to Part I & II:

* Python Basics:[ Part I](https://christopherkalfas.github.io/python_basics_whyd_it_have_to_be_snakes)

* Python Basics:[ Part II](https://christopherkalfas.github.io/python_basic_part_ii_snake_logic)


## **FUNCTIONS**
As we know, functions are a 'block' of code that does a specific task and allows programmers to reuse useful pieces of logic. 

### Function Construction
![](https://media.giphy.com/media/123SJ2jmu2XSUg/giphy.gif)

A function in Python starts with the keyword `def`. The `def` keyword also shows up in Ruby. However, that is where the similarity ends. Once you use the `def` keyword and define the name of your function, which should be lower and *snake_cased*, we use a colon `:` . The block we want to attach to our function ***MUST be indented***. In Ruby and JavaScript, indentation is more of 'recommendation' to make the code easier to parse, but is Python the indentation is a requirement for functionality.

Passing in arguments to your function looks similar to Ruby and JavaScript, but just like before, the indentation is requirement as opposed to recommended. **ALSO**, *parentheses are **required** in Python*.

In Ruby, we need to declare when our method finishes. We do that using the `end` keyword. In JavaScript, the function's block is contained in 'curly' brackets- `{}` . Python doesn't use either one of those. The end of a Python method is defined by the *last line of code that is **indented** under the function name*. You can see why indentation is so important.


**Python:**

```
def greeting(name):
    print("Hello, {}!".format(name)     #  <---- inside block

greeting(name)         #  <----------------- outside block
```

**Ruby:**

```
def greeting(name)
	puts "Hello, #{name}!"
end 

greeting(name)
```

**JavaScript:** 

```
function greeting(name) {
	console.log("Hello, ${name}!")
}

greeting(name)
```

#### **Note on 'Return**'
The return keyword is utilized in a similar way to Ruby and Javascript. Python needs the return value to define inside the block to give us the result of our function. If we don't set the return value, Python's interpreter hands back the keyword, `None`.  None is technically a Python Object representing nothingness.



## **LOOPS**
![](https://media.giphy.com/media/RI4LTRjrVJhTskGtrb/giphy.gif)

#### **While Loops**
Hopefully, by now, you're starting to see the patterns a little more clearly. 'While' loops are very straight forward and will look very similar to Ruby and JavaScript.

**Python:**

```
count = 0

while (count < 3):
     count + 1
	   print("Hello World!")
```

**Ruby:**

```
count = 0 

while count < 3
	count += 1
	puts "Hello, World"
end
```

**JavaScript:** 

```
let count = 0

while (count < 3) {
	console.log("Hello, World!")
	count ++
}
```

#### **For Loops**
There are a few different aspects to discuss with For Loops. First, in Python, it is sometimes called a *for IN loop*. The construction is noticeably similar to Ruby and just a little different from JavaScript.

**Python:**

```
humble_brag = ["Chris", "is", "good", "at", "explaning", "Python"]

for i in humble_brag:
    print(i)
```

**Ruby:** 

```
humble_brag = ["Chris", "is", "good", "at", "explaning", "Python"]

for i in humble_brag do
    puts i
end
```

**JavaScript:**

```
let humbleBrag = ["Chris", "is", "good", "at", "explaning", "Python"]

for (i in humbleBrag) {
    console.log(i)
}
```

Congratulations!  Over the last three blogs, we covered a lot of material, and I hope that all of the comparisons to Ruby and JavaScript helped expedite your learning curve through the basics. When I was newer to coding, I was intimidated by the prospect of constantly learning multiple languages. I was worried that learning Ruby meant that it was the only backend language I can use, and I have to learn something completely different to make my self more marketable. Now, I see that learning a new language like Python is substantially easier because I know Ruby.  I hope you feel the same. I wish you well as you venture on your own into the depths of Python, but as you descend, I hope you are bringing some confidence and, of course, a silly walk with you. 

![](https://media.giphy.com/media/Irdr4KvHw0shi/giphy.gif)
