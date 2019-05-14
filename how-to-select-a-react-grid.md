---
title: What to Look For in a React Grid
published: true
description: Hooks are now stable in React, let's understand how to use them with everyday KendoReact components.
tags: React, JavaScript, Grid, Components
---

Finding a workhorse grid for tabular data in your applications is inevitably going to be something you have to figure out as a front-end developer working in any type of enterprise or big business. Understanding what to look for and what features you can envision needing in the future when the client or your boss asks for more details, more rows and by the way, make the font bigger will ya. Well, you just going to have to tell him that the font is staying 14px, but the other stuff, we can help with.

When we look for a grid, especially in the enterprise, where you are buying several licenses for your key front-end developer needs to have a few things. When talking about these must haves, I'm going to show you these features in KendoReact, just know that there are many options out there and it's just a matter of selecting one that fits all the criteria you want. As I can't know exactly what your porject will entail, you can't always fathom what new features your grid or your application for that matter might end up needing. So ensuring you find a solution that can grow with you and your development needs is priority.

## Performance

Most of the major component libraries are going to workout in your component building phase  and you may not run into performance issues until you start using some real data and interacting with it in a live environment. For this reason, before making any final decisions on a particular library, you should use tools like the React [Performance Tools](https://reactjs.org/docs/perf.html).

We some amazing articles on our blog about performance including one in particular about [Profiling React Components] complete with examples of how to get started using the User Timing API. Just as you would profile components you build and release yourself to production, when looking for a component library to bring into your project you should be putting those components through testing them with some of your application specific data. How do they perform under the situations you envision them working.

## Package Support

All React comonent libraries should give you the ability to install through [npm](https://docs.npmjs.com/about-npm/) or [github](https://help.github.com/en/articles/about-github-package-registry). Currently, KendoReact makes all of their components comsumable via the public npm package registry. We make our packages easily consumable through npm to ensure that if you need to build a demo to show your boss, that's totally fine! As well you can get a free month of support so that you can really test out every aspect of what it would be like developing with the KendoReact library having full 24/7 support. 

## Touch and Mobile

## Security

## Must Have Features in a React Grid

As someone who has constantly worked on teams where I have been asked to really push the envelope of what is possible for a grid, I have found the KendoReact grid to always meet my needs and then some. As well there are other grids on the market so let's go through a laundry list of things you should look for in a React Grid. I think mostly about my time building line of business applications for a large auto manufaturer. We had a massive inventory system and many of our views required a grid. These are the features that I would not have been able to work with if I didn't have them.

### Basic Sort, Filter and Paging Options

Of course we need to ensure that any grid that we decide to use has options for basic [Sorting](https://www.telerik.com/kendo-react-ui/components/grid/sorting/), [Filtering](https://www.telerik.com/kendo-react-ui/components/grid/filtering/) and [Paging](https://www.telerik.com/kendo-react-ui/components/grid/filtering/). We need a grid that will very easily demonstrate how to do each of these. So at a basic level let's see how the KendoReact grid handles these operations.

#### Sorting

In React we typically will have a wrapper around our component that will allow us to keep track of a single components state. We can utilize this local state to store the information about our sorting, what field we want to sort on and the direction as in ascending or descending. We handle these setting through props and we can easily turn the sorting behavior on and off through a prop called `sortable`. The following StackBlitz example shows a very basic setup where we want to sort our data based on a productName. The React component that we use the following props that we will utilize to do this basic sorting: `sortable`, the default is true, however if you pass false to this prop you will toggle off the sorting feature. But this prop alone is just a switch so to speak. In order to get full sorting capabilities we need to easily be able to change the order of our data and KendoReact makes this very easy with kendo-data-query. 

The [Data Query package](https://www.telerik.com/kendo-react-ui/components/dataquery/) helps when applying the sorting, filtering, grouping, and other aggregate data operations. In React we have the concept of a container component, these container components are the best place to keep track of our state for our grid component, to further help to organize and keep this container component clean by ensuring that you don't have to write all of the code that orders and filters our data for our component, we can import the `orderBy` function use it to sort our data by `productName`. This makes it super easy to ensure that our data is initially loaded with a sort in place, maybe we want to always start off in a state where the data is in reverse alphabetical order. We would have the following setup in our state object:

```
state = {
  sort: [
    { field: 'ProductName', dir: 'desc' }
  ]
}
```

And now when we create our Grid component in React we just need to pass the data into the grid using the `data` prop and we can use `orderBy` and pass in our settings that we already have stored in our state object:
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

Already and with very minimal effort we have sorted our products by `productName` in a descending fashion. It's important to look for libraries that give you additional tools to work with basic data operations. This additional ecosystem around KendoReact supplies things like data operations, animations and other common utilities that make working with the individual components, like the data grid very easy to do.

In order to make the individual column sortable we just need to add a few more props that will tell the grid what to do `onSortChange`. This brings us to our next thing to look out for. When searching for a React Grid, you will need to carefully review the API and see what props the grid surfaces for us to work with. The `onSortChange()` is an event that fires when the sorting of the Grid is changed. We handle this event ourself and sort the data using a simple arrow function that updates our state using the `setState()` method in React.

By default, when filtering is enabled, the Grid renders a filter row in its header. Based on the type of data the columns contain, the filter row displays textboxes in each column header where the user can filter string, numeric, or date inputs.

#### Filtering

Most of the filtering that I want to do can be achieved with a [Custom Filter Cell](https://www.telerik.com/kendo-react-ui/components/grid/filtering/#toc-custom-filter-cell). This technique is poular among different grid options out there and it's easy to understand and it's powerful. 

### Virtual Scrolling

## Playing The Long Game

When looking for a good grid, or a general component library for that matter, you want to know that if you invest in using the library, that it's going to continue growing and that development on the library does not fall by the wayside. Some open source libraries and commercial ones too, have had short lives either because a main contributor spends less time on the project or because the company building the product was not able to keep the project a float. It almost feels like I'm teeing this one up for Kendo UI. Whether we are talking about KendoReact, kendo for Angular or any other flavor of our components, you can trace back Kendo UI back to the early 2000's and it's JavaScript flavors to it's days of being a huge competitor with jQuery UI. 

Knowing that a library has been around for that long, and that new flavors and products are being built to this day in React, your favorite front-end framework, it should give you confidence that it will be here for ten more years and will grow and bugs will get fixed quickly. These are things that you want in a library. Having these traits will ensure you can have longevity with the tools and that your skills can be transferable or exploited as a developer in another job. YOu only get this from the larger libraries that have longevity.

## Enterprise Level Support

We don't need to spend a lot of time on this one, it's plain and simple. Libraries that are not licensed rarely have any type of support outside of at-will community help. Most big web development shops and enterprise level businesses have tight deadlines and their developers push the technology to the edges, sometimes it's helpful to have someone to reach out to that is an expert on working with the library, we can make those people accessible to you, they run our customer support channels. With KendoReact you have the ability to choose from [several levels of customer support](https://www.telerik.com/purchase/support-plans), something a lot of UI libraries don't make available. It's something we have you covered with on our components, but if you do choose another Grid or component library, this is feature that you will not only need, but will save you time and costly development work by not being able to easily speak to the experts and engineers that build the tool. You may even look further than support and want your component library to have a dedicated team out there on Twitter advocating. These are also people that can help you learn and use the component library.

