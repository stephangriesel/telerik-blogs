---
published: true
title: How to Create a Custom React Hook
summary: With the release of React 16.8 now behind us, and learning about basic hooks out of the way, lets tackle building a custom hook on our own from scratch.
keywords: JavaScript, React, Custom Hooks, Functions
---

Let's learn what it takes to create a custom React Hook as well as all of the rules we must keep in mind about using Hooks.

Hooks are just functions! Anything that is a function can become a hook. The React documentation has lots of information out on how to work with both basic and advanced hooks. The documentation also has information on creating custom Hooks. I myself, have been covering the topic for several months and want to bring everything I know about Hooks to focus on one topic. Creating a custom hook that can be easily shared with others and can serve as a template or inspiration for creating other custom Hooks. I feel that the documentation on the [ReactJS](https://reactjs.org) site is exhaustive on the subject, but my concern is the lack of a very simple example.

I'm taking a roundabout way of getting to this example at the end of this blog post. This is because I want you to be prepared for creating custom hooks and the only way to do that is to review Hooks first. Although they are very similar to creating a basic function, there is more information that you need to know before creating custom Hooks yourself. If you have not read up on hooks, I have provided some articles to get you up to speed. These links get you acquainted with the React Hooks API, and I feel like that is a prerequisite to creating your own custom Hooks.

### ReactJS.org Documentation

*   [React Conf Recap](https://reactjs.org/blog/2018/11/13/react-conf-recap.html)
*   [React v16.8: The One With Hooks](https://reactjs.org/blog/2019/02/06/react-v16.8.0.html)
*   [Introducing Hooks](https://reactjs.org/docs/hooks-intro.html)
*   [API Reference](https://reactjs.org/docs/react-api.html#hooks)

### My Basic Hook Articles

*   [Basic React Hooks for State and Effects](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects)
*   [Basic React Hooks for Context](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context)
*   [Basic React Hooks for Reducers](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-reducers)

## Let's Revisit The Basic Hook

If you feel that you have sufficient knowledge of basic Hooks, you can skip directly to [creating custom Hooks](#create-a-custom-hook-of-your-own).

Without going through all of the basic Hooks again, I think we just need to revisit one of them: the `useEffect` Hook. I learned while reading up on Hooks on the [ReactJS.org docs](https://reactjs.org/docs) that there are two ways of using `useEffect`. You can use it [without cleanup](https://reactjs.org/docs/hooks-effect.html#effects-without-cleanup) or [with cleanup](https://reactjs.org/docs/hooks-effect.html#effects-with-cleanup). These are terms I expect anyone at this stage of working with hooks to either know or to take a few minutes to understand with the links I just provided.

With classes and before Hooks were available, side effects were placed in one of many lifecycle methods like: `componentDidMount` or `componentDidUpdate`. In cases where we have duplicated code in both of those methods (performing the same effect for mounting and updating) we can now do these things inside a functional component and we can do it with just one Hook. That's right, I'm talking about `useEffect`.

`useEffect` tells React that our component needs to do something after the component renders. It runs after the first render and after every update. In my previous articles I only talk about side effects WITHOUT cleanup, so I would like to cover really quick how to allow a functional component to have a side effect WITH cleanup.

Below is an example of how `useEffect` can run without any cleanup:

    useEffect(() => {
      document.title = `You clicked ${count} times`;
    });

If you do need cleanup to run, you can return a function from `useEffect`. This is optional, but allows you to run some code after your effect and before any new effect runs. A situation where you subscribe to something may need an unsubscribe as part of the effects cleanup process. React will perform this cleanup on unmount.

    useEffect(() => {
      console.log("Subscribe to Something);
      return function cleanup() {
        console.log("Unsubscribe to Something);
      };
    });

The effect above will run on every render more than one time. React cleans up effects from the previous render before running the effects of the next render, this should be noted. For an explanation on [why Hooks run on each update](https://reactjs.org/docs/hooks-effect.html#explanation-why-effects-run-on-each-update), check out the ReactJS Docs. Remember though, this behavior can be opted out of if it causes performance issues.

We can also [optimize performance by skipping effects with an optional argument](https://reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects). For instance, maybe we don't want to run the subscribe/unsubscribe effect unless some id has changed. Check out the example below to understand how this can be done, it's fairly simple!

    useEffect(() => {
      console.log("Subscribe to Something);
      return () => {
        console.log("Unsubscribe to Something);
      };
    }, [props.something.id]); // only if something.id changes

Hooks and specifically `useEffect` now allow you to split up code based on what it is doing rather than what lifecycle method it's in. When we only had classes and lifecycle methods, we would sometimes have to mix concerns. Now, using multiple `useEffect` methods, React can apply each effect in the order they are specified. This is a huge benefit for organizing code in your application.

## The Obvious Benefits of Using Hooks

Hooks have a lot of benefit to us as developers, and they are going to change the way we write components for the better. They already help us to write clearer and more concise code - it's like we went on a code diet and we lost a lot of weight and we look better and feel better. It brings out our jaw line and makes us feel lighter on our toes. It's the one change that actually works for us. Just look at what React Hooks have done for others!

![positive transformation](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/transformation.png?sfvrsn=e8caf499_1 "positive transformation")

All kidding aside, Hooks really does trim the fat. It cuts down and makes our code more readable, concise and clear. To demonstrate let's check out a class version of our canonical "document title effect" and see the difference between how we used to write something like this side by side with an example using an npm installed Hook that does the same thing.

The side-by-side below shows how the component has lost a little weight. We not only save about five lines of code in this simple example, but the readability and test-ability also improve with the change over to Hooks. Switching existing code over to Hooks could have a big impact on sheer volume of code and readability, but would encourage you to take it slow, remember that Hooks is backwards compatible with the code it's replacing and can live side by side with it, no need to rewrite the whole codebase immediately. Check out the StackBlitz demos for this code: [Before](https://stackblitz.com/edit/react-state-hook-04?file=Counter.js) and [After](https://stackblitz.com/edit/react-custom-hook-npm?file=Counter.js)

[![Before And After](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/beforeandafter.gif?sfvrsn=8a30f722_1 "Before And After Code")](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/beforeandafter.gif?sfvrsn=8a30f722_1)

## Five Important Rules for Hooks

Before we create our own Hook, let's review a few of the major rules we must always follow.

1.  Never call Hooks from inside a loop, condition or nested function
2.  Hooks should sit at the top level of your component
3.  Only call Hooks from React functional components
4.  Never call a Hook from a regular function
5.  Hooks can call other Hooks

If you would like, you can enforce these rules in your team with an [ES Lint plugin](https://reactjs.org/docs/hooks-rules.html#eslint-plugin). Also on that same page [there are good explanations](https://reactjs.org/docs/hooks-rules.html#explanation) on why these rules are required.

## Create a Custom Hook of Your Own

I really liked something that was tweeted out recently by [Adam Rackis](https://twitter.com/AdamRackis): "[Hooks unleash a level of composition well above and beyond anything we've seen](https://twitter.com/AdamRackis/status/1095408337498316805)." What I would have you understand about Hooks is that all of the great changes that we have seen with Classes and how we have so many options for composition, well that's all available in Hooks now. This means that now our hands are not tied when it comes to the composition of functional components in React. And this is a huge advancement for React developers.

Custom Hooks are JavaScript functions whose names are prefixed with the word `use`. A custom Hook is normal function but we hold them to a different standard. By adding the word `use` to the beginning, it lets us know that this function follows the rules of Hooks.

With a better understanding of Hooks, lets take what we know to be a simple piece of code, our document title update, and create a simple custom Hook.

It seems like something we may want to do on several pages or inside several different functional components in our app. When some type of information changes we want to update the document title with some type of string. Additionally, we don't want to repeat this logic inside every functional component. We will start by extracting this code into a Hook locally on the same page, and then see how the same hook can be imported into many components and co-located. Pretty simple right?

So we know that a Hook can call a Hook. And if that is true then our custom Hook can also call one of the React Core Basic Hooks, like `useEffect`. Let's review a functional component that updates the document title one more time. The code below can also be seen in [this StackBlitz example](https://stackblitz.com/edit/react-state-hook-05?file=Counter.js).

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

So what we would like to do here is create a custom Hook that we pass a piece of text into and the Hook updates the document title for us. Let's first look just at the code required to create this custom Hook:

    const useDocumentTitle = (title) => {
      useEffect(() => {
        document.title = title;
      }, [title])
    }

Above you see that all we really need this Hook to take as an argument is a string of text which we will call `title`. Inside the Hook we call React Core's basic `useEffect` Hook and set the title so long as the title has changed. The second argument to `useEffect` will perform that check for us and only update the title if its local state is different than what we are passing in. You mean, creating a custom Hook is as easy as creating a function? Yep, it's that easy at its core, and that function can reference any other Hook. Hot damn... Creating custom Hooks is easier than we thought!

Let's review what our overall functional component will now look like. You will see that I left the old call to `useEffect` commented out, above it is how we use the custom Hook for this instead. This can be viewed in an [updated StackBlitz demo](https://stackblitz.com/edit/react-custom-hook?file=Counter.js):

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

Let's clean it up just a little bit more and see how we might use this hook if it were supplied by some npm package instead of being copy pasted at the top of our file. I will show the code below as well as link to an [updated StackBlitz demo](https://stackblitz.com/edit/react-custom-hook?file=Counter.js).

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

This is fabulous, but I also want you to notice that I don't have to import `useEffect` in my functional component now, because that gets taken care of in the Hook we imported from `'@rehooks/document-title'`. So if I don't need `useEffect`, I can omit that from my component imports.

I hope this illustrates the very basics of creating a custom React Hook and that you see the power even with such a simple example.

Here are the two StackBlitz examples side by side if you want to fork them and play around!

1.  [Extract a Custom Hook from Existing Code](https://stackblitz.com/edit/react-custom-hook?file=Counter.js)
2.  [Import a Hook From NPM or Co-located File](https://stackblitz.com/edit/react-custom-hook-npm?file=Counter.js)

The easiest way to discover more React Hooks that you can either copy and paste into your code or npm install is to visit these GitHub related links:

*   [Copy Paste Popular React Hooks](https://reacthooks.surge.sh/)
*   [Awesome React Hooks](https://github.com/rehooks/awesome-react-hooks)
*   [Collection of React Hooks](https://github.com/nikgraf/react-hooks)

Big thanks to [Amit Solanki](https://github.com/iamsolankiamit) who made this [document title Hook](https://github.com/rehooks/document-title) available as an npm package as well as [Adam Rackis](https://twitter.com/AdamRackis) for contributing such a profound outlook on Hooks in a brilliant tweet that inspired me to write about the subject. The developer community has embraced Hooks and that cannot always be said about new features of a framework when they first are released.

The easiest way to discover more React Hooks that you can either copy and paste into your code or npm install is to visit these GitHub related links:

[Copy Paste Popular React Hooks](https://reacthooks.surge.sh/)  
[Awesome React Hooks](https://github.com/rehooks/awesome-react-hooks)  
[Collection of React Hooks](https://github.com/nikgraf/react-hooks)