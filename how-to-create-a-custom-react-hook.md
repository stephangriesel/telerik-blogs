---
published: false
title: How to Create a Custom React Hook
summary: With the release of React 16.8 now behind us, and learning about basic hooks out of the way, lets tackle building a custom hook on our own from scratch.
keywords: JavaScript, React, Custom Hooks, Functions
---

Hooks are just functions! Anything that is a function can become a hook. The React team has put lots of information out on how to work with basic and advanced hooks, as well with how to create them yourself. I have been covering the topic for several months and I want to bring everything I know about them together to focus on one topic now. Creating your own custom hook that you can easily share with others and can serve as a template or inspiration for any other custom hooks you decide to create in the future.

If you have not read up on hooks, below is some required reading material as well as the articles I have written on the subject as a series. It may be easier to breeze through these articles before we get into custom hooks. I recommend understanding the React Hooks API first, then figuring out how you can create your own hooks, which I cover very simply in this article.

### ReactJS.org Documentation

[React Conf Recap](https://reactjs.org/blog/2018/11/13/react-conf-recap.html)
[React v16.8: The One With Hooks](https://reactjs.org/blog/2019/02/06/react-v16.8.0.html)
[Introducing Hooks](https://reactjs.org/docs/hooks-intro.html)
[API Reference](https://reactjs.org/docs/react-api.html#hooks)

### My Basic Hooks Articles

[Basic React Hooks for State and Effects](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects)
[Basic React Hooks for Context](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context)
[Basic React Hooks for Reducers](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-reducers)


## Let's Understand The Basic Hook

I learned while reading up on Hooks on the ReactJS.org docs that there are two ways of using `useEffect`. You can use it [without cleanup](https://reactjs.org/docs/hooks-effect.html#effects-without-cleanup) or [with cleanup](https://reactjs.org/docs/hooks-effect.html#effects-with-cleanup). These are terms I expect anyone at this stage of working with hooks to either know or to take a few minutes to understand with the links provided.

Side effects, in classes went in one of many lifecycle methods like:
`componentDidMount`, `componentDidUpdate`. In cases where we had sometimes duplicated code in both of those methods(perform same effect for mounting updating) we can now do this type of thing inside a functional component and we can do it with one method called `useEffect`. 

By using `useEffect`, we tell React that your component needs to do something after render. It runs both after the first render and after every update. In my previous articles I only talked about side effects without cleanup, so we need to start our learning today understanding how to allow a functional component to have a side effect with cleanup. I want to make the example they provide on the ReactJS.org site inside StackBlitz as they do not supply one in the ReactJS docs. I think that in order to understand how to create our own Hook, we need to stay close to these examples of using `useEffect`.

To create a create custom Hooks, we need to understand what deep down hooks are providing for us and what they help us hook into. The idea is that they can hook into anything that is a regular function.


