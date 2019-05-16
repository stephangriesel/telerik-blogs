---
title: What to Look For in a React Grid
published: true
description: Finding a grid for tabular data in your apps is something a lot of us eventually look for as an enterprise level developer. In this article I try to give some insight into what features I look for and why the KendoReact Grid fits the bill.
tags: React, JavaScript, Grid, Components
---

Finding a workhorse grid for tabular data in your applications is inevitably going to be something you have to figure out as a front-end developer working in any type of enterprise or large company especially when building line of business applications. Understanding what to look for and what features you can envision needing in the future when the client or your boss asks for more features is a good thing to think about up front when choosing your grid.

When we look for a grid, we sometimes need additional components to go along with it, if we can get a grid that comes as part of a larger library, this is a huge bonus. Purchasing a library which requires licensing is best for the scenario of building applications in the enterprise. This greatly narrows down the libraries we need to look at. When talking about these must haves, I'm going to show you the features that are available today in KendoReact, but many other UI library's work in a similar fashion. There are many options out there and it's just a matter of selecting one that fits all the criteria you want. As I can't know exactly what your project will entail, I will at least try and think about what most developers will need to know when looking for a grid solution. I hope that you can take this guide and expand on it for your own research and maybe you find that [KendoReact](https://KendoReact.com) is a great option for your next grid as it comes with a complete UI framework to boot.

## Performance

Most major component libraries are going to appear to work fine in application demos and during your development phase. But you may run into performance issues once you start using real data and users start interacting with it in test and production. For this reason, before making any final decisions on a particular library, you should use the React [Performance Tools](https://reactjs.org/docs/perf.html) to analyze it's performance and try to replicate a real use case or scenario similar to how you will use it in production.

We have an info on the [Telerik Blog](https://www.telerik.com/blogs/) about measuring performance including one article in particular about [Profiling React Components](https://www.telerik.com/blogs/profiling-react-components-with-the-user-timing-api) which shows how to use the [User Timing API](https://developer.mozilla.org/en-US/docs/Web/API/User_Timing_API). In combination with the React Blog's [Introducing the React Profiler](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html) article are great resources for measuring performance of a React component. Just as you would profile components you build and release yourself to production, when looking for a component library to bring into your project you should be putting those components through testing them with some of your application specific data. How do they perform under the situations you envision them working.

## Package Support

All React comonent libraries should give you the ability to install through [npm](https://docs.npmjs.com/about-npm/) or [github](https://help.github.com/en/articles/about-github-package-registry). Currently, KendoReact makes all of their components comsumable via the public npm package registry. Below is an example of importing and using the KendoReact Grid component into your project, I feel it's one of the easier components to get working.

![](https://imgur.com/XFSD3ZL.gif)

 We make our packages easily consumable through npm to ensure that if you need to get your hands dirty and build a demo, your just an **`npm install`** away! As well you can get a free month of support during a trial period, so that you can really have the time you need to evaluate the product or you can always just head over to our [Get Started](https://www.telerik.com/kendo-react-ui/getting-started/#toc-project-setup).

## Must Have Features in a React Grid

As someone who has constantly worked on teams where I have been asked to really push the envelope of what is possible for a grid, I have found the KendoReact grid to always meet my needs and then some. Let's go through a laundry list of things you should look for in a React Grid. I think mostly about my time building line of business applications for a large auto manufaturer. We had a massive inventory system and many of our views required a grid. A lot of my reccomended features come from the many requiremnts I have seen time after time building real grids in real applications. At the very minimum, there are three featuires we can definitely agree tat any grid we look at wil have to do these things.

### Sort, Filter and Paging

Of course we need to ensure that any grid that we decide to use has options for basic [Sorting](https://www.telerik.com/kendo-react-ui/components/grid/sorting/), [Filtering](https://www.telerik.com/kendo-react-ui/components/grid/filtering/) and [Paging](https://www.telerik.com/kendo-react-ui/components/grid/filtering/). We need a grid that will very easily demonstrate how to do each of these. So at a basic level let's see how the KendoReact grid handles these operations.

#### Sorting Examples

In React we typically will have a wrapper around our component that will allow us to keep track of our components state. We can utilize this local state to store information about our sorting, what field we want to sort on and the direction (ascending or descending), default settings. We can pass these into our component through props. In KendoReact, we have a sorting behavior with the ability to activate and deactivate through a a prop called `sortable`. The following StackBlitz example shows a very basic setup where we want to sort our data based on a productName. The default is true, and as you would guess, if you pass a `false` value to this prop you turn off the sorting feature. There are many other props easy to work with just like this one that allow you to gain more control and customization for sorting and other options. Very easily we can create a grid like below:

![](https://imgur.com/0BIqoH5.gif)

Another thing that we will need for our grid is a library we can use to query data, we can build our own of course, But in KendoReact, we have a package called the [Data Query](https://www.telerik.com/kendo-react-ui/components/dataquery/) package which helps when applying the sorting, filtering, grouping, and other aggregate data operations. It makes methods like `process()`, `orderBy`, and `filterBy` available. These methods are helpful in areas outside your grid component as well, it's just a utility library, but another huge bonus.

 In React we have the concept of a container component, these container components can be utilized to store and help track our state for the grid component, we can import the `orderBy` function use it to sort our data which we have imported from a `json` file which in turn has a column called `productName`. This makes it easy to loaded our data with default sort already in place, maybe we want to always start off in a state where the data is in reverse alphabetical order. We would have the following setup in our state object:

```
state = {
  sort: [
    { field: 'ProductName', dir: 'desc' }
  ]
}
```

And now when we create our Grid component in React we just need to pass the data into the grid using the `data` prop, the product of this value is an `orderBy` applied to the json data and as the second argument we can pass in our settings from our state object:

```
render() {
  return (
    <Grid data={orderBy(products, this.state.sort)}>
      <Column field="ProductID" />
      <Column field="ProductName" title="Product Name" />
      <Column field="UnitPrice" title="Unit Price" />
    </Grid>
  );
}
```

Already and with very minimal effort we have sorted our products by `productName` in a descending fashion. Although I'm not going to go through many code examples, you would see that the KendoReact Grid has many other ways of helping you manage your grid. WE can talk about some of those, just to get an idea of the level of customization you can achieve.

In order to make the individual column sortable we can use `onSortChange()`, an event that fires when the sorting of the Grid is changed. We handle this event ourself and sort the data using a simple arrow function that updates our state using the `setState()` method in React.

By default, when filtering is enabled, the Grid renders a filter row in its header. Based on the type of data the columns contain, the filter row displays textboxes in each column header where the user can filter string, numeric, or date inputs.

#### Filtering and Paging Examples

Most of the filtering that I want to do can be achieved with a [Custom Filter Cell](https://www.telerik.com/kendo-react-ui/components/grid/filtering/#toc-custom-filter-cell). This technique is easy to understand and it's powerful. Filtering can also be accomplished similar to how we did with our data earlier in the sorting example. Using a higher order component in conjunction with the `process()` Data Query method, we can manage local data. It has its own state and adds the filter, sort, total, and skip props to the Grid to handle an `onDataStateChange()` event. We can bind to more than one grids if needed using different sets of data without the need for you to write any logic for the filtering, sorting or paging.

Example showing Sorting, Filtering and Paging:
[StackBlitz Example](https://stackblitz.com/edit/kendoreact-hoc-with-stateful-grid?file=app/main.jsx)

### Virtual Scrolling

Sometimes, when we have a large amount of data in our grids. This could be a large numbers of columns or rows, we want to implement virtual scrolling. While the user is scrolling the table, the Grid needs to display only the visible data. In KendoReact, we make virtualized data a reality on both columns and rows. [Column Virtualization](https://www.telerik.com/kendo-react-ui/components/grid/columns/column-virtualization) ensures that columns outside the current visible aria of the grid will not be rendered.

As well, the grid has a special scrolling mode called [Virtual Scrolling](https://www.telerik.com/kendo-react-ui/components/grid/scroll-modes/virtual/). It's this scrolling mode that is most useful with large data sets. You can set a prop on the grid called `pageSize`. 

In [this demo](https://stackblitz.com/edit/kendoreact-virtual-scroll-mode?file=app/main.jsx), if you open the grid in a new browser window and inspect the grid (as seen in the animated gif below) as you scroll, you will notice the the only rows getting rendered to the view at any one time are only those that you see. Once you scroll past ofther records, they are removed and new records are rendered. Having this type of functionality can mean a boost to grid performance.

![](https://imgur.com/nOt0wBp.gif)

## Playing The Long Game

When looking for a good grid, or a general component library for that matter, you want to know that if you invest in using the library, that it's going to continue growing and that development on the library does not fall by the wayside. Some libraries have been short lived either because a main contributor spends less time on the project or because the company building the product was not able to continue the project. This is somnething you don't want. In most cases, active development on the project ensures future bug fixes and maintenenace at the least. In the case of KendoReact, we will continue maintaining the current components and continuously releasing new ones.

Knowing that a library has been around for that long, and that new flavors and products are being built to this day in React, your favorite front-end framework, it should give you confidence that it will be here for ten more years and will grow and bugs will get fixed quickly. These are things that you want in a library. Having these traits will ensure you can have longevity with the tools and that your skills can be transferable or exploited as a developer in another job. YOu only get this from the larger libraries that have longevity.

## Enterprise Level Support

We don't need to spend a lot of time on this one, it's plain and simple. Libraries that are not licensed rarely have any type of support outside of at-will community help. Most big web development shops and enterprise level businesses have tight deadlines and their developers push the technology to the edges, sometimes it's helpful to have someone to reach out to that is an expert on working with the library, we can make those people accessible to you, they run our customer support channels. With KendoReact you have the ability to choose from [several levels of customer support](https://www.telerik.com/purchase/support-plans).

Overall the Kendo React Grid is highly capable and stacks up on the higher end when compared to other similar component libraries for React. Just take a look at some of the other features that it provides here on the [KendoReact Data Grid (Table) Overview](https://www.telerik.com/kendo-react-ui/components/grid/). That page also has more information on thow to get started with a trial or license. However, we suggest looking around to see what else is out there that competes at this high level and if there are any features that the KendoReact grid does not have, you may find them obn our [KendoReact Roadmap](https://www.telerik.com/kendo-react-ui/roadmap/).
