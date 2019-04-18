---
title: React Amsterdam a Look Back
published: false
description: A look back at React Amsterdam Workshops and Talks.
tags: React, JavaScript, Amsterdam, Conference
---

React Amsterdam took place last week in Amsterdam Noord at [De Kromhouthal](https://kromhouthal.com/en/) organized by [GitNation](https://gitnation.org/) an amazing group of folks who do an amazing job at running developer conferences like [JS Nation](https://jsnation.com/) another Netherlands based JS community project and now conference, [React Day Berlin](https://reactday.berlin/) a first of ti's kind ful day conference in Berlin Germany, and others. This years React Amsterdam conference was attended by more then 1500 React developers. I attended the conference, volunteered for both days of workshops and ran a booth for my company [Progress](https://www.progress.com/) to show off our suite of [KendoReact](https://www.telerik.com/kendo-react-ui/) UI components.

## An Amazing Conference Location 

The Kromhouthal used to be a major marine engine manufacturing plant. I showed up the day before and got to see the hall before most of the confernce setup was complete. Alone it's a cold dark hall, a scene that in the past would have been a labor intense atmosphere with massive machines, today it's used for major events and can holds thousands of people with it's long hall and massively tall ceilings. The venue was easily accessible using the ferry from Central Station to the IJplein terminal but I also could have came from the Noordpark Metro station and in either situation just ahd a short 5 minute walk to the venue through a bustling creative area having a mix of local resident housing and soon to be a hotel and packing district. This area will continue to be a great location especially with plans to extend a bridge from the city center over the IJ (river).

## Amazing Workshops Teaching Valuable Principles and Patterns

Although not at the infamous Kromhouthal, part of React Amsterdam (the workshops) took place nearby, in the shadow of A'DAM Lookout at the [Tolhuistuin](https://tolhuistuin.nl/) a restaurant also fronting the IJ with amazing views for the workshop attendees. 

## Conference Day Highlights

There were so many great presentation and Lightening talks, I want to take some time to highlight what I think were the most valuable ones that I attended. Bieng someone who works with a lot of UI, layout and presentation in React, I am a big proponent of the fundamentals and general knowledge. i start to get lost when it comes to the advanced and deep dive topics outside of UI and basic React, and what's great about this conference is that they have something for everybody. Let's look at some of those talks and review them here:

### Requisite React (Kent C Dodds)
The conference started off strong with [Kent C Dodds](kentcdodds.com/about/) on the main stage with a talk called ["Requisite React"](https://www.youtube.com/watch?v=4KfAS3zrvX8&t=1405s/). In his own words, this talk is about: "Taking a few steps back and thinking about the usefulness of the fundamentals". We learn how to fix a droopy facuet head (with pics), and learn how understanding abstractions help us to be more effective when using them, not only in real life 😊 but also in our code. This means being mindful of our abstractions and understanding that each one ultimately has some type of cost. My favortie abstraction that he dives into is that of JSX and I won't ruin the talk, but getting a look at how we can easily convert our Babel into raw JS, we are able to see under the hood and understand this abstraction better. I felt a lot of the talk was mostly about how to level up as a React developer and if you were a boss or manager who sent several of your developers out to [React Amsterdam](https://react.amsterdam/), this is exactly the type of information you want out of the gate!

### Refactoring React (Siddarth Kshetrapal)
No time is wasted getting into another very valuable fundamentals based talk around [refactoring in React](https://www.youtube.com/watch?v=4KfAS3zrvX8&t=3268s), again we are defintiely getting our value right out of the gate with many helpful tips this time from [Siddarth Kshetrapel](https://github.com/siddharthkp/) an independent devloper from India who does an amazing job refactoring a login and authentication form. Starting with class components and constrtuctors with a fair amount of prop drilling involved, we refactor this code quickly into something more manageable and future proof. Some of the techniques that he talks about are spreading props, using methods passed down in props the proper way and how to ensure that we are not overriding prop values for methods or aplying them due to not managing our props correctly. He touches on principles like "Single Responsibility" and "Seperation of Concerns". I really like most the parts where he talks about understanding about mixing of controlled vs uncontrolled state and how to avoid this. Pick one, he likes uncontrolled components, and this gives us the chance to get into higher order components or better yet, React Hooks. `useSmartness()` FTW!

So those talks were very code heavy and I was already in the mood for some straight up slide talk! My favorite kiind fo talks! I don't have to strain my eyes and I still learn some new stuff I didn't know before. 

### A Common Design Language (Andrey Okonetchnikov)
[Andrey](https://github.com/okonet) who also did an amzing workshop on the same topic of Design Systems in React, puts all the pertinent info into a very clean and easy to understand talk on building a common design language and reducing the choices of options between typography, spacing and color to create a design language system. Using a common design language systems allows for reusability of design choices across multiple products and logos. This can be something as simple as he points out as the design of the German government logos vs Austrian government logos. One has a clear design system and language the other although creative lacks distinguishable characteristics that would show a clear alignment of all of it's properties through a common design language.

<!-- photos of logos side by side -->

[Andrey's presentation](https://www.youtube.com/watch?v=4KfAS3zrvX8&t=6900s) had many strong visuals like above that helped to show us how a design system language can help not only your developers and designers talk, but also help your organization speak to it's clients and customers clearly and with great meaning and commonality. The presentation leads into design languagges for digital products and this is where we tie in the component oriented capabilities of React that make it easy to define a common language with your UI achieveing similar results as discussed before but now within digital products. A truly amazing talk and I really suggest taking the time to watch.

### Designing With React (Mark Dalgleish)
Following teh previous design language presentation, we nicely transition into a talk from Mark Dalgleish on [designing in React](https://www.youtube.com/watch?v=4KfAS3zrvX8&t=8562s). Using design systems paired with React Mark is able to design in the final medium. Because React is so component oriented, it allows us to build our own domain specific language. I have seen first hand at companies I have worked at like Tesla capitalize on the ability to do this in React and other web technologies. Mark has some other examples of this idea spreading throughout our industry as many companies build their own design systems. Mark's major points backup the ability to capture the design intent from our design systems and applying them to the web and native apps. [Seek style-guide](https://github.com/seek-oss/seek-style-guide) is something that Mark's company has created and is a great resource and example of a design system for React executed remarkably.

Another amazing resource that Mark shows off is the [React Sketch.app](http://airbnb.io/react-sketchapp/) which renders React components to Sketch helping to design with real data, in react with real component code and manage your design system implemented in React. Watch the video for information on an amazing npm package they created called `html-sketchapp`. I will let you discover that amazing gem on your own. 

So far I'm 4 talks in, and I have watched the majority of the talks running back to our booth each break to interact with the attendees talk components. For someone like me who just likes to be totally immersed in technology and talking about it, this event really allowed me to get into my element. One of the things I love about my company and my position is that they let me geek out about React and not feel like I have to be a pushy sales person. Aside from questions I had to field about our own component library, most of the talk at the conference was around fundamentals, bleeding edge features and the React roadmap, what's coming next. just an amazing conference to really get knee deep in JavaScript and React more specifically.

The next four talks are all on Server Side Rendering (SSR) using frameworks like Next JS for pre-rendering, Crystalize for the backend to create lightening fast scalable SSR React apps, the upsides and downsides of creating apps that use SSR, topics like rehydration, time to interactive and other things related to how our larger e-commerce sites render. In the e-commerce world, shaving milliseconds or maybe even full seconds off of load time can be very valuable. These 4 talks take you on a journey through the benefits and gotchas of SSR.

- [Next for Next.js](https://www.youtube.com/watch?v=4KfAS3zrvX8&t=10427s) (Tim Neutkens)
- [Lightning fast SSR React](https://www.youtube.com/watch?v=4KfAS3zrvX8&t=10991s) (Håkon Gullord Krogh)
- [Speeding up React SSR](https://www.youtube.com/watch?v=4KfAS3zrvX8&t=11452s) (David Mark Clements)
- [Demystifying Server-Rendered React Apps](https://www.youtube.com/watch?v=4KfAS3zrvX8&t=11870s) (Fernando Porazzi) 


## React is Amsterdam

Talk abouit how Amsterdam is a perfect city for JavaScript and more importantly React developers.  Some of the sponsors at the vents were based in or had offices in Amsterdam or Netherlands. The city offers so much in historical, artistic, tech and shopping, so it's obviously a great place to bring the React community and is very relaxed yet highly invigorated at the same time. Given enough time and the ability to travel throughout the city and learn the Metro, Dutch national rail company NS (Nederlandse Spoorwegen) and the various other ferry and tram systems, you can easily move around to the areas that you want to visit and crank up the energy or turn it down by traveling just out of the city's center.

I stayed in the Wilbautstraat area just 4 stops off the metro from Central Station at a wonderful hotel that I talk about more in my [Developers Guide to React Amsterdam](https://dev.to/httpjunkie/the-developers-guide-to-react-amsterdam-4h60/).

## React 2020

If you are planning on attending the React Amsterdam 2020 event, mark your calendars now, it will be April 16th and 17th. 