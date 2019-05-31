One of my favorite things about React Hooks is the ease of which you can now use state within your functional components. You can find some great examples on [ReactJS.org](https://reactjs.org/docs/hooks-intro.html) as well as I have some great articles covering the basics on the [Telerik Blog](https://www.telerik.com/blogs/author/eric-bishard).

My tip starts with understanding the concept of a basic React Hook, and moves on to show how to use someone elses hooks in your own code. Sharability of code is one reason React Hooks are becoming veryy popular. A final [StackBlitz](https://stackblitz.com) demo will demonstrate how to use that custom hook to pass either `true` or `false` to a prop in a [KendoReact]() component rendering it horizontal or vertical based on the browser width using a specified CSS media query that you don't even have to write. Here is a preview of it:

![](https://i.imgur.com/etEIlNo.gif)

We are only going to cover the code needed to flip the value we pass to the KendoReact Menu component. But the demo will contain more code and features so that you have a fully working example in React.

First let's briefly cover `useState()` because I want you to understand the most fundamental way to use a hook. Let's say that we need to have a piece of state in one of our components that simply keeps track of a value, and when that value changes over time, we need our component to re-render and update a piece of text n the screen that shows the curent state of that value.

```
const StockPrice = () => {
  const [price, setPrice] = useState(188.22);
  return (
    <p>Current stock price is {price}</p>
  )
}
```

What's happening on the second line, is that we are setting up a state variable named `price`. It will get a default value that I have hard coded to `188.22`. As well we have another value called `setPrice` that can be used to update the state known as `price`. Recognize the correlation between the two and the naming convention and we will come back to it in a moment.

We also need to display the stock price on the screen by placing it within curly braces somewhere inside the render function like so: `{price}`. This is how any value in React is displayed.

If you are familiar with React's `state` object, the code above is equivelant to the following code used in a class component:

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

Now let's create a function that we can use to call that update method :

```
const updatePrice = (newPrice) => setPrice(newPrice);
```

We now have everything we need to set and update our stock price and we are well on our way to understanding te basics of how to use a basic React Hook. One thing I will note is that the defintion of the `price` and `setPrice` are done using [array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment). This works because the call to `useState()` returns two things, a basic value (in our case a number) assigned to the first variable called `price` and a function assigned to the second variable called `setPrice`.

That is the basics of how to use state in a React functional component, if we put all this together we can easily set, update and display state in a functional component with just a few lines of code. Very clear and concise. Here it is all together and you can optionally run the code below in a [StackBlitz demo](https://stackblitz.com/edit/react-tip-price-hook?file=StockPrice.js) to see it working:

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

So now that we have a basic idea of how Hooks work in a React functional component, let's take that knowledge and apply it to using a hook that was written by someone else. Let's imagine we have an application and inside that application we have a `<Menu />` component that takes a prop called `vertical`. If passed a value that is truthy, it will render our component vertical otherwise horizontal. That component at it's most basic looks like this:

```
import { Menu } from '@progress/kendo-react-layout';

const MenuWrapper = () => {
  return (
    <Menu items={items} vertical={true} />
  );
}
```

Where items is a `json` list containing the text and hierarchy of menu buttons, However; in our app we need to render this component either vertically or horizontally based on the screen being above or below `415px` which is the value that we have determined to not be a mobile device once exceeded. We can use a custom hook for this called `useMediaPredicate` that we can import form a library called **react-media-hook**.

Outside of the React component shown above we can determine if a breakpoint has been exceeded or not using this React Hook. like so:

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

What we have done here is use someone elses custom React Hook, not a built in React Hook. If we visit their GitHub page, we can see the [actual implementation details of how that hook is built](https://github.com/streamich/use-media/blob/master/src/index.ts) and once we have determined that this is safe and exactly what we want, we can use their [nicely packaged hook](https://github.com/streamich/react-use-media), which allows us to simply import the hook, pass it a string which determines the media query and we minimize the code that needs to be written inside of our actual functional component. This is amazingly powerful and illustrates beyond using built in React Hooks, how we can share code with other developers and use that code in a very clear and concise way.

I hope you like this tip, maybe you even learned something new today. If you would like to see this demo with a little bit more context, check out this [this StackBlitz demo](https://stackblitz.com/edit/react-layout-hello-world-4-z8t9sk?file=app/main.js) I have put together specifically for the FrontEndFocus "Tip of The Day". It has some additional responsive behavior you might find useful and some additional stying not shown above in our code samples, but I think you will find it extremely easy to navigate and play around with!

My name is Eric Bishard, I am the developer advocate for the KendoReact team and if you have any questions about this tip or just want to learn more about our component library, hit me up on Twitter [@httpJunkie](https://twitter.com/httpJunkie)! Thanks...