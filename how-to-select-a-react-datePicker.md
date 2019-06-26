---
title: Choosing the Right React Date Picker
published: true
description: Finding a Date Picker for your apps is a requirement for most enterprise level applications. In this article I'll give you some insight into what features I look for.
tags: React, JavaScript, Grid, Components
---

Finding a good date picker for your application should be easy, but there are so many options out there and many things to take into consideration. There are free date pickers from open source libraries and paid date pickers that come with a license and support. Understanding what to look for and what features you can envision needing for your project will be very helpfulk and a good thing to think about up front when choosing your date picker.

## Performance
Before making a final decisions on a particular date picker component (or library), you should use the React Performance Tools to analyze the performance and try to replicate a real use case or scenario similar to how you will use it in production.

The React.js Blog's Introducing the React Profiler is a good tool for measuring React component performance in the browser. Just as you would profile components you build and release yourself, when looking for a component to bring into your project you should always be testing them within your own application. Check how they perform under the situations you envision them working in?

## Package Support
All React component libraries should give you the ability to install through npm or GitHub. Below is an example of importing and using a React Grid component into your project.

*PKG SUPPORT (DATEPICKER) IMAGE GOES HERE*

Must-Have Features in any Date Picker
The following list of features is largely based on my experience building line of business applications and different scenarios I have required a date picker.

## Dropdowns are Gross

Show me a date picker with three dropdowns for month date and year and I will show you a bad user experience. There are several reasons why you don't want to do this. The first is that it is much harder to swap the order of dropdowns than it is to simply supply the date picker with a different date format. Second is that you leave the developer having to put these sepereate values together after the selection in order to get the full date that we really need to work with. Another reason is that it is much harder to ensure that the user actually selects each dropdown correctly and it creates for a less scalable overall solution that does not fare well with users. Dropdowns also provide the worst user experience for users on mobile. My reccomendation is to stay away from this method of selecting a date. This is where the almighty date picker comes into play!

## Input, Calendar or Both?

A lot of date pickers give you the option to have just an input which has a masked date, usually month or day followed by year and an easy way to format that date. This gives us the ability as developers to determine the format as well as set it by locality. In the US, I will want the month first, but in the UK, I will want the day first. The input is great for those who mostly use their keyboards when filling out forms, but this is not every user, others rely on the mouse or finger to select from a calendar. This is why I think your date picker should feature both of these options and most date pickers I run across on forms do supply both options.

*INPUT AND CALENDAR ANIMATION IMAGE GOES HERE*

## Good UX and Keyboard Control

My concern is that if you are paying for a DatePicker off the shelf, it should have good UX and keyboard controls so that it's just as easy if not easier to use with a keyboard rather than a mouse. As well, how does that same control work on mobile. Does it work with gestures? Is it easy to select the date using your fingers instead of a mouse or keyboard? These are all questions you should be asking and determining which scenario best fits your application.

Every application is different. When booking flights, we typically need the date range feature, as well, having a button for today's date or the ability to select time is not as important. However, when visiting your dentists website or choosing a doctor visit or maybe the best time to take your car in to get serviced, these scenarios may need a single date picker with the option of selecting time. Another trcky situation is a birthday picker. In my oppinion, the best way to do this is with a three step process. Select the Month, then day and finally year of the date you are trying to input. Because different applications throw different scenarios at you, the best date pickers will be ones that provide a variety of different options for the developer out of the box.

## Which One Do I Choose?

My goal here is not to push you in the direction of a single date picker, instead I would rather give you some of my ideas of wyhat the best date picker is and let you decide which one to choose. There is no doubt that when it comes to React and open source date pickers, I'm a huge fan of Material UI because they cover most of the features that I require in a date picker. As a developer of 20 years a datepicker calendar was one of the first very complicated web component I ever built and I have only built one myself since then. I know what type fo wrok goes into these very complex components so I definitely would rather you go with something open source that has all of the major issues worked out than try to build your own. 

As far as paid components go, I'm reluctant to tell you about KendoReact as you probably know we create amazing components. There are many great paid options out there. At the end of the day I want you to do your due dilligence and your own research to help you pick the date picker that works best for you. However, if you are interested in hearing more about what we provide, my friend Carl has put together a great piece on how to use our date picker in an article called ["Unleash the Power of the KendoReact DatePicker Component"](https://www.telerik.com/blogs/powerful-react-datepicker-component-example), so if you do pick ours, this is a great place to start to learn how to leverage it's power and build something amazing.

## Enterprise Level Support

To put it simple, components that are not licensed rarely have any type of support outside of at-will community help. Most of the big web development shops and enterprise level businesses have tight deadlines and their developers push technology to the edge. It's helpful to have a team to reach out to that has expert knowledge of the components you're working with and paying good money for.

Those are some of the key criteria on which to evaluate a React date picker for your next application. If there are any features that you think you can't live without, put them in the comments and let us know what your favorite date picker features are.