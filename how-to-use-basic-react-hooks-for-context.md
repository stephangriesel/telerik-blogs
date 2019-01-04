---
title: How to Use Basic React Hooks for Context
summary: A future release of React introduces an important new feature. React Hooks. Get "hooked" on React as we take a look at the useContext React Hook!
keywords: Guide, JavaScript, React, React Hooks, Tutorial 
---

With React Conf 2018 behind us, we have learned that the 16.7 release of React introduces an important new feature: React Hooks. Get "hooked" on React as we take a look at the useContext React Hook!

# The Third Basic Hook: Context

We started this series talking about the two most commonly used and easily learned [React Hooks](https://reactjs.org/docs/hooks-intro.html) and you can see that blog post here: [How to Use Basic React Hooks for State and Effects](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects). We explored the React JS Docs [Proposal](https://reactjs.org/docs/hooks-intro.html) for Hooks and provided some [StackBlitz demos](https://dev.to/httpjunkie/basic-react-hooks-586m) that you follow along with and fork each demo we talk about. Understanding how state and effects work is not the whole story, in fact, it will take more than two blog posts to cover Hooks well. We still have one more basic hook to learn about before fully covering the basics.

After reading this article, you should be comfortable with being able to share data between functional components in your application by using various basic hooks and `setState`. This is a gateway into being able to do more state management in a pattern similar to what you know in Flux and Redux but without importing another library. We can do it with React core. But first we need to understand Context in React.

## Using React Hooks for Context

To understand the third basic React Hook `useContext,` we first need to have a good understanding of the Context API, a stable feature since [React 16.3](https://reactjs.org/blog/2018/03/29/react-v-16-3.html). Like learning most things, sometimes we have to fully understand another concept before moving forward. If you're familiar with Context API, you can skip to the [`useContext` section](#useContext). However, if Context API is new to you, we'll go over it briefly and show some demos before we moving on to using Context with Hooks. You cannot `useContext` without first having a Context being provided in your application. I'd also like to show you a StackBlitz demo that will serve as a starting point for the code we will work with. It picks up where we left off with exploring state and effects.

A good example for using Context is a profile component. Think about some of the information that might be displayed on a profile. When I'm logged into xyz.com, I have a cloud of data that needs to be available to all or some of a profile component's child components. We can assume this profile component needs two components: `<user>` and `<team>`. One of these two components will display my user name and image, the other will display my team—at my company, we have people on a React, Angular and Vue team, so we could use the frameworks as team names. Back to the code, we can pass the data needed (as an object) into a `<provider>` component through it's `value` attribute. We could let any component and its child components share this data.

Let's take a look at how to approach this component by simply passing props through components, which is definitely an option in the pre-Context API era. We propagate our data down through each component in the component tree "prop drilling." Inputs into each component allow passing and passing on state from the outside world through to every single component and it's child components.

![Prop Drilling visual](https://i.imgur.com/hTOdcL1.gif)

Let's see a code demo of this pre-context era example.

<iframe width="100%" height="400" src="https://stackblitz.com/edit/profile-no-context-api?file=index.js&amp;view=editor&amp;ctl=1"></iframe>

If an application has 10 components, each of which have their own tree of components that in turn have their own tree of components, would you rather manually pass props around to components that may or may not need the data? Or would you rather just consume that data from any point within a component tree? Context allows this sharing of values between components without having to explicitly pass a prop through every level of the tree. Let's try to visualize how the Context API by itself can be applied to class-based components:

![Context API visual](https://i.imgur.com/QeAuK4k.gif)

Let's also see a working example of that in StackBlitz!

<iframe width="100%" height="400" src="https://stackblitz.com/edit/profile-with-context-api?file=index.js&amp;view=editor&amp;ctl=1"></iframe>

## A Primer on Context API

So as the last part of understanding the basic React Hooks, we simply need to understand this: Just how we were able to access state using [useState](https://reactjs.org/docs/hooks-state.html) and just how we were able to access a alternative life-cycle pattern with [useEffect](https://reactjs.org/docs/hooks-effect.html). We now need to be able to consume a provider using a hook called [useContext](https://reactjs.org/docs/hooks-reference.html#usecontext).

In the Context API demo above we definitely saw a way to share data through many components. But it involved one pattern that always felt a bit clunky to me and really did not help in minimizing the amount of code we needed to write. Going from our simple prop drilling example to a much more maintainable Context API example, we ended up with some code that, while it is a better solution to our problem, really clutters up our components. Let's look at what I'm talking about:

![Context API code example](https://i.imgur.com/VcmZ4vg.gif)

Each and every place I want to consume the context, I have to wrap these `ProfileContext.Consumer` tags around the DOM elements that I want to consume that provider. It would be nice to just create a `const` in that functional component with a hook to use the Profile Context. These consumer containers have always looked weird to me. Hooks can make this better.

![useContext code example](https://i.imgur.com/ShawwTQ.gif)

This is already much nicer to look at. It doesn't feel clunky—in fact, it makes me feel like we actually made the code more readable. This is one example of how Hooks will change the way that we write normal, everyday components.

This calls for an updated StackBlitz example. Let's see our Profile component now using Hooks. Not much to explain—if you remember, when we hooked into state using `useState,` we had a tuple of values that we needed to understand. One was the actual state and the other, a method to update the state. With `useEffect,` there are some tricks you need to understand to do things like cleanup and the fact that it replaces multiple life-cycle methods. So the first two hooks are very involved with several moving parts. With `useContext,` we just point it at an existing context and that property now holds a reference to that context. It's that simple.

<iframe width="100%" height="400" src="https://stackblitz.com/edit/profile-usecontext?file=index.js&amp;view=editor&amp;ctl=1"></iframe>

## Look Ma, No Provider

In the demo above, we are introduced to `useContext` and since we are only reading the data inside of the context, we have passed the object/data directly into the `createContext()` method. This is completely valid and we don't have to wrap the `<Provider>` component around the profile component. This is not how I want to leave it though—I actually do want to create that provider, because in order to be able to change the `team`, I need to create a Provider. But I wanted to show that if you are passing in some data and not accessing any functions like we want to do, you can set it up without a provider.

We will revert back to using a provider, because in some cases, we will need to have the ability to update some part of that context's state. For instance, I want to be able to change the Team that our user is affiliated with.

For this scenario, we will again create a `<Provider>` and not just passing in a default context state like we did above

## Updating State Within a Provider

I want to revisit our Context API example and update it to be able to use `setState` to update one of our properties. We should be able to update the Team value by calling a function that we will put inside our state as a key value pair.

<iframe width="100%" height="400" src="https://stackblitz.com/edit/profile-with-context-api-setstate?file=index.js&amp;view=editor&amp;ctl=1"></iframe>

Let's ensure that the user can initiate a change in Team simply by pressing a button with the name of the team you would like to switch to. We want the change to happen from within the User component, but we also want the buttons to show up at the bottom of the Profile view.

![updated profile visual with buttons](https://i.imgur.com/TX4lnVJ.gif)

With the addition of the buttons, we will need each one to handle a click and pass the proper team framework type to the function, which will take an argument ie. name of team: Vue, Angular or React.

![example code for buttons](https://i.imgur.com/vhecIhX.gif)

We will need a function that can handle changing the state, we will make a new property on our state named `toggleTeam`, it's value will be the actual function which calls `setState`. We will call this method through the context.

![State with added function to change team](https://i.imgur.com/PGl9csI.gif)

Now we can change the Team value as well as read from the context. This pattern does both the setup and subscribing for us.

![change team buttons visually working example](https://i.imgur.com/gXSRe7B.gif)

I have provided another StackBlitz demo that enhances the original Context API example. Remember, this code below is not using Hooks, we will see next how to do that.

<iframe width="100%" height="400" src="https://stackblitz.com/edit/profile-with-context-api-setstate?file=index.js&amp;view=editor&amp;ctl=1"></iframe>

Next, we will look at another example. This one has a similar setup for the buttons and their handler to change Teams. In fact, there is no difference between the button syntax and the state object in this Hooks version. A big benefit of using hooks is that we can omit the usage of `<ProfileContext.Consumer>` tags wrapped around everything that we want to be able to consume. It added unwelcomed HTML in our component. We simply crate a const in each functional component:

`const context = useContext(ProfileContext);`

And we just call the context and it's methods as we did before.

<iframe width="100%" height="400" src="https://stackblitz.com/edit/profile-usecontext-setstate?file=index.js&amp;view=editor&amp;ctl=1"></iframe>

I'd like to show you one more example that takes our current profile component and refactors the Change Team buttons into their own component and converts the Context API Provider to be functional and it's `this.state` to implement `useState` instead. Like I noted in the last example, we also got rid of the `<ProfileContext.Consumer>` tags and now everywhere we are accessing context via `useContext`. All of our components are now functional as well.

<iframe width="100%" height="400" src="https://stackblitz.com/edit/profile-usecontext-setstate-no-classes?file=index.js&amp;view=editor&amp;ctl=1"></iframe>  

## Wrap Up

I hope that these interactive examples allow you to understand the basics of using React Hooks for Context. If you are new to React, we have more content here on the Telerik blog specifically around [All Things React](https://www.telerik.com/blogs/all-things-react), which contains a plethora of information about React and its ecosystem. Please explore our articles and products and let me know if you have any questions or ideas for articles on subjects relating to React.

Thanks for taking the time to read about React Hooks—below is additional information around the topic that you can find online!

## Early Documentation and Articles on Hooks:

[React Docs on Hooks](https://reactjs.org/docs/hooks-intro.html)  
[Making Sense of React Hooks](https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889)  
[Understanding Hooks in React a Deep Dive](https://blog.bitsrc.io/understanding-hooks-in-react-a-deep-dive-d5d5dc88ecd9)  
[A Simple Intor into Hooks](https://daveceddia.com/intro-to-hooks/)  
[React 16.7 Hooks Tutorial](https://www.techiediaries.com/react-hooks/)  
[Hooked (Formiddable)](https://formidable.com/blog/2018/hooked-facebook-react/)  
[Flux Without Fuss: From Containers to Hooks](https://medium.com/iqoqo-engineering/flux-without-the-fuss-from-containers-to-hooks-bda35c622e3f)

## Video Resources on Hooks

[React Conf 2018 Day One Talks](https://www.youtube.com/watch?v=kz3nVya45uQ)   
[Share Complex Logic across React Components with Custom Hooks](https://egghead.io/lessons/react-share-complex-logic-across-react-components-with-custom-hooks)   
[Access and Modify a DOM Node with the React useRef and useEffect Hooks](https://egghead.io/lessons/react-access-and-modify-a-dom-node-with-the-react-useref-and-useeffect-hooks)   
[Share Logic Across Multiple React Components with Custom Hooks](https://egghead.io/lessons/react-share-logic-across-multiple-react-components-with-custom-hooks)   
[Use the useState React Hook](https://egghead.io/lessons/react-use-the-usestate-react-hook) [Test React Components that use React Hooks](https://egghead.io/lessons/react-test-react-components-that-use-react-hooks)   
[React Hooks a Complete Introduction](https://www.youtube.com/watch?v=jd8R0a2Ur8Q)   
[TODO List with Hooks](https://www.youtube.com/watch?v=cAZ-fOd1RpA)