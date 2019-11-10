---
layout: post
title:      "Connecting the Props"
date:       2019-11-10 20:52:28 +0000
permalink:  connecting_the_props
---


I have been learning React with Redux for the past few weeks, and I've got to say its pretty rad. It's powerful, fast, and lets you pull together a dynamic web app in the blink of an eye. It also confuses the hell out of me. 

For my final project blog, I'd figure I'd try to clear up up something that it is foggy to me. Maybe it's murky to you as well, and I hope this helps you, but more importantly, ME. 

Abstraction has been the most significant challenge of becoming a software developer. I struggled to understand how objects-related to each other, or how JavaScript, a 'synchronous' programming language, is optimal when used 'asynchronously.'   

Naturally, The hardest part of React and Redux is getting literal. I found a lot of the terminology to be difficult to grasps because they do precisely what their names say they do, and I don't know how to handle it.


![](https://media.giphy.com/media/9sVP2K0yYM6J2/giphy.gif)

For example;

**Props**- are properties. They are passed down from a parent Component to their children. Attributes passed down or inherited from* your* parent to you are not *changeable*. Even if you dye your hair blue and leave the choir for a punk-rock band, your flowing locks and sense of rhythm still came from your props; I mean pops'. Primarily, props help you write reusable code. They are similar to parameters in functions.

![](http://giphygifs.s3.amazonaws.com/media/gu8IhIriagKUo/giphy.gif)

**State**- is used to track information or values that can change. My state of mind is a property or an attribute of being a human. I can't exist with some state of mind; what that state of mind* is *can change. In the mornings, my state of mind is 'sleepy'(previous state), I drink coffee(action), and I set or 'reduce' my state of mind to 'wired'(new state). I dispatch this change by posting a picture of me to Instagram, drinking said coffee with the hashtag '#caffeinated.' Now anyone looking at my post can see my new state of mind and my self-absorption. 

![](https://media.giphy.com/media/3RID97HU3TxEk/giphy.gif)

Props and states are also relevant when you need to connect React and Redux.  The connection consists of two functions:

1. **mapStateToProps**
2. **mapDispatchToProps**


The **mapStateToProps** function's purpose is to return or access a certain aspect or all of your data from your store; viewed as Props in your React Container.

```
const mapStateToProps = (state) => {
    return { items: state.items }
}
```

As you can see, the function *separates the concerns* and helps keep your components *stateless*, and thus, *reusable*. So any time the store is updated, **mapStateToProps** is called. What you get back is a plain or vanilla JavaScript Object, which merges as the component's props.
Think of this as 'reading' a list of items. 


A lot of the time, we do not need to just 'read' or get our data. Sometimes we want to 'write' or set our data. That data needs to persist in our Redux store.  The second function needed for our connection is **mapDispatchToProps**.

Just as literal as everything else I've written in this blog, **mapDispatchToProps**,  *dispatches*, or tells the data where it is being sent to create a Redux action.  This created action is available to the React Component as a prop. Inside of the React component, an event listener, such as a 'click,' carries-out a 'change' or *action*. Think of this as adding to a list of items.

```
const mapDispatchToProps = dispatch => {
    return {
        addItem: () => {
            dispatch(addItem())
        }
    }
}
```

The last step is the 'change' needs to connect to the store. 

This connection allows the component to access the current state from the store and dispatch actions to the store with a change of state.


```
export default connect(mapStateToProps, mapDispatchToProps)(Component)
```


So there you go, a profound explanation of something you could understand by reading the names. Clear as mud?

![](https://media.giphy.com/media/tU6XeiHpmBNXq/giphy.gif)

