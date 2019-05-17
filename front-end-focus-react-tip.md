---
published: false
title: Front-end Focus Tip
summary: Draft for Front-end Focus article tip section for our sponsorship.
keywords: Guide, JavaScript, React, Hooks, Tutorial 
---

Hooks are a new feature of React that allow you to manage state.
Each slice of state that you want to manage can easily be created using React's new `useState()` method.
The most typical way of working with this method is to save it's return value using array desctructuring.

Because the `setState()` return value is a stateful value, and a function to update it, without array destructuring, we would have to write JavaScript like the following, in order to work with `useState()`.

```
const countState = useState(0);
const count = countState[0];
const setCount = countState[1];
```

This is obvioulsy verbose and we are creating a variable called `countState` that is unecessarry. The React team definitely would not reccomend this way of working with the `useState()` method either. 

Instead we can use array destructuring to save both of those variables we want (`count`, `setCount`) and instead we can write something like this:

```
const [count, setCount] = useState(0);
```

This is great, we have learned something new about React in that we now know how to instantiate state in a component using `useState()` one of the most common and basic of the new React Hooks methods. But we have also touched on array destructuring which allows you to create multiple variables using an array assignment which assigns each of our variables in the array depending on the return value of the `useState()` method. Two birds, one stone.

Let's finish learning about the Hook though. Now that I have a place to store my state (`count`) and a method to update it (which uses `setState()` under the hood), we can imagine how a button might be used to update this state. 

We will need two more things to completely understand further. A function that will use our `setCount()` method and tell it how to update the `count` state each time we call it (simply adding one to the previous value).

```
const incrementCount = () => setCount(count + 1);
``` 

And finally, a button in our JSX that will call that function everytime the user clicks it as well as a display for the count on the screen:

```
return (
  <div>
    <p>You clicked {count} times</p>
    <button onClick={incrementCount}>Click Me</button>
  </div>
)
```

And that's it. We learned about the new [React Hooks useState](https://reactjs.org/docs/hooks-reference.html#usestate) as well a little bit about [array destructuring](https://kentcdodds.com/blog/react-hooks-array-destructuring-fundamentals). As well, I have prepared a [StackBlitz Demo](https://reactjs.org/docs/hooks-reference.html#usestate) with everything working in case you want a live working example to play with.