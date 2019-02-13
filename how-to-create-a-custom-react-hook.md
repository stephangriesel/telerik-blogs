---
published: false
title: How to Create a Custom React Hook
summary: With the release of React 16.8 now behind us, and learning about basic hooks out of the way, lets tackle building a custom hook on our own from scratch.
keywords: JavaScript, React, Custom Hooks, Functions
---

Hooks are just functions! Anything that is a function can become a hook. The React team has put lots of information out on how to work with basic and advanced hooks, as well with how to create them yourself. I have been covering the topic for several months and I want to bring everything I know about them together to focus on one topic now. Creating your own custom hook that you can easily share with others and can serve as a template or inspiration for any other custom hooks you decide to create in the future.

If you have not read up on hooks, the end of this article has what I believe to be required reading, as well a few articles I have written on the subject. It may be easier to breeze through these articles before we get into custom hooks. I recommend understanding the React Hooks API first, then figuring out how you can create your own hooks, which I cover very simply in this article.

### ReactJS.org Documentation

[React Conf Recap](https://reactjs.org/blog/2018/11/13/react-conf-recap.html)  
[React v16.8: The One With Hooks](https://reactjs.org/blog/2019/02/06/react-v16.8.0.html)  
[Introducing Hooks](https://reactjs.org/docs/hooks-intro.html)  
[API Reference](https://reactjs.org/docs/react-api.html#hooks)  

### My Basic Hooks Articles

[Basic React Hooks for State and Effects](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects)  
[Basic React Hooks for Context](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context)  
[Basic React Hooks for Reducers](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-reducers)  


## Let's Revisit The Basic Hook

If you feel that you have sufficient knowledge of basic Hooks, you can [skip directly to creating a custom Hook](#create-a-custom-hook-of-our-own).

I learned while reading up on Hooks on the [ReactJS.org docs](https://reactjs.org/docs) that there are two ways of using `useEffect`. You can use it [without cleanup](https://reactjs.org/docs/hooks-effect.html#effects-without-cleanup) or [with cleanup](https://reactjs.org/docs/hooks-effect.html#effects-with-cleanup). These are terms I expect anyone at this stage of working with hooks to either know or to take a few minutes to understand with the links provided.

Side effects, in classes went in one of many lifecycle methods like: `componentDidMount` or `componentDidUpdate`. In cases where we had sometimes duplicated code in both of those methods(perform same effect for mounting and updating) we can now do these things inside a functional component and we can do it with one method called `useEffect`. 

By using `useEffect`, we tell React that your component needs to do something after the component renders. It runs both after the first render and after every update. In my previous articles I only talked about side effects without cleanup, so we need to start our learning today understanding how to allow a functional component to have a side effect with cleanup. I think that in order to understand how to create our own Hook, we need to completely understand `useEffect`.

Like I said, some effects do not need cleanup, they are simple, like the ones we have already learned, like updating the document title.

```
useEffect(() => {
  document.title = `You clicked ${count} times`;
});
```

If you return a function from `useEffect`, you can optionally do some cleanup. A situation where you subscribe to something may need to run an unsubscribe as part of the effects cleanup. React performs this cleanup on unmount. 

```
useEffect(() => {
  console.log("Subscribe to Something);

  return function cleanup() {
    console.log("Unsubscribe to Something);
  };
});
```

The effect above will run on every render more than one time. React cleans up effects from the previous render before running the effects of the next render. For an explanation on [why Hooks run on each update](https://reactjs.org/docs/hooks-effect.html#explanation-why-effects-run-on-each-update), in the ReactJS Docs. This behavior can be opted out of. 

We can also [optimize performance by skipping effects with an optional argument](https://reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects), for instance, maybe we don't want to run the subscribe/unsubscribe effect unless the user id has changed.

```
useEffect(() => {
  console.log("Subscribe to Something);

  return () => {
    console.log("Unsubscribe to Something);
  };
}, [props.something.id]); // re-subscribe only if props.something.id changes
```

I would also like to mention that if you have unrelated logic inside your `useEffect` try refactoring the unrelated code out into it's own `useEffect`. You can have as many `useEffect` calls as you would like. For instance, both of the `useEffect` calls above could be inside the same functional component.

Hooks allow splitting up code based on what it is doing rather than what lifecycle method it's in which creates a mixing of concerns. React applies each effect in the order they are specified.

I'm stating obvious rules for using Hooks I know. However if we want to understand when and why we would use a custom Hook, we need to understand these rules and ideas around Hooks. It will help us realize what code needs to go into a Hook and what code doesn't. Also we now kow that we can probably have multiple calls to multiple custom Hooks right alongside calls to `useEffect` after all, they are all just Hooks and as we said we can call as many as we like.

## More Important Rules About Hooks

Before we create our own Hook, let's review a few of the major rules we must always follow.

1. Never call Hooks from inside a loop, condition or nested function
2. Hooks should sit at the top level of your component
3. Only call Hooks from React functional components
4. Never call a Hook from a regular function
5. Hooks can call other Hooks

If you would like, you can enforce these rules in your team with an [ES Lint plugin](https://reactjs.org/docs/hooks-rules.html#eslint-plugin). Also on that same page [there are good explanations](https://reactjs.org/docs/hooks-rules.html#explanation) on why these rules are required. Feel free to read up on that, it's about a 5 minute read.

## Create a Custom Hook of Our Own

I really liked something that was tweeted out today.. "Hooks unleash a level of composition well above and beyond anything we've seen". What I would have you understand about Hooks is that all of the great changes that we have seen with Classes and how we have so many options for composition. It's all available in Hooks. This means that now our hands are not tied when it comes to the composition of functional components in React. And this is the biggest takeaway.

Custom Hooks are JavaScript functions whose name starts with `use` and that may call other Hooks. So a custom Hook is merely a normal function. By adding the word use to the beginning, it let's us know that this special function follows the rules of Hooks we stated in the section above.

I wen through all of this information above because I really wanted you to be best setup to understand when, where and how to use Hooks. Now we will do one final thing in this article. We will take what I know to be the simplest piece of logic that we already know about and create the simplest custom Hook I can think of.

If you remember, we had the example of how to update the document title using the `useEffect` Hook. Well, this seems like something we may want to do on several page or several components in our app. When some type of information changes we want to update the document title with some type of string. Pretty simple right. 

So we know that a Hook can call a Hook. And if that is true then our custom Hook can also call one of the React Core Basic Hooks, like `useEffect`. Do you see where I am going with this? Let's review a functional component that updates the document title one more time. The code below can also be seen in [this StackBlitz example](https://stackblitz.com/edit/react-state-hook-05?file=Counter.js).

```
import React, { Component, useState, useEffect } from 'react';
function Counter() {
  const [count, setCount] = useState(0);
  const incrementCount = () => setCount(count + 1);

  useEffect(() => {
    document.title = `You clicked ${count} times`
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={incrementCount}>Click me</button>
    </div>
  )
}

export default Counter;
```

So what we would like to do here is create a custom Hook that we pass a piece of text into and the Hook updates the document title for us. Let's first look just at the code required to create this custom Hook:

```
const useDocumentTitle = (title) => {
  useEffect(() => {
    document.title = title;
  }, [title])
}
```

Above you see that all we really need this Hook to take as an argument is some string of text, we call it `title`. Inside the Hook we call the `useEffect` Hook and set the title so long as the title has changed, our second argument to the `useEffect` method will perform that check before updating document title. You mean, creating a custom Hook is as easy as creating a function. And that function can reference any other Hook. Hot damn. Creating custom Hooks is easier than I thought.

Let's review what our overall functional component will now look like, you will see that I left the old call to `useEffect` commented out, above it is how we use the custom Hook for this instead. This can be viewed in an [updated StackBlitz demo](https://stackblitz.com/edit/react-custom-hook?file=Counter.js) as well:

```
import React, { Component, useState, useEffect } from 'react';

const useDocumentTitle = title => {
  useEffect(() => {
    document.title = title;
  }, [title])
}

function Counter() {
  const [count, setCount] = useState(0);
  const incrementCount = () => setCount(count + 1);

  useDocumentTitle(`You clicked ${count} times`);
  // useEffect(() => {
  //   document.title = `You clicked ${count} times`
  // });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={incrementCount}>Click me</button>
    </div>
  )
}

export default Counter;
```

Let's clean it up just a little bit more and see how we might use this hook if it were supplied by some npm package instead of being copy pasted at the top of our file. I will show the code below as well as link to an [updated StackBlitz demo](https://stackblitz.com/edit/react-custom-hook?file=Counter.js).

```
import React, { Component, useState } from 'react';
import useDocumentTitle from '@rehooks/document-title';

function Counter() {
  const [count, setCount] = useState(0);
  const incrementCount = () => setCount(count + 1);

  useDocumentTitle(`You clicked ${count} times`);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={incrementCount}>Click me</button>
    </div>
  )
}

export default Counter;
```

This is fabulous and notice that I don't have to import `useEffect` in my functional component, because the Hook that I imported from the npm package has that import, so if I don't need to `useEffect` in my functional component because the `useDocumentTitle` Hook does it for me, I can omit that and write less code. I hope this illustrates and you see the power in using and creating custom React Hooks.

Here are the two StackBlitz examples side by side if you want to fork them and play around!

1. [Extract a Custom Hook from Existing Code](https://stackblitz.com/edit/react-custom-hook?file=Counter.js)
2. [Import a Hook From NPM or Co-located File](https://stackblitz.com/edit/react-custom-hook-npm?file=Counter.js)

Big thanks to [Amit Solanki](https://github.com/iamsolankiamit) who made this [document title Hook](https://github.com/rehooks/document-title) available as an npm package. It's a great and simple example of how to create a React Hook at the most basic level and I couldn't think of a better first Hook to introduce you to in order to get you thinking about creating your own custom Hooks!
