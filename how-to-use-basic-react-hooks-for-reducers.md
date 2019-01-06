---
title: How to Use Basic React Hooks for Reducers
description: useReducer hook and a Primer on useRef
tags: React, Hooks, Reducers, References, JavaScript
---

# How to Use Basic React Hooks for Reducers

In the past few articles, we have become familiar with React Hooks. In our first article, we learned about [State & Effect](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects) which allows us access to local state and side effects inside a functional component.

In our second article we learned about React's [Context API](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context) and demonstrated how to use it with regualr classes in a profile component. The Context API allows us to share data with child components using a provider and consumer. But until Hooks came around this was not achievable with functional components. So we refactored that code to use the `useContext` hook. This involved refactoring classes in our project to functional components and after the refactor, we removed all classes from our demo making everything easier to read and less syntax.

In both cases we learned how to do things that normally are done with class components, but using hooks so that we could do the same work inside of functional components.

To reiterate what we elarned in the past, hooks can only be used inside functional components or other hooks. They don't work inside classes.

In this article, we take what we have learned and apply that knowledge to a more advanced demo using the `useReducer` hook. Understanding the basic `useState` hook can prepare us for learning about `useReducer` so if you have not read the first article of this series it is highly encouraged before moving on.

I want to also mention, that although React has a built in `useReducer` hook, that does things in a Redux type manner. There are also custom hooks out there like `useObservable` which will allow you to work with a more MobX style way of doing things. But today we will focus on `useReducer` because Redux is the more popular way of working with unuidrectional data in React and is encouraged by the React team hence a built in hook called `useReducer`.

# Your Only Job Was to Manage State in Your Application

It is many developers opinion, that the main thing you should always consider when building React applications, is to understand what your state currently looks like and understanding what does my UI look like.

We seperate these in a proper React application, so they are easy to keep compartmentalized. This means we can typically just build out or UI and then we simply focus on managing it's state. This determines what we do next and we get to decide exactly what happenes each time the UI is intereacted with and how that might mutate the state we are managing.

# A Primer on Reducers

Let's talk about the difference between a Redux state reducer and the JavaScript method [Array.prototype.reducer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce). 

The canonical array prototype example is a sum function. When we call the reducer on an array that contains only numbers, we can return a single value summing up all values in the array and returning the total as a single value. As well the reducer can be fed an initial value to start at. Let's briefly take a look at some code that demonstrates the reduce method from JavaScripts `Array.prototype` method called `reduce()`.

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

If you have worked with Redux reducers, you probably see a similarity in the example I jsut explained and how Redux reducers work. You can easily draw paralells to understand why the Redux Reducer shares a similar name.

A sum function is the most simplest example, but inside that reducer, you can do any work you wnat iteratively between those curly braces. Think of it as a recipe that no matter what the contents of the array, this function always produces the same result considering the same input. A pure function. This is a powerful concept especially when used to manage state for an application.

The Redux Reducer, similar to the Arrays reducer, returns the accumulation of something, in our case 'state' based on all previous and current actions and state modifications that have taken place in the past.

So Redux style reducers act as a reducer of state. It receives a `state` and `action`. The state gets reduced (accumulated) based on the action type and then returned as the new state. Each time we reduce we can refer to that operation as a single cycle.

Just like in cooking a Bordeaux style Bordelaise sauce, we start with many ingredients. Butter, shallots, veal, pepper and of course wine. All of these ingredients are combined together in a pan and simmered or (reduced) down. Repeated, given the same steps, using the same ingreditents, same amounts, same stove and same temperatures, we should yield the same result each time. A single wonderfully awesome sauce. Still wondering where they get the name reducer?

### Let's Build a Working Example

We are going to build a Todo application. To start out with, we want our Todo list to have an initial Todo item that simply says:  "Get Started". 

![](https://i.imgur.com/Sz7XNmS.png)

When we add a new Todo item, the process is to first dispatch an action.

This action get's handled by a Reducer function. Our action type is `ADD_TODO` and our reducer function switcehs on these types. When the reducer function notices type `ADD_TODO`, it acts on it by taking the old state spreading that existing state out and appending our new Todo item to the end, then returning the new state as the result.

Another action we might create could be `COMPLETE_TODO` or better yet, `TOGGLE_COMPLETE`. I like the latter as it gives us the ability to uncomplete so to speak if the user clicks the wrong Todo.

In this case our reducer doesn't add any new items to the list, it modifes one property of an exisitng Todo item. So let's pick up where we left off above, if we started out with one Todo that says "Get Started" and then we add a new Todo: "Take a break" our new state should look like this:

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

Notice that each Todo has several properties, one of them, an `id`. This is a unique key and we use it specifically to know which Todo we want to update.

The reducers job for `TOGGLE_COMPLETE` is to update that `complete` property from it's current value `false` to the opposite value `true`. Once this is done, any changes will be propogated down to any components that use this piece of state causing them to update. Our list can be thought about as the listener and once we add or complete or remove a todo, the list should immediately reflect those new changes.

So, since each `completed` property in our Todo starts out as `false`, if we call `TOGGLE_COMPLETED` on teh Todo witht he id of `1`, our state should get updated to look like the following:

```
{ 
  id: 1, 
  name: 'Get started', 
  complete: true // We changed it!
},
{ 
  id: 2, 
  name: 'Take a break', 
  complete: false 
}
```

We have described (albeit a simple example) of the entire Redux cycle also referred to as unidirectional data flow.

This was not easily achievable in React without a library like Redux. But now, thanks to the advent of Hooks, we can easily implement the Redux reducer pattern in any React application without using a library like Redux. 

I will admit that using state in this manner should probably be reserved for working with internal state and that this will not mean tha large applications where state is managed by Redux is now obsolete, this is not the case. But it gives React developers are clear and concise Redux style way of managing internal state right away without installing any depenedencies.

## The State We Will be Managing

Traditionally in Redux, a decision on how to categorize state and where to store it was one of the biggest questions concerning Redux from a beginners persepctive. It's actually the [first question in their Redux FAQ](https://redux.js.org/faq/organizing-state#do-i-have-to-put-all-my-state-into-redux-should-i-ever-use-react-s-setstate) and here is what they state:

> There is no “right” answer for this. Some users prefer to keep every single piece of data in Redux, to maintain a fully serializable and controlled version of their application at all times. Others prefer to keep non-critical or UI state, such as “is this dropdown currently open”, inside a component's internal state. 

Hooks are powerful in the layer of the application where we keep track of things like “is dropdown open” and "is menu closed". We can take care of proper management of the UI data in a Redux style manner without leaving React core.

In a machine that it's sole responsibility to constantly change and append state, the reducer is the part that is different about each operation. It's the logic that either increments a counter or manages a complex object that changes to have ramifications on the current state. Giving us access to that as well as setState from within functional components is the final piece of the puzzle and at the same time the first piece to a new puzzle.

Let's take a look at how we manage the very simple todo type application. But it's a perfect example for demonstration purposes. Here are the rules of our TODO app.

We are going to need a few mvoing pieces in order to contrive even a simple real world case for using useReducer. We will need to keep track of how our state is modified and updated using actions like "add", "complete" and "clear". Using a pattern familliar to Redux we typically would associate each of these processes with a particular action type that is handled by a dispatcher:

 - A form field allowing us to enter a task
 - A dispatcher handling our form when it submits
 - An actual object that holds the our tasks
 - An actual Task Component to encompass everything
 - An actual Reducer that handles the modifying of our state

Let's start by adding and composing all of these pieces together. I don't typically go over how to setup a React project because that can be done many ways, instead I like to give my users a StackBlitz demo that they can fork and work on along side the tutorial, once forked, this project is yours to do with as you want. You can use this information and this code however you want.

WHere we start is with a brand new project and for this tutorial we will do everything inside the `index.js` file. Once finished, you may want to make it a point to extract each piece of logic and all components out to their own files, this is a great excercise especially for beginners.

In our example simple, we will have the Todo component that we create be the actual root level component of our application, that would look something like the following:

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

But the code I want you to start out wiht is a little bit further along than that. I have added enough to get us started, so I have added a form and input field that does not yet submit. As well I have added a styled list, a chunk of json we can use as a seed for generating todo items to test that our list renders out and that the shape of our data conforms to our HTML.

You will need to fork this [StackBlitz Demo](https://stackblitz.com/edit/todos-usereducer-hook-start) to follow along with the tutorial.  There is a fork button on the StackBlitz demo and give it a new name, this will create a clone of my starting point to work on.

![](https://i.imgur.com/Nyelqcq.gif)


Now that we have the project forked, we will make our first change by importing the `useReducer` hook from React, update thie first line in the file as follows:

```
import React, { useReducer } from 'react';
```

We need to add our call to the `useReducer` now. It takes `state` and `action` as arguments. We assign that to an array object which is a tuple (two values) this is [destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) because the `useReducer()` matches this as it's return value:

Add the following line just above the return statement in the Todo component:

`const [todos, dispatch] = useReducer(todoReducer, initialState);`

`items` will be the piece of state which is the actual list of todo items, `dispatch` will be the actual reducer used to make changes to that list of items. In the `return` statement we create a group of divs for each item our `items` array.

Our application will now have errors because we have not yet created a function called `todoReducer`. Let's add that code right below  the line that we setup our `initialState` assignment on.

```
const todoReducer = (state, action) => {
  switch (action.type) {
    case 'ADD_TODO': {
      return (action.name.length)
        ? [...state, {
          id: state.length ? Math.max(...state.map(todo => todo.id)) + 1 : 0,
          name: action.name,
          complete: false
        }]
        : state;
    }
    default: {
      return state;
    };
  }
}
```

This may seem complex at first, maybe not. All it's doing is setting up a function that takes `state` and `action`. We then switch on that `action.type`. At first we will only have one action, but we want to setup a default catch all as well, this default will simply return the current state.

But if it catches a real `ADD_TODO` we will return the current state, spread out, with our payload appended on to the end. The tricky part is assigning the new ID, what we have done here is we have taken the existing list of todos and return the max id plus one, otherwise zero.


Since I have already setup an initialState, we are good to move onto the next step. We need to make sure that when typing in the input field, that when we hit enter, the value we have input get's sent off to a function that will do the reducing. 

So first let's replace the div with the classname `todo-input` with the following:

```
<div className="todo-input">
  <form onSubmit={addTodo}>
    <input ref={inputRef} type="search" id="add-todo" placeholder="Add Todo..." />
  </form>
</div>
```

What this does is it ensures that when we hit enter, that we send the form information off to a function called `addTodo()` we also reference the input using the `ref` attribute and give that element a reference value of `inputRef`. making these changes mean we need to now to two more things.
 
1) We need to create a property called `inputRef` which calls the `useRef` hook.
2) We need to create a function called `addTodo()`

Let's start with creating the `inputRef` property. At the top of your Todo component, add the following property:

`const inputRef = useRef();`

We will use the ref attribute to get a reference to the input, this will allow us to access it's value later. This reference will be backed by a local property in our Todo functional component but we that will just be a call to the `useRef` hook which allows us to access all of the ref goodness inside a functional component. With a local property named `inputRef` we will be able to make calls like: `inputRef.value`.

As well you will need to import that hook just like we did `useReducer`. Update the first line of the `index.js` file to reflect the following:

`import React, { useReducer, useRef } from 'react';`

Finally we need to create the `addTodo()` function that will use this reference and will be responsible for dispatching our action of type `ADD_TODO`. Just above the `return` add the following function:

```function addTodo(event) {
  event.preventDefault();
  dispatch({
    type: 'ADD_TODO',
    name: inputRef.current.value,
    complete: false
  });
    inputRef.current.value = '';
}
```

Inside of our function we are first calling preventDefault in order to keep the page from refreshing when we hit submit the form.

We then dispatch our `ADD_TODO` action using the `inputRef` to access the input value from the form. All todos initially get a completed of false. Finally we set the `inputRef` value to nothing. This clearss the input field. Good enough for a demo.

Finally, we have one more update we need to make before the `ADD_TODO` will work. Inside of our JSX we are still mapping over initialState. WE need to change that from:

`{initialState.map((todo) => (`

to:

`{todos.map((todo) => (`

Now we should have a working `useReducer` hook that is utilizing our `addTodo` function in orderr to dispatch our `action` to the `todoReducer`.

## Adding Completed Todos

Let's bring in a familliar hook from our first blog post `useEffect` I just want to make sure we have a working example of that hook inside this project as well, we will update the `document.title` everytime that we check off a todo we will display the count or number of completed todos in our list.

Just above our `addTodo()` function, let's add the logic for figuring out how many completed todos we have and we will need a `useEffect` method to update the `document.title` when it changes:

```
const completedTodos = todos.filter(todo => todo.complete);
useEffect(() => {
  // inputRef.current.focus();
  document.title = `You have ${completedTodos.length} items completed!`;
})
```

As well, we will need to bring in that hook:

`import React, { useReducer, useRef, useEffect } from 'react';`

We are not done yet, we now need to add a event that will call the function which will dispatch our `COMPLETED_TODO`. Add a onClick handler to our `div` with the className of `todo-name`.

```
<div className="todo-name" onClick={() => toggleComplete(todo.id)}>
  {todo.name}
</div>
```

Next we need a function to handle this click event, it's simple and only dispatches a simple id and the action type. Add this right below our `addTodo()` function:

```
function toggleComplete(id) {
  dispatch({ type: 'TOGGLE_COMPLETE', id });
}
```

Finally we add the case to our `todoReducer`:

```
case 'TOGGLE_COMPLETE': {
  return state.map((item) =>
    item.id === action.id
      ? { ...item, complete: !item.complete }
      : item
  )
}
```

I have also setup a style and we will add or remove that style based on if the todo has a completed value of true. Just below the `todos.map` code, lets' change the line of code that looks like this:

```
<div key={todo.id} alt={todo.id} className="column-item">
```

to this: 

```
<div className={`column-item ${todo.complete ? 'completed' : null}`}
  key={todo.id}>
```

We don't need that alt attribute anymore, so we removed it. That should do it, now when we simply click on our todos it will dispatch an action and set the completed value to true on that specific todo and now our filter will pick up on this by way of the `useEffect` method which in turn updates the `document.title`. We will also get our className `completed` applied and our completed todo will become opaque to represent a completed todo.

At this point we pretty much have everything working except for the delete functionality as well as the button that should clear all todos from the list. To round out our demo we will repeat what we have already learned in order to make these last to pieces of functionality work.

## Deleting a Todo

It should be pretty trivial at this point to hook (pun intended) up a delete and clear todos button. The styling and HTML have already been taken care of, so we just need to make them work.

Let's start by adding the onClick event for the close icon inside the todos HTML:

```
<div className="todo-delete" onClick={() => deleteTodo(todo.id)}>
  &times;
</div>
```

We'll add the function that will dispatch the action, these don't have to be their own function, we could dispatch right from the `onClick` or we could setup a similar switch statement to handle all of the dispatching, we can take whatever approach to this we want, I wanted to add them one by one for purposes of this demo.

Now we create a function that will handle the dispatch:

```
function deleteTodo(id) {
  dispatch({ type: 'DELETE_TODO', id });
}
```

And you guessed it, we now just need to add a case in our reducers switch statement to handle the reduction, this is where we actually remove a todo from the list and return the old state minus the deletion. We can do this easily because we have provided an `id`, in the same way we know which todo to complete by passing an `id`, we can also delete an item, we just need to ensure that it returns the new state. We can achieve this with the array filter prototype. 

```
case 'DELETE_TODO': {
  return state.filter((x) => x.id !== action.id);
}
```

## Clearing all Todos

For the clearing of todos, we actually don't need much, when the action get's distpatched for the `CLEAR_TODOS`, the only thing being passed is the actual action type, no payload, because once we get into the reducer, we are simply going to return an empty array. 

Here is the three different pieces of code you will need to make that happen.

Add an `onClick()` to the HTML button:
```
onClick={() => clearTodos()}
```

Add a function to handle the dispatch:
```
function clearTodos() {
  dispatch({ type: 'CLEAR_TODOS' });
}
```

And a case in our reducer function:
```
case 'CLEAR_TODOS': {
  return [];
}
```