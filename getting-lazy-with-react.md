---
published: false
title: Getting Lazy with React
summary: As your app grows, so does your bundle size. Splitting your bundle can help you lazy-load only the things the user absoutely needs. This can reduce the code needed for an initial load, delaying other loading only when the user asks for it.
keywords: Guide, JavaScript, React, Lazy-loading, Suspense
---

React has been adding many amazing features over the past year that make working with components in React a breeze. Back in October of 2018, React released it's lazy loading feature in Ract 16.6\. I knew that React had a pretty decent component based Router system that I could use and I had learned about this new feature coming to React called Suspense. In Suspense would be a function I could use called lazy that would allow me to achieve the lazy loading capabilities that I was looking for. But I was more amazed at how much simpler it seemed to be. And that has been my experience most of the time in React. I find that if React has an opinion about something and they help you to do it. It's going to be pretty easy and straightforward.

I started my learning out in the React blog with an article highlighting the release of this feature: [React v16.6.0: lazy, memo and contextType](https://reactjs.org/blog/2018/10/23/react-v-16-6.html). This document links to many other documentation resources to help you understand code splitting and how it is part of the React Suspense and Lazy features.

A few must see videos on the subject are [Jared Palmer](https://www.youtube.com/watch?v=SCQgE4mTnjU) and <a href="">Dan Abramov's</a> React Conf 2018 talks on suspense as well as <a href="">Andrew Clark's "React Suspense"</a> talk at ZEIT day in San Francisco.

## What Does This Mean for Developers

The added asynchronous rendering capabilities means that we can optimize the initial page load increasing the performance of our application and help to provide a better user experience by loading chunks of our application delayed.

We want to defer non-critical resources and load them on demand as needed using code splitting. This will help us to manage the loading of images, data, anything we want to bundle up seperately, we can get really creative with these features.

A good practice in building your web application will be to segregate these resources as critical and non-critical. We want to load the critical stuff first as well as any data that is needed to serve the initial page load. Then less critical resources can get loaded as we move to a new page, roll over an image, whatever.

## Basic Approach to Code Splitting

The best way to use code splitting in your application is through the use of the dynamic import syntax. Create React App and Next.js both support this syntax in their latest versions. An example of that might look like this:

    import("./math").then(math => {
      math.sum(1, 2, 3);
    });

## Code Splitting With Lazy in React

In React, we have a function as of React 16.6 that we can use letting us render a dynamic import as a component. This makes splitting and loading React components a breeze. Instead of just importing a component from another file and and rendering it immediately. Let's say that we have an **ArtistComponent** that has a list of events that we can loaded from an **Events** component and we only want to load the **Events** component if the **ArtistComponent** gets loaded. We could do the following:

    const Events = React.lazy(() => import('./Events'));

    function ArtistComponent() {
      return (
        <div className="event-list">
          <Events />
        </div>
      );
    }

When using React.lazy, we achieve automatically loading of a bundle containing the **Events** component when our **ArtistComponent** renders. But what happens when the module containing the **Events** component is not yet loaded by the time the **ArtistComponent** renders? If we bring the Suspense component into the mix, we can provide a fallback to display until the **Events** component is loaded. Notice below that the only change in order to provide a loading indicator is the addition of the **Suspense** component and a prop named `fallback` in which we pass a basic loading **div**.

    const Events = React.lazy(() => import('./Events'));

    function ArtistComponent() {
      return (
        <div className="event-list">
          <Suspense fallback={<div>Loading...</div>}>
            <Events />
          </Suspense>
        </div>
      );
    }

`React.lazy()` takes in a function that returns a promise which is the result of an import statement.

What if I want more than one component loading at the same time? That's fine, we can wrap many lazy loaded components inside the Suspense component and everything will work exactly the same:

    const Events = React.lazy(() => import('./Events'));
    const Events = React.lazy(() => import('./Gallery'));

    function ArtistComponent() {
      return (
        <div className="event-list">
          <Suspense fallback={<div>Loading...</div>}>
            <Events />
            <Gallery />
          </Suspense>
        </div>
      );
    }

All of this is providing for a better user experience. Again this is nothing new that we couldn't do in React before, however; you would have to import other dependencies and libraries to do it, a library like `react-loadable` would be used. But now with Suspense and Lazy, we can do it inside of React core without adding of additional dependencies.

We should also look at one more example of how to do this with React Router.

    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
    import React, { Suspense, lazy } from 'react';

    const Events = lazy(() => import('./routes/Events'));
    const Gallery = lazy(() => import('./routes/Gallery'));

    const App = () => (
      <Router>
        <Suspense fallback={<div>Loading...</div>}>
          <Switch>
            <Route path="/events" component={Events}/>
            <Route path="/gallery" component={Gallery}/>
          </Switch>
        </Suspense>
      </Router>
    );

## A Simple Demo Application

Now that we have a pretty basic idea of how to use Suspense just by walking through the canonical code samples above, let's create a simple working app in StackBlitz. We just need to show some very basic stuff.

First we will need a navigation and some routing to simulate an application that has a home page that loads immediately and then an additional page that gets loaded on demand by the user actually navigating to the page. The idea is that we don't load the second page until the user clicks on the navigation link for it.

The demo has a `info.js` page that will provide some basic information to our users upon the site loadinging initially. We have not setup any dynamic loading on the `info.js` file and we set it's route to be a forward slash.

next we have a page called `Repos` and this page calls out to an API and generates a list of popular JavaScript repos from GitHub. But this page could be anything. This second page is only sometimes clicked on and for this reason we don't want to eagerly load it for every user. Let's take a look at what this might look like, first we have the dynamic import:

    const Repos = lazy(() => import('./components/Repo'));

Next we have our JSX using all of the tricks we learned in the code samples above:

    <Router>
      <>
        <ul>
          <li><Link to="/">Info</Link></li>
          <li><Link to="/repos">Repos</Link></li>
        </ul>
        <hr />
        <Suspense fallback={<div>Loading...</div>}>
          <Route exact path="/" component={Info} />
          <Route exact path="/repos" component={Repos} />
        </Suspense>
      </>
    </Router>

You can see all of this in action in the following StackBlitz demo:

[STACKBLITZ DEMO](https://stackblitz.com/edit/react-router-with-suspense?file=index.js&amp;view=editor&amp;ctl=1)

I have actually commented out the normal dynamic import that you would use, and wrapped it with a promise instead, I return the dynamic import, but I want to specify some time before it loads that component in order to simulate a real loading issue that would result in using the Suspense fallback.

    // const Repos = lazy(() => import('./components/Repos'));
    const Repos = lazy(() => new Promise(resolve => {
      setTimeout(() => resolve(import('./components/Repos')), 1500);
    }));

We are just scraping the surface here, but we are doing things in a much easier way than if we had to handle a lot of the issues that React takes care for us behind the scenes with error boundaries and loading. There is much more to learn about using React's new Suspense features, how to create a better UX experience amongst other things, but I hope that this simple tutorial gives you a good idea of how to easily get started and dip your toes in by using lazy loading in React. For more information on Suspense and React's Lazy feature, try visiting the [ReactJS.org documentation](https://reactjs.org/docs/getting-started.html) and watching all of the great videos I linked to from above!

Thanks for reading, I hope you enjoy each of our React Learning Series articles and while you're here and learning about components, why not stop by the [KendoReact](https://www.telerik.com/kendo-react-ui/) page and check out our live StackBlitz demos for our components built from the ground up for React!