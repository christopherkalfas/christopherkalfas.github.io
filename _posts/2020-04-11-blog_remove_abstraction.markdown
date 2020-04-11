---
layout: post
title:      "Blog.remove('abstraction')"
date:       2020-04-11 20:02:34 +0000
permalink:  blog_remove_abstraction
---


This week I thought I'd switch gears away from React applications and talk about object-oriented programming.  Understanding how different models could communicate with one another was my first significant 'road-block' moment. A year later, thinking through Object Relational Mapping is probably my strongest skill. 

![](https://media.giphy.com/media/S9XaGr8wQ9Jwk/giphy.gif)


Trying to grasp abstractions is always something I've struggled with, but I discovered I had to think through real-world/discrete examples to 'flip-the-switch' in my head; to understand them.

So let's say we are designing the back end for a Restaurant POS system.

**We have three models:**
* Customers
* Restaurants
* Waiters  

The way I would connect these models would be a `has_many :through association`. 

* A Customer has_many Restaurants
* A Customer has_many Waiters: through Restaurants
* A Waiter has_many Customers: through Restaurants

![](https://media.giphy.com/media/s239QJIh56sRW/giphy.gif)

When models need to associate, at least one model needs to store the relationship mentioned above, the child model stores the link to its parent.

If that is too abstract for you, then you are like me. A great discrete way of thinking about storing a relationship is to think of a dog and its owner. 

Human logic says, I know that my dog belongs to me. I know my address and my dog doesn't, so I would hold the link to my dog. You would be wrong. When an owner loses a pet, that owner knowing their address and their dog's name doesn't help find them. However, if the dog has a collar, a stranger can see  that this is * your dog*,  and get your phone number or address. Then the stranger brings the dog back to it's owner. So in computer logic, the dog stores the relationship information about the owner. 

![](https://media.giphy.com/media/LdPoviVCWgLf2/giphy.gif)

Now back to our restaurant example. Let's use the same discrete reasoning to help decide how to relate the restaurant models. Customers and Waiters don't own each other, and I would hope a waiter doesn't have my home address or phone number. Well, let's break down what information you would and wouldn't give while having dinner at a restaurant.

**A waiter needs to know:**
* A customer's name - When waiters are totaling their tips, they need to know which receipt belongs to the customer in the system. 
* The amount of the check - For the same reason as above, they are adding the tip; the customer wrote down and making sure the total, including the tip, is equal to the receipt the customer signed.

**A waiter doesn't need to know:**
* My credit card number, because, well duh.

**A customer needs to know:**
* The total bill amount with tip- Maybe the meal was a work dinner, and the customer has to turn it in with the expense report. Or they are keeping up with a budget.
* The date the meal occurred- for the same reasons as above
* The waiter's name - So they know how to address the waiter during dinner.

**A customer doesn't need to know:**
* ANYTHING ELSE
* 
**A restaurant (or the POS computer) needs to know:**
* Every customer's name, check total,  and credit card number. 
* The waiter's name, the waiter's bank account number(where to send the tip) and both party's contact information.

Hopefully, the light is starting to turn on, but in essence, as programmers, we need to think about our models as real objects and what those objects need to function in the real world. You have to think through your actual experiences with restaurants and waiters, or appointments and doctors, and let what pieces of information you utilize in the real world motivate how the different computer models associate together. 

In the Case of the Customer-Restaurant-Waiter...
The *restaurant* holds the ID's for both Customers and Waiters.

![](https://media.giphy.com/media/uhYKP2f4xRz7q/giphy.gif)

Object-Relational-Mapping doesn't sound quite as scary when you realize the abstract answers you seek are hidden in your life-real discrete experiences.  

