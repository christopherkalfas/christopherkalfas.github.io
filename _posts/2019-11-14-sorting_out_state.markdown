---
layout: post
title:      "Sorting out State"
date:       2019-11-15 00:53:16 +0000
permalink:  sorting_out_state
---


This next blog update is a tutorial for adding a 'filter-by' or 'sort' button in a React Container.  
 
Let's say you are rendering out a list in no particular order, and you decide to add a feature that allows users to sort and re-render that list by some key-value pair. For this tutorial, our list is an array of mystical creatures. We want users to be able to sort this list by popularity or 'likes.'
  
	
**Create 'Sort' Button** – The first thing you need to do is create a button that triggers the sorting. You want to place this button in your Container Component. This logic needs to go into your Container for several reasons.
1. The first reason is the principle of 'Separation of Concerns.' Separating your app's concerns allows you to delegate specific responsibilities to individual components. Utilizing this concept makes refactoring much more comfortable to implement because depending on what you are changing, your refactoring only happens in one place. A useful metaphor to think about this is an automobile assembly factory. If sports car designers want to add a new factory color to the car, who on the assembly-line needs to know about the change? The factory worker who builds the engine? No. The factory worker who is responsible for making sure the passenger-side door fits? No way! That's not relevant information to them. The only factory worker who needs to know is the one who, you guessed it, paints the car. Automobile factories wouldn't be able to meet their quotas if they pulled everybody into a meeting for every change to the manufacturing process. That's not practical for them, and it's certainly not practical for us as members of a development team.   
2. Secondly, the feature belongs in the container as opposed to other components because container components are primarily concerned with *how things work*. They also are often *stateful*. Back to our example of sorting the list of creatures, this button adds a new way the app functions, and it changes the state of our creatures list. So, we are in the right place to add this button. Huzzah!
3. In this specific example we are going to make the button a 'check-box' that renders at the top of our creatures list. We also want to attach an 'on click' event to trigger the change.

```
<input type='checkbox' onClick={this.handleClick}/>
```



**Define Button State and 'Click' Event**  - Let's work through the logic of how to handle the click. We want the array of creatures sorted-- IF the button is clicked, --ELSE we want the list to render 'as-is.' How can we check whether or not the button has triggered? Since the button triggering changes the state of our data, we should give that button a state to change. Additionally, the change of state happens inside our component; we know this state needs to be initialized with a value and then updated to another value on our 'click' event. Also, we know theres no need for props because props can't change, props are passed down, so if we are changing the state, it needs to happen internally in our component. Since containers are concerned with state, we can also define our state in the same component. So no hunting for another file! Three Cheers for separation of concerns!
1. Let's define our initial state for the button. Since the button needs to be clicked to make the change, we can initialize the state of the button as not being clicked, and we want to render the list' as-is' or the state of the button clicked as false. We set in the initial state in the constructor method because it runs first.
2. The next part of the logic is IF the button is clicked, change the state. So in our click handler, we need to update or manipulate the state of the button being clicked. We are going to use a function that is available to all React Components, 'this.setState().' We want to use this function instead of directly modifying the state because setting state happens asynchronously. Updates to the state are internally batched and then executed when React is ready to do so. If we only modify the state, React won't register the change of the button's state when the code runs. The state would not have enough time to be updated, and the sorted list would never render. We instead use ‘this.setState(),’ This function is designed to let us tell React that the state of our component has changed. Then, the component knows to re-render the list, waiting for the change of state. Next, we need to pass the state change to our setState method. In the case of our example, that means setting the state of being clicked to true. Also, if we just set the state to 'true,' this is a one-time click, and that's not too fun. Instead, we want to set the state equal to the opposite of whatever it is currently set to. So, we pass in an anonymous function with an argument of the previous state. That way, we are toggling the state. Reverse, reverse!

```
constructor(){
        super()
        this.state = {
            hasBeenSorted: false
        }
    }
    handleClick = () => {
        this.setState(previousState => {
            return {
                hasBeenSorted: !previousState.hasBeenSorted
            }
        })
    }
```


**Implement Sort Method in Container** - The last piece of logic we need to incorporate is the conditional sorted list of creatures into our component's render method. There are a few ways to do this, but this example, we are going to take advantage of the ternary operator. The operator takes three elements to work:
1. A condition followed by a question mark
2. The expression we want to execute if the condition is true. This expression is followed by a colon.
3. The expression we want to execute if the condition is false.

For our example, the condition we want to check is the state of the button being clicked. If the conditional is true, we want to execute a sort of the array by 'likes.' If the conditional is false, render the list as is.

```
render(){
        return(
            <div>
            <input type='checkbox' onClick={this.handleClick}/>
            <label>Sort By Likes</label>
            {this.state.hasBeenSorted ? (
                <Creatures creatures={this.props.creatures.slice().sort((a,b) => b.likes - a.likes)}  deleteCreature={this.props.deleteCreature} />
            ) : (
            <Creatures creatures={this.props.creatures}  deleteCreature={this.props.deleteCreature}/>
            )}
            </div>
        )
    }
```

Now that we know how to use the ternary operator let's add a label to our button to make its purpose clear. 

```
<input type='checkbox' onClick={this.handleClick}/>
<label>{this.state.hasBeenSorted ? 'Remove Filter' : 'Sort By Likes'}</label>
```
The label is just a cometic conditional setting of the text of the label to reflect the current condition of state.

**Quick Note!** -  When using the sort method. Sort destructively changes an array. So, if sorted our list's state, we wouldn't be able to 'unsort' our array. That's not super useful as we want users to have the option between sorted and unsorted. Pretty easy fix! We can add the slice method to our sort method. If you're a little rusty on 'slice,' remember that the slice method returns a portion of a copy of an array into a new array. Since we want a copy of the whole portion of the array, we don't worry about passing beginning and ending points; usually utilized by the slice method. The original, or un-sorted array is not modified.

And there you have it! Feeling sorted out? I am!
