---
layout: post
title:      "Where We're Going We Don't Need to Calculate Time "
date:       2020-03-27 17:54:25 +0000
permalink:  where_were_going_we_dont_need_to_calculate_time
---



I recently spoke to my cousin, she is a software developer consultant at one of the country's preeminent firms, and she told me about a code challenge she encountered during the interview process. The code challenge involved building a calendar, similar to the iOS calendar, in seven hours.  I thought to myself I have no idea how to do that! So as I started to build a calendar application and quickly realized a problem I'm sure many React Developers have faced. When making fetch-requests, the strings and date structure are confusing and hard to format.

In Javascript, developers can use  the `new Date()` method, `.toLocaleString()`, `.setInterval()`, and state manipulation in a myriad of different combinations. It's enough to make your head spin.

![](https://media.giphy.com/media/26uf6Rkcj5rE8H5Hq/giphy.gif)

Or developers can use a JS package called [Moment.js.](https://www.npmjs.com/package/react-moment)

Moment.js allows users to access dates and times without the headache mentioned above. There is almost an endless amount of formatting options, including a time-zone feature.  Additionally, the documentation is excellent and relatively easy to use. 

![](https://media.giphy.com/media/i5x5BcIqmlod2/giphy.gif)

Let's dive in and implement the package in a simple React application, shall we?


#### INSTALL 

In the terminal run, `yarn add moment` or `yarn add moment-react`. If you are importing from `moment-react`,  you can use the Moment package as a child node and can utilize it like traditional components.

#### IMPLEMENTATION 

You can also import Moment.js in your component's state by setting the value of a `dateObject` to `moment()`.


`
state={
dateObject.moment()
}
`

Now that we have imported the package, let's talk about formatting. Moment.js has built-in input methods that can format the date and time as we see fit. For example, if we wanted to return the names of days in the week, set a variable to the moment object and call the `weekdaysShort()` method. 

`weekdayshort = moment.weekdaysShort()
`

How easy is that?! 

![](https://media.giphy.com/media/xTiIzoyw4Yh3mRM5DG/giphy.gif)

Now you can pass your variable into your components return method.

```
render(){
        let weekdayshortname = this.weekdayshort.map(day => {
            return(
                <th key={day} className="weekday">
                    {day}
                </th>
            )
        })
	return(
	      <div className="container">
		       {weekdaysshortname}
	     </div>
   )
}
```


Check out the table of different formats available through Moment.js. [Moment.js Formatting](https://momentjs.com/docs/#/displaying/format/) For the calendar, we need the day of the month(ie. 1st, 2nd, etc..), which we can access with `.format('D')`. Also, we need to know what day of the week, is the first of the month, so the correct day of the week and date align for each month. We can use Moment.js to return this data by calling on the `.startOf()` method and `.format()` methods. 


```
firstDayOfMonth = () => {
        let dateObject = this.state.dateObject
        let firstDay = moment(dateObject).startOf('month').format('d')
        return firstDay
}
```


Those examples are a small percentage of what is available to you using Moment.js. Still, hopefully, the ease of implantation this package encourages you to build a calendar or clock worthy of the coding-gods! And if appeasing the coding -gods isn't your thing, then at least you can move on to other aspects of your application without getting bogged down. 

![](https://media.giphy.com/media/Btv7SwSH15KGk/giphy.gif)

