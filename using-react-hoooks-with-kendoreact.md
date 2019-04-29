---
title: Using React Hooks With kendoReact
published: false
description: Hooks are now stable in React, let's understand how to use them with everyday KendoReact components.
tags: React, JavaScript, Kendo, Components
---

With the release of Hooks, building React applications and managing local state of components is now easier, more straight forward and concise. Yes there is a lot to know about Hooks from a conceptual standpoint, and we have many articles here on the Telerik blog to help you get aquainted with Hooks and started using them in your application. Building React applications has not always been a breeze, in fact before Hooks there was a lot you had to know about several patterns and practices in React just to do everyday things like state management, seperating logic within your components, ensuring that you could share lifecycle methods and such across components and resusing rendering logic across many components. The reoccurring theme here is code and logic reuse and to do it well, it required understanding about several different techniques like Mixins, Higher Order Components, and Render Props. Before Hooks, React developers when faced with ever growing local state concerns would sometimes reach for Redux or MobX to manage their data  and communication state, this was a natural use for Redux, but there are other forms of application state that using Redux is typically a poor choice for. Before Hooks was released, this type of state was accessed using class based components that would interact with `this.state`, a convention that React is familliar with and allowed us to instantiate and update in a one way data flow pattern.

**We may talk about concepts in this article that you may or may not understand, below are some articles that explore the different ways to use Hooks. If you feel that you don't understand something in this article it's most likely easy to look up and dive deeper in these article I have provided**

- [Say Hello to Create React App (2/3)](https://www.telerik.com/blogs/hello-create-react-app-2) to help get started in React
- [Learn Basic React Hooks State and Effects](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects) for local state and effects
- [Learn Basic React Hooks for Context](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context) 
- [Learn Basic React Hooks for Reducers](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-reducers) 
- [Learn to Create Custom React Hooks](https://www.telerik.com/blogs/everything-you-need-to-create-a-custom-react-hook) 

The [ReactJS.org documentation on Hooks](https://reactjs.org/docs/hooks-intro.html) is also a great resource that you should know about.

As I stated before, Hooks are great for dealing with a certain types of application state. A few examples are control state and local component state and session state. I'd like to leverage hooks when working with our KendoReact components, but I want to start simple. Let's refactor one of the StackBlitz demos from a demo that uses classes and switch it to using functional components instead. We will look for instances where the demo is using `this.state` and `this.setState` because when we convert the component to functional we will not have to use the `this` keyword anymore, we will not need to use a constructor or call `setState`. When we work with Hooks, we do things slightly differntly. So let's get into refactoring the KendoReact demo that shows how to work with our [KendoReact Dialog](https://www.telerik.com/kendo-react-ui/components/dialogs/dialog). I have [forked the original StackBlitz demo](https://stackblitz.com/edit/kendoreact-dialog-class-based?file=app/main.jsx) from the Dialog Overview page, that will be our starting point.

If you look at this demos `main.jsx` page which I have shown below, there are several target areas we can identify that will change when using a functional component and React Hooks. The code and lines highlighted in GREEN will need modification, and the lines highlighted in RED will be able to be removed completely.

![](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/refactor_highlightsa35421f46b9440238e5b2b97852059ba.png?sfvrsn=66550209_0)

1. On line 5 we have a `class App` definition, we need to convert this to a functional component.
2. On line 6 we have a constructor, line 7 a call to `super()` and on line 9 we have some binding. None of these are needed in our functional component using Hooks.
3. On line 9 we create an instance of our state and give it a default value of `true` this will be done all in one line with Hooks.
4. On line 15 we have a function that calls `this.setState` and when we convert to using hooks, we will be calling a different method, one that we define ourselves on the same line as I mentioned before we we define our `visible` hook.
5. On line 21 we have a call to `render()` which will not be necessarry in our functional component
6. On line 24, 25, 28 and 29 we have refernces to `this` that will not be needed. Also we will be calling a differnt method than `toggleDialog` as hooks has a slightly differnt naming convention we will follow.

The first thing we need to do is to convert the class to a functional component, remove the constructor and call to `super()`, the binding of the `toggleDialog()` function.

