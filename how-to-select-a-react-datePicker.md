---
title: Choosing the Right React Datepicker UI Component
published: true
description: Finding a good datepicker comes with so many options to take into consideration, let's talk about what features to look for in a React datepicker!
tags: React, JavaScript, Grid, Components
---

> Finding a good datepicker for your application should be easy, but there are so many options out there and many things to take into consideration.

Understanding what to look for and what features you can envision needing for your project will be very helpful and a good thing to think about up front when choosing your datepicker.

## Performance

Before making a final decision on a particular datepicker component (or library), you should use the React [Performance Tools](https://reactjs.org/docs/perf.html) to analyze the performance and try to replicate a real use case or scenario similar to how you will use it in production.

The React.js Blog's [Introducing the React Profiler](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html) is a good tool for measuring React component performance in the browser. Just as you would profile components you build and release yourself, when looking for a component to bring into your project you should always be testing them within your own application.

## Package Support

All React component libraries should give you the ability to install through npm or GitHub. It should be simple to find the packages, install them into your project and get to work.

<span style="font-size: 18px;">Must-Have Features in any Datepicker</span>  

The following list of features is largely based on my experience building line of business applications and different scenarios I have required a datepicker.

### A Clean User Experience

We have all seen the date pickers on webpages that use three different native browser dropdowns for month date and year. This is not a clean user experience and there are several reasons why you most likely don't want to do this in your application. The first is that it is much harder to swap the order of dropdowns than it is to simply supply the datepicker with a different date format. Second is that you leave the developer having to put these separate values together after the selection in order to get the full date that we really need to work with.  
![Example of Bad Dropdown UX](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/threedropdowns.gif?sfvrsn=96df7da_1 "Example of Bad Dropdown UX")

Another reason is that it is much harder to ensure that the user actually selects each dropdown correctly and it creates for a less scalable overall solution that does not fare well with users. Dropdowns also provide the worst user experience for users on mobile. My recommendation is to stay away from this method of selecting a date. This is where the almighty datepicker comes into play!

### Input, Calendar or Both

Selecting a datepicker that offers localization provides a better user experience. A lot of datepickers give you the option to have just an input which has a masked date, usually having what looks like placeholder text that indicates the month or day, followed by the year. With this setup, you will usually be able to format the date very easily. This gives us the ability as developers to determine the format as well as set it by locality. In the US, I will want the month first, but in the UK, I will want the day first. The input is great for those who mostly use their keyboards when filling out forms, but this is not every user, others rely on the mouse or finger to select from a calendar. This is why I think your datepicker should feature both of these options and most datepickers I run across on forms do supply both options.  

![Datepicker Example with Input and Calendar](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/inputandcalendar.gif?sfvrsn=55f2ca66_1 "Datepicker Example with Input and Calendar")

### Good UX and Keyboard Control

A datepicker should provide a good user experience, solid keyboard controls, strong mobile functionality, and the ability to work with gestures. Ask yourself if the component you’ve picked can do all of these things or at least the ones necessitated by your application.

Every application is different. When booking flights, we typically need the date range feature, as well, having a button for today's date or the ability to select time is not as important. However, when visiting your dentist's website or choosing a doctor visit or maybe the best time to take your car in to get serviced, these scenarios may need a single datepicker with the option of selecting time. Another tricky situation is a birthday datepicker. In my opinion, the best way to do this is with a three-step process. Select the Month, then day and finally the year of the date you are trying to input. Because different applications throw different scenarios at you, the best datepickers will be ones that provide a variety of different options for the developer out of the box.

## Enterprise Level Support

To put it simply, components that are not licensed rarely have any type of support outside of at-will community help. Most of the big web development shops and enterprise level businesses have tight deadlines and their developers push technology to the edge. It's helpful to have a team to reach out to that has expert knowledge of the components you're working with and paying good money for.

Those are some of the key criteria on which to evaluate a React datepicker for your next application. If there are any features that you think you can't live without, put them in the comments and let us know what your favorite datepicker features are.

## What's the Best Datepicker?

I’ve shared with you my key criteria on which to evaluate a React datepicker for your next application – performance, package support, clean ux, input options, keyboard control and enterprise-level support. If there are any features that you think you can't live without, put them in the comments and let us know what your favorite datepicker features are.

My goal here is not to push you in the direction of a single datepicker, instead, I would rather give you some ideas of what features and qualities to look for and let you decide which one to choose. I have built a couple of datepicker components and I know what type of work goes into even the most simple datepicker components, so I definitely suggest finding one that fits the bill, has all the requirements you need and hopefully someone else does all the hard work to build and maintain it. I loved the challenge of building my own, but this type of component is one that is very tricky and is best to buy off the shelf or find a great open source option.

As far as paid components go, there are many great paid options. At the end of the day, you will do your due diligence and research to pick the datepicker that works best for you. However, if the KendoReact DatePicker is on your list to evaluate, my friend Carl has put together a great piece called ["Unleash the Power of the KendoReact Datepicker Component"](https://www.telerik.com/blogs/powerful-react-datepicker-component-example), that should save you some time during the evaluation process. it is a great resource where to learn how to leverage this Particular React DatePicker’s power and build something amazing.