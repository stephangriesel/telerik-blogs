---
title: Using React Hooks With kendoReact
published: false
description: Hooks are now stable in React, let's understand how to use them with everyday KendoReact components.
tags: React, JavaScript, Kendo, Components
---

With the release of Hooks, building React applications and managing the local state of components is now easier, more straight forward and concise. Yes, there is a lot to know about Hooks from a conceptual standpoint, and we have many articles here on the Telerik blog to help you get acquainted with Hooks and started using them in your application. Building React applications has not always been a breeze, in fact before Hooks there was a lot you had to know about several patterns and practices in React just to do everyday things like state management, separating logic within your components, ensuring that you could share lifecycle methods and such across components and reusing rendering logic across many components. 

The reoccurring theme here is code and logic reuse and to do it well, it required understanding about several different techniques like Mixins, Higher Order Components, and Render Props. Before Hooks, React developers when faced with ever growing local state concerns would sometimes reach for Redux or MobX to manage their data and communication state, this was a natural use for Redux, but there are other forms of application state that using Redux is typically a poor choice for. Before Hooks was released, this type of state was accessed using class-based components that would interact with `this.state`, a convention that React is familiar with and allowed us to instantiate and update in a one-way data flow pattern.

**We may talk about concepts in this article that you may or may not understand, below are some articles that explore the different ways to use Hooks. If you feel that you don't understand something in this article it's most likely easy to look up and dive deeper in these articles I have provided**

- [Say Hello to Create React App (2/3)](https://www.telerik.com/blogs/hello-create-react-app-2) to help get started in React
- [Learn Basic React Hooks State and Effects](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects) for local state and effects
- [Learn Basic React Hooks for Context](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context) 
- [Learn Basic React Hooks for Reducers](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-reducers) 
- [Learn to Create Custom React Hooks](https://www.telerik.com/blogs/everything-you-need-to-create-a-custom-react-hook) 

The [ReactJS.org documentation on Hooks](https://reactjs.org/docs/hooks-intro.html) is also a great resource that you should know about.

As I stated before, Hooks are great for dealing with certain types of application state. A few examples are control state, local component state and session state. I'd like to leverage hooks when working with our KendoReact components, but I want to start simple. Let's refactor one of the StackBlitz demos from a demo that uses classes and switch it to using functional components instead. We will look for instances where the demo is using `this.state` and `this.setState` because when we convert the component to functional we will not have to use the `this` keyword anymore, we will not need to use a constructor or call `setState`. When we work with Hooks, we do things slightly differently. So let's get into refactoring the KendoReact demo that shows how to work with our [KendoReact Dialog](https://www.telerik.com/kendo-react-ui/components/dialogs/dialog). I have [forked the original StackBlitz demo](https://stackblitz.com/edit/kendoreact-dialog-class-based?file=app/main.jsx) from the Dialog Overview page, that will be our starting point.

If you look at this demo's `main.jsx` page which I have shown below, there are several target areas we can identify that will change when using a functional component and React Hooks. The code and lines highlighted in GREEN will need modification, and the lines highlighted in RED will be able to be removed completely.

![](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/refactor_highlightsd0a7fbadfafc46d9a85a3d76286e1d3e.png?sfvrsn=67caeb6d_0)

1. On line 6 we have a `class` definition, we need to convert this to a functional component.
2. On line 7 we have a constructor, on line 8 a call to `super()` and on line 10 we have some binding. None of these are needed in our functional component using Hooks.
3. On line 9 we create an instance of our state and give it a default value of `true` this will instead be a call to the `useState` hook.
4. On line 13 we need to rename the `toggleDialog` function and switch it to the ES6 Arrow Function style syntax, lines 14 through 16 will simply call an update method provided by our `useState()` assignment called `setVisible` and the value it will be referencing will be `visible` instead of `this.state.visible`.
5. On line 21 we have a call to `render()` which will not be necessary in our functional component
6. On line 22, 23, 26 and 27 we have references to `this.` and `this.state` that will need to be to reference `visible` and `toggleVisible` instead of `toggleDialog` and I will explain later on why I want to rename that function.

let's get started. The first thing we need to do is to convert the class to a functional component, remove the constructor and call to `super()`, the binding of the `toggleDialog()` function. There are multiple syntax options we could use here, I prefer the ES6 Arrow Function style:

    const multiply = (x, y) => { return x * y };  

In our component line 6 would now look like this:

    const DialogWrapper = () => {

Let's go ahead and set up our hook that will take the place of the state object. Instead of creating an object named state, we will set up a call to `useState()` and destructure its return value into a variable that will hold our state and an update/set method to update that piece of state. Our name of our state will be `visible` and its update method will be called `setVisible`. We will basically remove the entire constructor and replace it with this one line:

    const [visible, setVisible] = useState(true);

Since we are using the `useState()` basic hook, we also need to import it. Our React import will now look like:

    import React, { useState } from 'react';

Next, we need a function inside this component that will deal with calling `setVisible` for the purposes of toggling its value. We decided that we would name it `toggleVisible` instead of `toggleDialog` and since we are in a functional component, the syntax that was used before will not work, for this reason, I will update it to the ES6 Arrow Function style. This function will simply set the `visible` state to the opposite of its current state at the time. behind the scenes React is managing this `visible` variable in a similar way as it would if you were calling `setState` in a class component. that management is just being abstracted by something behind the scenes called `useReducer` but we are not going to get into exactly how all of that works in this simple example. Our new code looks like the following:

    const DialogWrapper = () => {;
      const [visible, setVisible] = useState(true);
      const toggleVisible = () => setVisible(!visible);

Now we need to get rid of the `render()` block and it's two curly braces. Also, we need to remove all references to this `this.toggleDialog` and `this.state.visible` and change them to `toggleVisible` and `visible` accordingly. Now inside of our `return()` we will have the following changes:

    return (
      <div>
      <Button className="k-button" onClick={toggleVisible}>Open Dialog</Button>
      {visible && <Dialog title={"Please confirm"} onClose={toggleVisible}>
        <p style={{ margin: "25px", textAlign: "center" }}>Are you sure you want to continue?</p>
        <DialogActionsBar>
        <Button className="k-button" onClick={toggleVisible}>No</Button>
        <Button className="k-button" onClick={toggleVisible}>Yes</Button>
        </DialogActionsBar>
      </Dialog>}
      </div>
    );

Again we have just updated our code in the `return()` to not reference the `this` keyword and to use our new function name `toggleVisible`.

These are all the changes that need to be made. We have successfully converted our KendoReact demo to use a functional component and the basic `useState` hook. Let's take a look at what our overall changes looked like using and awesome tool called GitHistory:

![](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/class-vs-functional-animation.gif?sfvrsn=8a9c864d_0)

What I have done here is downloaded the original StackBlitz class based demo into its own Git repo. The class-based version would be the initial commit and then I made a second commit after refactoring to the functional hook style that we made. GitHistory gives me the ability to scrub through those commits and see in an animated way how our `main.jsx` file has changed over those two commits. I think it's a powerful visual for someone learning how to use hooks and seeing the change from the old class-based approach to the function based approach.

I have also pushed [this repo to my GitHub](https://github.com/httpJunkie/kendoreact-dialog-to-hooks-demo) account where you can [view it with GitHistory](https://github.githistory.xyz/httpJunkie/kendoreact-dialog-to-hooks-demo/blob/master/src/app/main.jsx) on your own. [GitHistory](https://github.com/pomber/git-history)(created by [Rodrigo Pombo](https://github.com/pomber)) is a very cool plugin that allows you to diff any file in your repo and scrub through the commits and see how over time the file has changed in a very visual way.

This is a great place to stop, we learned what it takes to convert a class component with a simple state object into a functional component using a hook, in our next part of this blog series we will take a deeper dive into setting up several KendoReact components which have more basic hooks and some advanced hooks like `useReducer` and take our hooks skills a little further.