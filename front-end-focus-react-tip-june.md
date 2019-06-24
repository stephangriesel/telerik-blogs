---
published: false
title: Front-end Focus Tip June
summary: Draft for Front-end Focus article tip section for our sponsorship in June.
keywords: Guide, JavaScript, React, Layout, Tutorial 
---

I recently spoke at a React conference in Chicago and I got a lot of questions about how I was conditionally controlling parts of my application based on the current breakpoint and doing things like hiding or showing menus depending on a small vs medium breakpoint.

![](https://imgur.com/zzE28c0.gif)

Luckily I have already written about the topic on the [Telerik Blog](https://www.telerik.com/blogs/creating-a-responsive-layout-in-react), but I figured I could provide a bite sized tip for this weeks newsletter.

The code for this application is on GitHub ([httpJunkie/react-loop-demo](https://github.com/httpJunkie/react-loop-demo)).

To explain this fucntionality we will start with a [cutom React Hook built by Lessmess](https://github.com/lessmess-dev) called [react-media-hook](https://github.com/lessmess-dev/react-media-hook) which uses the [matchMedia API](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia) under the hood. We can install this React Hook for media queries in any project by running `npm i react-media-hook`.

I have done so and imported it at the top level of my applicaiton in my `App.js` file (parent to all other components in my app). The import looks like:  

```import { useMediaPredicate } from 'react-media-hook';```  

If you are familliar with responsive media queries, you will feel comfortable with the way this React Hook allows you to define a variable that will track if our browser width is at minimum 600 pixels or more.

```let isMediumPlus = useMediaPredicate("(min-width: 600px)") ? false : true;```  

This local variable can be used in a few different ways. We could pass it into a component as a prop for use within that component and any time the value changes, the prop will update causing the child component to re-render. This way anything inside the child component that uses this value will get updated when the browser width changes from 599 pixels to 600 pixels.

In my application I have chosen a different approach. I have a class called `app-container` which sits on a `div` at the outer most level of my application. I use a ternary statement to render an additional class of `small` or `medium`.

If we go inside of my `Sidenav.css` in the `partial-components` directory, we will see that our sidenav will hide or show itself based on the `app-container` class having `small` or `medium` as a second class.

```
.app-container.small .sidenav {
  display: auto;
}
.app-container.medium .sidenav {
  display: none;
}
```

In conjunction with this concept I also use Hooks with React's Context API in a file called `AppContext.js`. Here I keep track of local React state called `navOpen`. This allows me to let my entire application know if my sidenav is open or closed at any given point in time. As well the ability to flip that value through an update method called `toggleSidenav`.

If we go back to the `App.js` file we can see that we wrap our entire application with an `<AppProvider></AppProvider>` tag.

This gives us the ability in any component (like `Sidenav.js`) to import our `AppContext`:  

`import { AppContext } from "../AppContext";`  

And then easily use that value using `context.navOpen`:

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

My `Menu.js` component, also consumes this context but also has a button that calls the update method:

```
<FontAwesomeIcon icon="bars" className="hoverable" onClick={() => {
  context.toggleSidenav(!context.navOpen)
}} />
```

Together these two concepts work in conjunction to hide and show the `Sidenav` and `Topnav` components based on breakpoints, but also to open or close the `Sidenav` using the menu icon. I hope that this handy tip helps you to build a more responsive application using React Hooks and the Context API. Both are very powerful concepts fairly new to React.
