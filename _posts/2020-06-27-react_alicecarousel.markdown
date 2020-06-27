---
layout: post
title:      "React + AliceCarousel"
date:       2020-06-27 21:42:57 +0000
permalink:  react_alicecarousel
---


![](https://media.giphy.com/media/IONcI446NLLTq/giphy.gif)

Hi, everyone!

Feel free to skip my motivation section, scroll down to the IMPLEMENTATION section.

#### MOTIVATION 
I recently finished building my portfolio website with React. While I have a lot of experience in sales, something I don't enjoy selling is myself. But alas, a portfolio website is pretty essential for a budding developer, so away I build. I looked at other developers' websites to draw inspiration, but I felt that a lot of them looked the same, and while many of them were beautifully designed, I felt like I didn't get a sense of who these people 'actually' are. I think it's essential for potential employers to get a sense of what you are like in your life outside of work. At the end of the day, you can be the best developer for a job, but if people don't like you, they're not going to hire you. 

![](https://media.giphy.com/media/UildSjm0vLJZe/giphy.gif)

So I decided I would build a slideshow to give a brief overview of my life so far. I included pictures of my friends and family, as while as from my previous jobs and theatrical performances. I figured it tells a story without making people have to read a long blog post, you know... like this. 

I digress, I wanted to share how I implement a React Package called 
"Alice Carousel." There are a ton of options, and if you aren't using Bootstrap in your app, I suggest you give this one a shot.

Let's dive in, shall we?


#### IMPLEMENTATION

In your React application, install [AliceCarousel](https://github.com/maxmarinich/react-alice-carousel).

`yarn add react-alice-carousel`

Inside your project source folder create a new component, for the sake of this blog we'll call it,

`Gallery.js`

Inside `Gallery.js` import React as well AliceCarousel and its corresponding CSS file. 
Also, if you are using your own images, create an `img` folder inside your source folder to keep them in.  

```
import React from 'react'
import AliceCarousel from 'react-alice-carousel'
import 'react-alice-carousel/lib/alice-carousel.css'
```

As far as importing the images, you can handle it two ways.

* Import the image at the top of the component file. 

* `import picture1 from '../img/picture1.png'`
 
*  Then you can pass the image as a prop to an image tag.
 
*  `<img src={picture1} .../>`

OR

* Import them inside the `img` tag.
 
* `<img src={require("../img/picture1.png")} .../>`

Great! Now lets layout the rest of the component.

Our Gallery component will define a variable called `handleOnDragStart`, assigned to an anonymous function that prevents the default action on the event.

`const handleOnDragStart = (e) => e.preventDefault()`

One of the cool aspects of the AliceCarsoul Package is that there are a ton of default methods you can use to customize your slideshow. Here is an example of the methods I used in my portfolio. 

```
  <AliceCarousel 
        autoHeight={false}
        autoPlayInterval={3000}
        autoPlayDirection="rtl"
        autoPlay={true}
        fadeOutAnimation={true}
        mouseTrackingEnabled={true}
        buttonsDisabled={true}
        disableAutoPlayOnAction={true}
    >
```

Great job. The last step is to add our images and add our `handleOnDragStart` to the image tags. 
```
<img src={require("../img/picture1.png")} onDragStart={handleOnDragStart} className="picture" alt="pic1"/>
```

That's all there is to it! Here is what the entire component should look like.

```
import React from 'react'
import AliceCarousel from 'react-alice-carousel'
import 'react-alice-carousel/lib/alice-carousel.css'

const Gallery = () => {
  const handleOnDragStart = (e) => e.preventDefault()
  return (
    <AliceCarousel 
        autoHeight={false}
        autoPlayInterval={3000}
        autoPlayDirection="rtl"
        autoPlay={true}
        fadeOutAnimation={true}
        mouseTrackingEnabled={true}
        buttonsDisabled={true}
        disableAutoPlayOnAction={true}
    >
	  <img src={require("../img/picture1.png")} onDragStart={handleOnDragStart} className="picture" alt="pic1"/>
      <img src={require("../img/picture2.png")} onDragStart={handleOnDragStart} className="picture" alt="pic2"/>

   </AliceCarousel>
  )
}
export default Gallery
```


Well done! AliceCarousel is an excellent package for React. I would also encourage you to try using it with an API for a little extra fun! If you want to check out my slide show, here is the link. 

[Website Slideshow](https://chriskalfas.com/about)

Thanks, everyone! See you next week!

![](https://media.giphy.com/media/4Ej4ELEyt0Uta/giphy.gif)



