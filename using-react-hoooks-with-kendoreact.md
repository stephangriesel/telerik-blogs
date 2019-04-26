---
title: Using React Hooks With kendoReact
published: false
description: Hooks are now stable in React, let's understand how to use them with everyday KendoReact components.
tags: React, JavaScript, Kendo, Components
---

With the release of Hooks, building React applications and managing local state of components is now easier, more straight forward and concise. Yes there is a lot to know about Hooks from a conceptual standpoint, and we have many articles here on the Telerik blog to help you get aquainted with Hooks and started using them in your application. Building React applications has not always been a breeze, in fact before Hooks there was a lot you had to know about several patterns and practices in React just to do everyday things like state management, seperating logic within your components, ensuring that you could share lifecycle methods and such across components and resusing rendering logic across many components. The reoccurring theme here is code reuse. To really get the best out of your React application understanding how to achieve this has not always been straight forward. It required understanding about several different techniques. To be specific, Mixins, Higher Order Components and Render Props just to do very basic co-location of logic and state management. As well React developers when faced with ever growing local state concerns would sometimes reach for Redux or MobX to manage that state. Using these state management tools for local component state has never felt like a great ideea to me, but it was often done and in some case done instead of using the local state object provided by React or in conjunction with local state. This could turn into massive amounts of boiler plate and in my opinion made understanding how to do state management in Ract very confusing.

We have turned a corner in the React world however, today these problems have a very simple and straight forward solution, but it does take some getting used to and practicing with React Hooks. If you are new to React or React Hooks I got you covered, let me suggest a few articles before we get going, just in case you feel you need a refresher on any of the topics below. Feel free to wander off and I will wait right here for you, then we can dig into using React Hooks with [KendoReact](https://www.telerik.com/kendo-react-ui/): 

- [Say Hello to Create React App (2/3)](https://www.telerik.com/blogs/hello-create-react-app-2) to help get started in React
- [Learn Basic React Hooks State and Effects](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects) for local state and effects
- [Learn Basic React Hooks for Context](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context) 
- [Learn Basic React Hooks for Reducers](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-reducers) 

The best place to start is with our 