---
published: false
title: How to Use Basic React Hooks for Reducers
description: A future release of React introduces an important new feature. React Hooks. Get "hooked" on React as we take a look at the useReducer React Hook!
keywords: Guide, JavaScript, React, React Hooks, Tutorial 
---

# How to Use Basic React Hooks for Reducers

In the past few articles, we have become familiar with React Hooks. In our first articel, we learned about [State & Effect](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects) which allows us access to local state and side effects inside a functional component.

In our second article we learned about [React's Context API](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context) demonstrating on a profile component using the Context API to share data with child components, we refactored that code to use the hooks. This involved refactoring classes in our project to functional components and by the time we were done we had not a single class left in our project.

In both cases we learned how to do things that normally are done with class components, but with hooks we can now do the same work inside of functional components.

We continue that journey today taking what we have learned from the first article and we will apply that knowledge to a more advanced hook called `useReducer`. Understanding the basic `useState` hook can prepare us for learning about `useReducer` so if you have not read the first article of this series it is highly encouraged.

# Your Only Job Was to Manage State in Your Application

It is many developers opinion, that the main thing you should always be considering when building a React application is just a few things. Understanding what your state currently looks like and understanding what does my UI look like.

We seperate these things in a proper React application, so they are easy to keep compartmentalized. This means we can typically just build out or UI and then we simply focus on managing it's state. This is first priority. This determines what we do next and we get to decide exxactly what happenes each time the UI is intereacted with and how that might mutate the state.

# Before We Jump Straight In

Let's talk about the difference between a Redux state reducer and the JavaScript method [Array.prototype.reducer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce). 

The array prototype at it's most simplest operates on an array, returning a single value based on all values in the array that get summed up to produce and return a single value (total). As well the reducer can be fed with an initial value to start at. Let's briefly take a look at some code that demonstrates the reduce method from JavaScripts `Array.prototype` method called `reduce()`.

```
const votesByDistrict = [250, 515, 333, 410];
const reducer = (accumulator, currentValue) => {
  return accumulator + currentValue;
}

console.log(votesByDistrict.reduce(reducer));
// expected output: 1508

// and below we simply add a value to start from:

console.log(votesByDistrict.reduce(reducer, 777));
// expected output: 2285
```

Now if you have worked with Redux reducers, you definitely will see the similarity. You can draw paralells and understand why the Redux Reducer shares a similar name. If you really get advanced with reducers, you can do a whole lot in between the curly braces and the work that goes on in between those curly braces is the reduction. Think of it as a recipe that you pass into reduce that is pure and always produces the same result considering the same input.

The Redux Reducer, similar to the Arrays reducer, returns the accumulation of something, in our case 'state' based on all previous and current actions and state modifications that have taken place in the past.

So Redux style reducers act as a reducer of state. It receives a `state` and `action`. The state gets reduced (accumulated) based on the action type and then returned as the new state. This is just one cycle of the reduce function.

### Let's Build a Working Example

We are going to build a Todo application. To start out with, we want our TODO list to have an initial value that simply says:  "Get Started". 

![](https://i.imgur.com/Sz7XNmS.png)

When we add a new Todo we want to dispatch a new todo item it should get merged with any existing state and the reducer should then return a new state that includes all Todos.

The way we add a new TODO is to setup a reducer to handle the action of type `ADD_TODO`. This will be a simple reducer that takes the payload we send and adds a new Todo to the list using the text we type into the form field.

Another action could be `COMPLETE_TODO`. In this case our reducer doesn't add any new items to the list, it modifes one property of an exisitng Todo item. So let's pick up where we left off above, we had added a new Todo item, giving us two of them now. Our state now looks like this:

```
{ 
  id: 1, 
  name: 'Get started', 
  complete: false 
},
{ 
  id: 2, 
  name: 'Take a break', 
  complete: false 
}
```

Notice that each Todo has several properties, one of them, an `id` can be used to know which Todo we want to update. The reducers job for `TOGGLE_TODO` is simply to update one of our items `complete` property value from it's current boolean value to the opposite. If each Todo starts out as `completed: false` Then if we call `TOGGLE_TODO` on one of our existing Todo's our returned state should now show the oppostie for that particular Todo:

```
{ 
  id: 1, 
  name: 'Get started', 
  complete: true 
},
{ 
  id: 2, 
  name: 'Take a break', 
  complete: false 
}
```

You will have reducers that act on all types of state. When we want to change any part of our applications state, we dispatch an action that gets handled by a reducer and returns us back the new state. Once state is updated, all subscribers to that state get notified and can then update accordingly. This entire cycle is referred to as a one-way (unidirectional) data flow.

This was not easily achievable in React without a library like Redux. But now, thanks to the advent of Hooks, we can easily implement the Redux reducer pattern in React core.

# Using React Hooks for Reducers

With React Hooks, we can access and manage state and it's side effects by using the [Basic React Hooks(useState & useEffect)](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects) and if we throw into the mix an advanced hook in `useReducer` and you got youself a party inside and around functional components that before hooks, just wasn't possible to do with React core on it's own.

## The State We Will be Managing

Traditionally in Redux, a decision on how to categorize state and where to store it was one of the biggest questions concerning Redux from a beginners persepctive. It's actually the [first question in their Redux FAQ](https://redux.js.org/faq/organizing-state#do-i-have-to-put-all-my-state-into-redux-should-i-ever-use-react-s-setstate):

It's complicated, There is no “right” answer. Some prefer to keep all data in Redux, maintaining a fully serializable and controlled version of an app. Others prefer non-critical or UI state to be maintianed in internal component state. Hooks are powerful in the layer of the application where we keep track of things like “is dropdown open” and "is menu closed". We can take care of proper management of the UI data in a Redux style manner without leaving React core.

It feels like the React team had a lot of time to study the landscape around state management and pull .

In a machine that it's sole responsibility to constantly change and append state, the reducer is the part that is different about each operation. It's the logic that either increments a counter or manages a complex object that changes to have ramifications on the current state. Giving us access to that as well as setState from within functional components is the final piece of the puzzle and at the same time the first piece to a new puzzle.

Let's take a look at how we manage the very simple todo type application. But it's a perfect example for demonstration purposes. Here are the rules of our TODO app.

We are going to need a few mvoing pieces in order to contrive even a simple real world case for using useReducer. We will need to keep track of how our state is modified and updated using actions like "add", "complete" and "clear". Using a pattern familliar to Redux we typically would associate each of these processes with a particular action type that is handled by a dispatcher:

 - A form field allowing us to enter a task
 - A dispatcher handling our form when it submits
 - An actual object that holds the our tasks
 - An actual Task Component to encompass everything
 - An actual Reducer that handles the modifying of our state

Let's start by adding and composing all of these pieces together.

[Install React with Create React App]()

[Install React without Create React App]()

We can start with the `index.js`, our application root lives in this file and it's the base of most React applications.

To keep our example simple, we will have the Todo component that we create be the actual root level component of our application:

```import React from 'react';
import { render } from 'react-dom';
import './style.css';

const Todo = () => {
  return (
    <>
      Todo Goes Here
    </>
  );
}

render(<Todo />, document.getElementById('root'));
```

I suggest forking this [StackBlitz Demo](https://stackblitz.com/edit/todos-usereducer-hook-start) and giving it a new name, this way you can follow along with the tutorial.  Just yhit the fork button on the StackBlitz demo and give it a new name, this will create a clone of my starting point to work on.

![](https://i.imgur.com/Nyelqcq.gif)


We will first need to import `useReducer` from React. 

```
import React, { useReducer } from 'react';
```

Next we will add as the first line of our functional Todo component the actual `useReducer` function. It takes `state` and `action` as arguments. It returns the state and  also takes some initial state. What we are going to do is destructure the `useReducer()` functions return value as a tuple contianing `items` and `dispatch`. The items will be the list of todo items, so we can also just go ahead and create an unordered list and map a list item out for each item in the list.

```const Todo = () => {
  const [items, dispatch] = useReducer(
    (state, action) => state,[]
  );
  return (
    <ul>
      {items.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```

So not everything is working yet, specifically because we have initialized our items as an empty array. If you were to update the code above and put a few task objects into that empty array you would then see some items populating our list:

![](https://i.imgur.com/qrFvyIp.gif)

Next we need an input that will allow us to enter a task. We don't want to stor it's value in state, so we will use the ref attribute to get a reference to the input, this will allow us to access it's value later. This reference will be backed by a local property in our Todo functional component but we that will just be a call to the `useRef` hook which allows us to access all of the ref goodness inside a functional component. With a local property named `inputRef` we will be able to make calls like: `inputRef.value`.

Any form element if we want to be able to process it's contents on a submit, needs a submit handler. We get this by wrapping the `<input ..>` with a `<form>...</form>` and adding an event handler `onSubmit(handleSubmit)` which will call a function named `handleSubmit()`. this function will take an event and we wil `preventDefault()` to ensure the page does not refresh on us. As well, this is where we are going to call dispatch. Our dispatch payload will be an object with a `type` and `name`.

So we have all of that worked out:

```
const Todo = () => {
  const inputRef = useRef();
  const [items, dispatch] = useReducer(
    (state, action) => state, []
  );

  function handleSubmit (event) {
    event.preventDefault();
    dispatch({
      type: 'ADD_TODO',
      name: inputRef.current.value
    })
    inputRef.current.value = '';
  }
  return (
    <>
      <form onSubmit={handleSubmit}>
        <input ref={inputRef} />
      </form>
      <ul>
        {items.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    </>
  );
}
```

Now our function is getting kind of beefy, but that's ok, we are achieiving a lot here and it's all related to this functional component. At this point if we were to enter a value into our field and hit enter, we would only really be calling preventDefault and clearing the form field value. We are missing a crucial step which is handled inside the `useReducer()` function.

Inside our `useReducer` function we need to create a switch statement on `action.type`. This will allow use to handle mutliple operations on the Todo list.

If you noticed the dispatch call in the code above, we have specified that `onSubmit()` calls the add `action.type` but we will also be calling from a clear button or maybe something else. The switch statement is the best construct in JavaScript for demonstration purposes. Let's add that now, we are working only with the `useReducer` function:

```const [items, dispatch] = useReducer(
    (state, action) => {
      switch (action.type) {
        case 'ADD_TODO': 
        return [...state, {id: state.length, name: action.name}]
      }
    }, []
  );
```

Now if we actually type in a value and hit enter, the `onSubmit` handler is fired eventually processing an `ADD_TODO` action type. It's name was used to update the list with our first generated Todo item. Nice, but we still have a few more opportunities now. We can add a "clear" and "complete" task option.

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