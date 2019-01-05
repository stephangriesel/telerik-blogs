---
published: true
title: How to Use Basic React Hooks for State and Effects
summary: With React Conf 2018 behind us, we have learned that with release 16.7 of React, an important new feature will be available: React Hooks. Join me as we go through working examples and get "hooked" on React.
keywords: JavaScript, React, React Hooks, State Management 
---

We are watching React slowly become more opinionated, and with the latest features, I would dare to say it's becoming more like a framework than ever before. React has typically been known to be less of a fully featured framework and more of a library that lets you render DOM and manage its state really well. The ecosystem has a few tools that are opinionated and still widely used as standard in a lot of React apps, like Redux for instance. Now Hooks are not Redux, but they are an alternative way of doing things for those who recently found Redux, which builds on the Flux pattern as a requirement for every application to mange state.

I believe that Hooks are a bridge to Redux but also a way of managing simple state without introducing Redux. It makes total sense that Dan Abramov was the one who showed us our first working example at React Conf 2018 as he is also the creator and [main contributor to Redux](https://github.com/reduxjs/redux/graphs/contributors). I think this lends credibility in some way towards the use of Hooks and indicates they are thinking about how to bring better state management into React core, and how to also ensure that Hooks will compliment and make use with Redux a priority.

With the introduction of things like code splitting, suspense, lazy, memo and now hooks, I think that the changes we have seen in 2018 are done with the developer and performance in mind. Competition with other frameworks is also becoming a reality. This competitive environment I believe is what is forcing React to become more of a lightweight framework. And if we are going to see a more opinionated React with framework-like features, I'm really happy about how the React team is going about these latest additions to the API. I asked a few people if they thought React was becoming a framework, a few said yes, one person just sighed, and another said, until they make the router part of React, I don't consider it a framework.

## Hooks for the Win

With [React Conf 2018](https://conf.reactjs.org/) behind us, we have learned that with release 16.7, a new feature will be available: [React Hooks](https://reactjs.org/docs/hooks-intro.html).

Currently you can read about the [Hooks](https://reactjs.org/docs/hooks-intro.html), view the [RFC (Request for Comments)](https://github.com/reactjs/rfcs/pull/68) and play around with the new feature using: `npm install react@next react-dom@next`. Hooks represent a strictly additive feature to [React](https://reactjs.org/) that introduces [no breaking changes](https://reactjs.org/docs/hooks-intro.html#no-breaking-changes), meaning it's completely opt-in. It provides an alternative to writing class based components simply to use state and access life-cycle methods.

Because Hooks will be implemented with a [gradual adoption strategy](https://reactjs.org/docs/hooks-intro.html#gradual-adoption-strategy) (living side-by-side with existing code), it gives teams time to refactor their code or simply leave the legacy code alone as they introduce new functional components using Hooks. Hooks have already been dubbed: "The Future of React," but it is also noted that classes will be supported for the foreseeable future. Hooks bring to functional components the things we once were only able to do with classes. Like being able to work with [state](https://reactjs.org/docs/hooks-state.html), [effects](https://reactjs.org/docs/hooks-effect.html) and context specifically.

In the past, some React developers have experienced confusion around when to use and when not to use classes. [@SophieBits](https://twitter.com/SophieBits) commented in the ["React Today and Tomorrow"](https://www.youtube.com/watch?v=V-QO-KO90iQ) talk that classes can be "[hard for humans and machines as well](https://reactjs.org/docs/hooks-intro.html#classes-confuse-both-people-and-machines)." I think we will see more of this move away from classes whenever possible. It's actually the right thing to do in some cases - the stance on this goes back years with talks like: ["How to Sleep at Night using React Classes,"](https://medium.com/@dan_abramov/how-to-use-classes-and-sleep-at-night-9af8de78ccb4) even though we must sometimes use them in the current React. But that issue is being handled now and we already see developers having strong opinions and using mostly functional components when and where they can.

Hooks give functional components the upper hand in React. Some of the additional Hooks already [available in the React API (16.7.0-alpha)](https://reactjs.org/docs/hooks-reference.html) include: useReducer, useCallback, useMemo, useRef, useImperativeMethods, useMutationEffect, useLayoutEffect, uhh did I get them all? Just driving the point home, this is useful stuff!

## So What are Hooks, How do We Use Them?

The easiest way to describe Hooks is to simply show you two examples, one being a class component that needs to have access to state and life-cycle methods and another example where we achieve the same thing with a functional component. I have read through the proposal for Hooks and for this reason I will use a similar code sample that Dan Abramov uses in the docs.

You could just read the docs, and I suggest doing so. However, I wanted to provide you with a working example that you can touch and feel and play around with. I learn best by getting my hands dirty. For this reason I wanted to provide the same examples illustrated in the docs, but with a [StackBlitz](https://stackblitz.com/) demo for each stage so that you can test it out for yourself.

This GIF below shows the difference between the Class and Functional Component example we will see in the next section:

![Functional vs Class](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/reactstatehook-04n054a108f6e739248898fad28d2ed3da9c6.gif?sfvrsn=137e3710_1 "State and Effect (Hooks)")

### Side-by-Side Example of `useState`

Below we follow the canonical counter example provided in the React docs. It contains a button inside of a `Counter` component. Once clicked, it advances the state by one and updates the `state.count` for rendering purposes.

First we see how to do this with a class based component using just `setState` :

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-state-hook-01?file=Counter.js&amp;view=editor&amp;ctl=1"></iframe>

The first thing to notice about the class-based component is that the class syntax uses a constructor that references the `this` keyword. Inside the constructor we have a state property. We also update the count using `setState()`.

Now, lets see how to do the same thing with Hooks, using a functional component:

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-state-hook-02?file=Counter.js&amp;view=editor&amp;ctl=1"></iframe>

In the functional component example we have an additional import of `useState`. There's no more class syntax or constructor, just a `const`. Its assignment sets the default and provides not only the `count` property, but a function for modifying that state called `setCount`. This `setCount` refers to a function and can be named whatever you like.

The functional component `incrementCount` method is easier to read, and references our state value directly instead of referencing `this.state`.

### Side-by-Side Example of `useEffect`

When updating state, we sometimes have side effects that need to happen along with each change. In our example of the counter, we may need to update the database, make a change to local storage or simply update the document title. In the docs, the React team chose the latter example to make things as simple to understand as possible. So let's do just that and update our examples to have a side effect that uses the new Hook `useEffect`.

Let's add this side effect to our existing counter example and again look at the old way of doing this with Classes vs working with Hooks. We will first see how to do this with a basic class-based component:

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-state-hook-04?file=Counter.js&amp;view=editor&amp;ctl=1"></iframe>

And next how to do the same thing with Hooks:

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-state-hook-05?file=Counter.js&amp;view=editor&amp;ctl=1"></iframe>

Now that we are introducing additional behavior, we start to see even more evidence of how switching to Hooks provides a cleaner way of dealing with state and side effects. What took two separate life-cycle methods in the class component we can achieve with just one call to `useEffect`. We do have one more import on the functional component example, but if we can get rid of the class syntax, an additional life-cycle method and make our code cleaner and more readable, it's totally worth it.

## Call `useState` and `useEffect` as Much as You Want!

Just like with `setState`, you can call `useState` as many times as you want. Let's switch to an example that shows a slightly more involved situation where we have a name we are displaying on the page, some inputs that allow for the name to be changed, and we want control over both the first name and the last name. We can create two separate properties, each with their own update or set function, and simply call `useState` on each in order to set the default.

In the GIF below, you can see what this would look like - as well as what it looks like with a class-based version, which we'll dig into a little more below.

![Functional vs Class](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/reactstatehook-06n07.gif?sfvrsn=18e0cae0_1 "State and Effects (Hooks)")

As you would expect we also have an update function for each name so that you can handle changes to them independently.

Let's see the code for the class-based component:

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-state-hook-06?file=Greeting.js&amp;view=editor&amp;ctl=1"></iframe>

And now the same thing with Hooks:

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-state-hook-07?file=Greeting.js&amp;view=editor&amp;ctl=1"></iframe>

I won't go over all the differences again, but I wanted you to see a slightly more complex example side-by-side. Hopefully you are starting to see the benefit of using Hooks.

Let's make one more change to this example and use `useEffect` to save our name to local storage so that we don't lose our state when we refresh the page.

Let's see the code for the class-based component:

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-state-hook-08?file=Greeting.js&amp;view=editor&amp;ctl=1"></iframe>

And now the same thing with Hooks:

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-state-hook-09?file=Greeting.js&amp;view=editor&amp;ctl=1"></iframe>

## Wrap Up

I hope that these interactive examples allow you to understand the basics of `setState` and `useEffect`. I plan to release more articles on the subject of React Hooks as well how to use them with our [KendoReact native React components](https://www.telerik.com/kendo-react-ui/). If you are new to React, we have more content here on the Telerik blog specifically around [All Things React](https://www.telerik.com/blogs/all-things-react), which contains a plethora of information about React and its ecosystem. Please explore our articles and products and let me know if you have any questions or ideas for articles on subjects relating to React.

Thanks for taking the time to read about React Hooks - below is additional information around the topic that you can find online!

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
[Use the useState React Hook](https://egghead.io/lessons/react-use-the-usestate-react-hook) [Test React Components that use React Hooks](https://egghead.io/lessons/react-test-react-components-that-use-react-hooks)  
[React Hooks a Complete Introduction](https://www.youtube.com/watch?v=jd8R0a2Ur8Q)  
[TODO List with Hooks](https://www.youtube.com/watch?v=cAZ-fOd1RpA)