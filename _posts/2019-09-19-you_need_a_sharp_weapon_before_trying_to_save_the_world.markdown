---
layout: post
title:      "You Need a Sharp Weapon Before Trying to Save the World"
date:       2019-09-19 17:35:26 -0400
permalink:  you_need_a_sharp_weapon_before_trying_to_save_the_world
---


Hello again, time for the 3rd installment of my blog. This time I’m offering up a look into how I am trying to bridge my new programming skills with my personal experiences. Coming from the world of sales and acting, I am accustomed to actively pursuing my goals, whether that means fame or financial stability. Another part of my personal experience is my underlying urge to leave the world better than when I came in. I don’t think I’m alone in that regard.

As an actor, making the world a better place meant offering audiences Escapism. The goal was to make audiences forget their financial, emotional, and interpersonal problems for a few hours. Audiences could forget their issues and watch fictional characters work through theirs instead. However, that wasn’t why I chose acting. I was an actor because of the lights, the music, and of course, the applause.

The Escapism was a justification.

Working in sales was a similar story. If I was helping folks as much as I could, my ‘profit margins’ (what percentage of a deal the salesperson makes), would make saving up for a house or retirement impossible. I would tell myself that I was protecting the customer from other salespeople who would take advantage of them. Well, relative to what I was doing.

So now that I am a programmer, making the world a better place seems more accessible for MY life.
I don’t want anyone to interpret my opinion as unfavorable towards sales or acting. For some people, they will have better answers than me to that question. I can only speak for myself and my happiness. I proudly wouldn’t trade my BFA or sales experience for a C.S. degree.

With all that said, I want to share more about my latest venture. Since becoming a programmer, I have been drawn with solving real-world problems with code. My childhood best friend organized a little fitness competition among our friend group. The game was straight forward. There is a weekly goal of ‘reps’ (sorry, bro) for a particular exercise. Maybe it’s 300 push-ups in a week or 500 sit-ups. At the end of the week, the person who was furthest from that goal donates twenty dollars to a charity of the winner’s choice (the person who did the most reps). Right now, the competition is tracked in Google SpreadSheet and operates off the “Honor System.”

SO as soon as I wrapped my head around Rails, I knew what I wanted to build. I was eager for the satisfaction of making the world a healthier and more charitable place! I was a little too enthusiastically thought, as I discovered building the was much harder than I anticipated. The issue I ran into was the complexity of mapping the object relations. Initially, I thought I could make the app using three models:

1. Users  2. Challenge Masters  3. Activities.

A User has many Challenge Masters, and a User has many Activities they’ve completed through Challenge Masters. Activities has many Challenge Masters and Activities has many Users through Challenge Masters. A Challenge Master belongs to one User and one Activity. I thought that was solid and dove right in. I started running into issues immediately. I hadn’t even thought about Charities. Can’t make the world a better place without those! But where do I store that relationship?
Refactor!
However, that wasn’t the end of my problems; I still hadn’t accounted for a way for a Challenge Master to assemble a group of specific users. Maybe it’s a group that all likes the same charity. Perhaps you want only people you invite to be able to compete. If any user could join any competition, you run the risk of Michael Phelps or Usain Bolt joining your group, and you could go bankrupt. Also, I hadn’t considered how Users track and post their progress. That’s the ‘hook’ of the game! Okay, let’s refactor again!

Actually, we won’t, but I think I’ve made my point. I was so eager to start building that my blue-point never had a chance to guide me to the ‘right’ way to make this. I was adding and dropping classes and relationships like an indecisive fantasy football owner. The quintessential lesson in building “Sweat Clause” is a lesson I thought I learned from my sales-mentor years ago. He used to quote Abraham Lincoln almost every week during sales training.
“Give me six hours to chop down a tree, and I will spend the first four sharpening the ax.”
Whether or not the ‘Vampire Hunter’ actually said those exact words a discussion for another day.

The quote serves as a reminder that the key to being productive is preparation. If I had taken about 3 hours and 55 minutes longer to start building, I would have saved DAYS building out my app. Since then, I started a habit of keeping a whiteboard or notebook with my computer. I don’t open my laptop until the mapping making sense, and I’ve essentially pseudo-coded the entire thing. My blueprints aren’t in my head anymore; they are in front of me at all times while I build. And, while this is probably extremely obvious to more seasoned programmers, I have been amazed at how much more efficient I’ve become. I learned, if I want to try and solve the world’s problems, I’d better have a good plan and not just good intentions.
