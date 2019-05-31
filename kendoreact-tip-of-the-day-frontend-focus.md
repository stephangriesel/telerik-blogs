# Tip of The Day

One of my favorite things about React Hooks is the ease of which you can use state within functional components. This tip starts with understanding the concept of a Basic React Hook and moves on to show how to use custom hooks in your own code. 

Shareability of code is one reason React Hooks are becoming very popular and that concept is illustrated in a  [StackBlitz](https://stackblitz.com) demo at the end of this brief tutorial. Here is a preview of that demo:

![](https://i.imgur.com/etEIlNo.gif)

Before we get into that demo and its basics, let's briefly cover the `useState()` React Hook because I want you to understand the most fundamental way to use a React Hook before diving into that demo.

## Part One, Basic React Hooks

Let's say that we need to have a piece of state in one of our components that tracks a value representing a stock price over time to be displayed on the screen. As well, we need our component to re-render and update that price on the screen when it's value changes. A contrived example of that component may look like this:

```
const StockPrice = () => {
  const [price, setPrice] = useState(188.22);
  return (
    <p>Current stock price is {price}</p>
  )
}
```

What happens here on the second line, is the creation of a state variable named `price` and assignment of a default value: `188.22`. As well we have a variable named `setPrice` that is actually a method used to update the state associated with it: `price`.

We also display the stock price on the screen by placing its variable name within curly braces inside the render function.

If you are familiar with React's `state` object, the code I have shown you above is equivalent to the following code that you would write if you used a class component:

```
class Counter extends React.Component {
  state = { price: 188.22 };
  render() {
    return (
      <p>Current stock price is {this.state.price}</p>
    );
  }
}
```

One thing I will note is that the definition of the `price` and `setPrice` are done using [array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment). This works because the call to `useState()` returns two things:  
1. A basic value (in our case a number) assigned to the first variable called `price`.  
2. A function (method) assigned to the second variable called `setPrice` used to update the `price`  

Once we have the `price` variable and `setPrice` update method setup, we can create a function that can be reused over and over in our component to call the `setPrice` method and update our state:

```
const updatePrice = (newPrice) => setPrice(newPrice);
```

We now have everything we need to set, update and re-render our stock price using React Hooks. If we put all this together we can easily set, update and display state in a functional component with just a few lines of code very clearly and concisely. 

```
const StockPrice = () => {
  const [price, setPrice] = useState(188.22);
  const updatePrice = (newPrice) => setPrice(newPrice);
  return (
    <>
      <p>Current stock price is {price}</p>
      <button onClick={() => updatePrice(188.55)}>Update Price</button>
    </>
  )
}
```

Here it that same code running in a [StackBlitz demo](https://stackblitz.com/edit/react-tip-price-hook?file=StockPrice.js) that you can play with.

## Part Two, Custom React Hooks

So now that we have a basic idea of how Hooks work in a React functional component, let's take that knowledge and apply it to using a hook that was written by someone else. Let's imagine we have an application and inside that application, we have a `<Menu />` component that takes a prop called `vertical`. If passed a value that is truthy, it will render our component vertical otherwise horizontal. That component at it's most basic looks like this:

```
import { Menu } from '@progress/kendo-react-layout';

const MenuWrapper = () => {
  return (
    <Menu items={items} vertical={true} />
  );
}
```

Where items is a `json` list containing the text and hierarchy of menu buttons, However; in our app, we need to render this component either vertically or horizontally based on the screen being above or below `415px` which is the value that we have determined to not be a mobile device once exceeded. We can use a custom hook for this called `useMediaPredicate` that we can import from a library called **react-media-hook**.

Outside of the React component shown above, we can determine if a breakpoint has been exceeded or not using this React Hook. like so:

```
import { useMediaPredicate } from 'react-media-hook';
import MenuWrapper from './MenuWrapper';

const App = () => {
  const isMediumPlus = useMediaPredicate('(min-width: 415px)');
  return (
    <MenuWrapper isMediumPlus={isMediumPlus} />
  );
}
```

What we have done here is use someone else's custom React Hook. If we visit their GitHub page, we can see the [actual implementation details](https://github.com/streamich/use-media/blob/master/src/index.ts) used to power this custom React Hook. Once we have determined that this is safe and exactly what we want, we can use their [nicely packaged hook](https://github.com/streamich/react-use-media), which allows us to very simply *import* their custom hook, and use it declaratively in our own functional components. This is amazingly powerful and illustrates beyond using built-in React Hooks, how we can share code with other developers and use that code in a very clear and concise way.

I hope you like this tip, maybe you even learned something new today. If you would like to see this demo with a little bit more context, check out this [this StackBlitz demo](https://stackblitz.com/edit/react-layout-hello-world-4-z8t9sk?file=app/main.js) I have put together specifically for the FrontEndFocus "Tip of The Day". It has some additional responsive behavior you might find useful and some additional stying not shown above in our code samples, but I think you will find it extremely easy to navigate and play around with!

My name is Eric Bishard, I am the developer advocate for the [KendoReact](https://www.KendoReact.com) team and if you have any questions about this tip or just want to learn more about our component library, hit me up on Twitter [@httpJunkie](https://twitter.com/httpJunkie)!