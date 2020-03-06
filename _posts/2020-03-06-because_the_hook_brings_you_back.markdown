---
layout: post
title:      "Because the Hook Brings You Back"
date:       2020-03-06 21:47:55 +0000
permalink:  because_the_hook_brings_you_back
---


When I was going through school and learning about React, we didn't cover hooks. During my first phone interview, the interviewer asked me about hooks. So, here we are, learning about hooks. I wanted to start working on a new language, but just as Blues Traveler once said, "because the hook brings you back. I ain't telling you no lie." I would have never guessed that song was actually about going back and learning new React concepts. That makes the song so much more profound. 

![](https://media.giphy.com/media/l2QE50jSRSuRYUYWA/giphy.gif)

Let's dive in, shall we?


**WHAT IS A HOOK?**

React Hooks allow functional components to have a state and utilize life cycle methods.

![](https://media.giphy.com/media/Poaj36am3ZqaA/giphy.gif)


**WHAT DOES THAT MEAN?**

I'll tell you, Dany! Before Hooks were introduced during the React 16.7 update, if a component needed to be *stateful*, it was written as a *class component*. The issue with using them as a class is that classes don't have support to a store like Redux/Thunk, which means that you have to use a higher-order components pattern. High-Order Components(HOCs) allow you to reuse the logic of a component. They are functions that take a component and returns a new component.  Building out your components using these HOCs requires you to restructure your components when you want to utilize them. This pattern can make components hard to read.

![](https://media.giphy.com/media/uN5iwZB2v2dH2/giphy.gif)

The other issue is that a foundational aspect of React is the separation of concerns, but using the HOC's makes some of the logic in your component unrelated to your function's original purpose.


**WHAT DO HOOKS DO?**

Hooks allow you to use stateful logic repeatedly without switching the structure of the component tree. The simplicity of hooks makes sharing stateful logic easy. Also, because we aren't using traditional lifecycle methods like 'componentDidMount' and 'componentWillUnmount,' there is less unused logic and decreases the likelihood of bugs.

In essence, Hooks let you split a component into 'chunks' or a collection of smaller functions that are related to other pieces. The most prevalent time you'll want to use hooks is when you need to fetch data. The other useful time you can use hooks is when you want to add state to a functional component. Now you don't need to refactor the entire component to add state.


**WHAT DO HOOKS LOOK LIKE?**

Here is a basic component that we will refactor to use hooks.


```
class NoHook extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

Great! Now, let's look at refactoring using hooks.

```
import React, { useState } from 'react';

function Hook() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You've clicked the button {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

So we can see a few new pieces at work
1.  useState- is imported from React
2.  useState is being deconstructed into two arguments. The first argument *count* is the name of our state. The second is the method name we are going to set the state. 
3. useState(0)- We are passing the useState method the value of our initial state. In this case, zero.  
4.  In the render method, we are using just the *count* property, because of the deconstruction.
5.  On the button, we have already defined both count and setCount as our variables, so there is no need for *this*. 

Now that we have a little more context about hooks, I want to leave you with another mind-blowing connection to the Blues Traveler hit. 

"Because the hook brings you back" 

Hooks bring/fetch state changes to your backend.  Because the hook brings you back, get it? 

![](https://media.giphy.com/media/BkVqfREIvC012/giphy.gif)

Maybe that's a stretch.
