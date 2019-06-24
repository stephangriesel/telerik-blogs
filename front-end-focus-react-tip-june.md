---
published: false
title: Front-end Focus Tip June
summary: Draft for Front-end Focus article tip section for our sponsorship in June.
keywords: Guide, JavaScript, React, Layout, Tutorial 
---

I recently spoke at a React conference in Chicago. I got a lot of questions about how I was controlling my Sidenav and Topnav based on breakpoints and manually clicking on the menu icon and how to make them work together as you see below.

![](https://imgur.com/zzE28c0.gif)

I have already written about the topic on the [Telerik Blog](https://www.telerik.com/blogs/creating-a-responsive-layout-in-react), as well I have taken the idea even further in the demo that I am using in my talks which can be found on GitHub at [httpJunkie/react-loop-demo](https://github.com/httpJunkie/react-loop-demo).

To explain this functionality we start with a [cutom React Hook built by Lessmess](https://github.com/lessmess-dev) called [react-media-hook](https://github.com/lessmess-dev/react-media-hook) which uses the [matchMedia API](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia) under the hood. We install this media query hook in our project by running `npm i react-media-hook`.

In my app, I import this hook at the top level of my `App.js` file (parent to all other components). 

```import { useMediaPredicate } from 'react-media-hook';```  

If you are familiar with responsive media queries, you will feel comfortable with the way this Hook allows you to define a variable and track if our browser width is at minimum 600 pixels or more.

```let isMediumPlus = useMediaPredicate("(min-width: 600px)") ? false : true;```  

This local variable can be used in a few different ways. We could pass it into a component as a prop and any time the value changes, the child component will re-render when the browser crosses the 599 to 600 pixel threshold.

In my app, I have chosen a different approach. I have a class called `app-container` which sits on a `div` at the outer most level of my application. I use a ternary statement to render an additional class of `small` or `medium`.

If we go inside of my `Sidenav.css` in the `partial-components` directory, we will see that our `Sidenav` will hide or show itself based on the `app-container` class having `small` or `medium` as a second class.

```
.app-container.small .sidenav {
  display: auto;
}
.app-container.medium .sidenav {
  display: none;
}
```

In conjunction with this concept, I also use Hooks with [React's Context API](https://reactjs.org/docs/context.html) in a file called `AppContext.js`. Here I keep track of a local React state called `navOpen`. Allowing my entire application at any time to know if my `Sidenav` is open or closed along with access to a method called `toggleSidenav` to change/flip that value.

In `App.js`, we can see that we wrap our entire application with an `<AppProvider></AppProvider>` tag. This gives us the ability in any component (like `Sidenav.js`) to import our `AppContext`:  

`import { AppContext } from "../AppContext";`  

And then easily use that value: `context.navOpen`, below is an example of how we do that:

```
const SideNav = () => {
  const context = useContext(AppContext);
  return (
    <div className={'sidenav ' + (context.navOpen ? 'show' : 'hide')}>
      <Menu />
    </div>
  )
}
```

My `Menu.js` component also consumes this same context but also has a button that calls the update method:

```
<FontAwesomeIcon icon="bars" className="hoverable" onClick={() => {
  context.toggleSidenav(!context.navOpen)
}} />
```

Together these two concepts work in conjunction to hide and show the `Sidenav` and `Topnav` components based on breakpoints, but also to open or close the `Sidenav` using the menu icon. I hope that this handy tip helps you to build a more responsive application using React Hooks and the Context API. Both are very powerful concepts fairly new to React.