---
layout: post
title:      "No Hands Modals in React.js with react-modal"
date:       2020-07-10 14:31:37 +0000
permalink:  no_hands_modals_in_react_js_with_react-modal
---


Hi everyone! This week I wanted to try and remedy a problem I regularly encounter when trying to add a package to a React project. Most of the time, multiple packages do very similar things. The 'deciding-factor' for me is looking at which package has the most downloads. In their README's the creators talk about how easy their package is to work with; I beg to differ.

![](https://media.giphy.com/media/VcWnY3R6YWVtC/giphy.gif)


I don't know about all of you, but in my experience, the creator uses a single example, and I need two or three examples to get my head around it.


So this week, I wanted to add a modal for my web-based React trivia game called TrivKalf. I know, I'm great at names. I haven't used Bootstrap for this app, and I didn't want to use it just for a modal. So I searched for the most popular React package not involving Bootstrap and found [`react-modal`](https://www.npmjs.com/package/react-modal).



##### Quick Side Note - What's a modal?

A modal is a graphical control element that overlays (and is subordinate to) the application's main UI design. 

##### What does that mean? 

 It means this thing...


![](https://i2.wp.com/www.cssscript.com/wp-content/uploads/2018/09/Minimal-Flexible-Modal-Window-Library-Modal.js.png?fit=488%2C360&ssl=1)


See, you knew what that was.

![](https://media.giphy.com/media/3o6fIWXqyD2lnGNrpe/giphy.gif)

Alright, back to `react-modal`! The example the creator gives lays out a basic modal that uses a button to open and close it. 

```
return (
<div>
        <button onClick={openModal}>Open Modal</button>
        <Modal
          isOpen={modalIsOpen}
          onAfterOpen={afterOpenModal}
          onRequestClose={closeModal}
          style={customStyles}
          contentLabel="Example Modal"
        >
 
          <h2 ref={_subtitle => (subtitle = _subtitle)}>Hello</h2>
          <button onClick={closeModal}>close</button>
          <div>I am a modal</div>
          <form>
            <input />
            <button>tab navigation</button>
            <button>stays</button>
            <button>inside</button>
            <button>the modal</button>
          </form>
        </Modal>
      </div>
    );
```

 I designed my game to handle fetching the next question from the API as a click event on the answer option a user selects. Before the next question renders, I use `setTimeout` method for a few seconds to render the right and wrong answer. I want my modal to open and close based on those events and not independent buttons. So the example doesn't really apply to what I was trying to accomplish. As I looked for more general use examples, I saw the package gives me a prop option of `closeTimeoutMS`. That's what I need!
 
 
But hold up, the documentation also states the `isOpen` prop is required, and as I mentioned, it needs an `onClick` event. I thought about connecting the `onClick` event to every answer option. Still, I had an issue with separating concerns. It was going to be messy to pull apart my existing logical to conditional render two different modals for "correct" and "incorrect," and refactoring multiple components.  Another option was to added `isOpen` state to my component. But for the same reason as above, the juice didn't seem worth the squeeze.  


I ended up using an already present state value of `isCorrect` (which returns a boolean to update the correct or incorrect score). When a question renders the value of `isCorrect` is `null`. Once the user input's their answer, the value is `isCorrect` is assigned a boolean. For the modal's required `isOpen` props, I attached it to the value of `isCorrect !== null`. So now the `isOpen` prop gets fired when ANY value is assigned. Pretty slick, right?

![](https://media.giphy.com/media/3o85xzhXeG6bY1ZPZ6/giphy.gif)

As for having two different modal styles, I used the `className` prop and attached it to a ternary operator that checks the value of `isCorrect`.

```
className={`results ${isCorrect ? "correct-color" : "incorrect-color"}`}
```

Cool, right? And those aren't complicated solutions, but it took me longer than I believe it should have to figure that out. Programmers with more experience than I probably could have figured that out much faster. However, developers with less experience than I will have a hard time getting that experience without having several examples of how to use something.  I think package creators should take a little more time and give a few different patterns with varying degrees of difficulty. That way, programmers can figure out how to implement the package faster, which is kind of the whole point of packages. 

Here's the props layout for the final version of my modal. 


```
return(
        <Modal
            isOpen={isCorrect !== null}
            closeTimeoutMS={4000}
            className={`results ${isCorrect ? "correct-color" : "incorrect-color"}`}
            overlayClassName="Overlay"
        >
            <div className="results-container" >
                <div className="content">
                    { isCorrect && (<h1>Impressive!</h1>)}
                    { !isCorrect && (<h1>Shame!</h1>)}
                </div>
                { !isCorrect && (
                    <div className="correct-answer">
                        <h4>The answer was: </h4>
                        <h1 className="answer-name" dangerouslySetInnerHTML={{__html: question.correct_answer}} />
                    </div>
                )}
            </div>
        </Modal>
    )
```

Also, here is the link to my game where you can check it out for your self.

[TrivKalf](https://trivkalf.firebaseapp.com/play-category)

Thanks, everyone! Until next week! 
