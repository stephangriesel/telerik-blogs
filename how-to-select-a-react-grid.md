---
title: What to Look For in a React Grid
published: true
description: Hooks are now stable in React, let's understand how to use them with everyday KendoReact components.
tags: React, JavaScript, Grid, Components
---

Finding a workhorse grid for tabular data in your applications is inevitably going to be something you have to figure out as a front-end developer working in any type of enterprise or big business. Understanding what to look for and what features you can envision needing in the future when the client or your boss asks for more details, more rows and by the way, make the font bigger will ya. Well, you just going to have to tell him that the font is staying 14px, but the other stuff, we can help with.

When we look for a grid, especially in the enterprise, where you are buying several licenses for your key front-end developer needs to have a few things. When talking about these must haves, I'm going to show you these features in KendoReact, just know that there are many options out there and it's just a matter of selecting one that fits all the criteria you want. As I can't know exactly what your porject will entail, you can't always fathom what new features your grid or your application for that matter might end up needing. So ensuring you find a solution that can grow with you and your development needs is priority.

## Must Have Features in a React Grid

As someone who has constantly worked on teams where I have been asked to really push the envelope of what is possible for a grid, I have found the KendoReact grid to always meet my needs and then some. As well there are other grids on the market so let's go through a laundry list of things you should look for in a React Grid. I think mostly about my time building line of business applications for a large auto manufaturer. We had a massive inventory system and many of our views required a grid. These are the features that I would not have been able to work with if I didn't have them.

### Basic Sort, Filter and Paging Options

Of course we need to ensure that any grid that we decide to use has options for basic [Sorting](https://www.telerik.com/kendo-react-ui/components/grid/sorting/), [Filtering](https://www.telerik.com/kendo-react-ui/components/grid/filtering/) and [Paging](https://www.telerik.com/kendo-react-ui/components/grid/filtering/). At it's basic we need a grid that will very easily demonstrate how to do each of these. So at a basic level let's see how the KendoReact grid handles these operations.

In React we typically will have a wrapper around our component that will allow us to keep track of a single components state. We can utilize this local state to store the information about our sorting, what field we want to sort on and the direction as in ascending or descending. We handle these setting through props and we can easily turn the sorting behavior on and off through a prop called `sortable`. The following StackBlitz example shows a very basic setup where we want to sort our data based on a productName. The React component that we use the following props that we will utilize to do this basic sorting: `sortable`, the default is true, however if you pass false to this prop you will toggle off the sorting feature. But this prop alone is just a switch so to speak. In order to get full sorting capabilities we need to easily be able to change the order of our data and KendoReact makes this very easy with kendo-data-query. 

The [Data Query package](https://www.telerik.com/kendo-react-ui/components/dataquery/) helps when applying the sorting, filtering, grouping, and other aggregate data operations. This helps to keep your component that wraps your grid nice and clean by ensuring that you don't have to write these sometimes basic and othertimes non-trivial operations yourself. You can import the `orderBy` function and immdiately be able to write code that when I click on a product name takes my data that the grid is using and orders it by name. That code would look something like this:

```

```

### Virtual Scrolling

## Playing The Long Game

When looking for a good grid, or a general component library for that matter, you want to know that if you invest in using the library, that it's going to continue growing and that development on the library does not fall by the wayside. Some open source libraries and commercial ones too, have had short lives either because a main contributor spends less time on the project or because the company building the product was not able to keep the project a float. It almost feels like I'm teeing this one up for Kendo UI. Whether we are talking about KendoReact, kendo for Angular or any other flavor of our components, you can trace back Kendo UI back to the early 2000's and it's JavaScript flavors to it's days of being a huge competitor with jQuery UI. 

Knowing that a library has been around for that long, and that new flavors and products are being built to this day in React, your favorite front-end framework, it should give you confidence that it will be here for ten more years and will grow and bugs will get fixed quickly. These are things that you want in a library. Having these traits will ensure you can have longevity with the tools and that your skills can be transferable or exploited as a developer in another job. YOu only get this from the larger libraries that have longevity.

## Enterprise Level Support

We don't need to spend a lot of time on this one, it's plain and simple. Libraries that are not licensed rarely have any type of support outside of at-will community help. Most big web development shops and enterprise level businesses have tight deadlines and their developers push the technology to the edges. You may be pushing a component beyond it's performance capabilities or using a tool in the wrong way. having the ability to get 24-7 support is not something every UI library out there has. It's something we have you covered with on our components, but if you do choose another Grid or component library, this is feature that you will not only need, but will save you time and costly development work by not being able to easily speak to the experts and engineers that build the tool. You may even look further than support and want your component library to have a dedicated team out there on Twitter advocating. These are also people that can help you learn and use the component library.

