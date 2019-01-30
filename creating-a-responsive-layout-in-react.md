---
published: true
title: Creating a Responsive layout in React
summary: In this article we learn how to setup a React application with Flexbox to make our layout responsive and a few npm packages to help with images and breakpoints, we also showcase the KendoReact Menu component and achieve some practical responsiveness!
keywords: Guide, JavaScript, React, Responsive, Tutorial 
---

In order to really move forward with any react application beyond just the individual component level, you need an outer layer that provides styles to help you layout your site, but contrary to what others would have you believe, it's not to hard to use some basic CSS and a few React Component packages to help us achieve some basic levels of responsiveness in an application.

Our goal will be to build a web page that changes at several breakpoints and changes the way we display our content on the page like the image below:

![](https://i.imgur.com/etEIlNo.gif)  

A lot of the time you will want the freedom of not being tied to a framework like Bootstrap or Material, you want to roll your own, but you also don't want to reinvent the wheel. In this tutorial we will use Flexbox, some basic media queries to create breakpoints determining how to render our layout.

I have a KendoReact Menu component that I know I want to use, it will need to switch between vertical and horizontal modes in order for me to use it the way that I envision. For mobile, I want my menu component to render horizontal (left to right) at the top of the page, like a top-nav menu bar, but on Tablet and desktop, I would like the menu to be vertical (top to bottom) along the left side of the page.

Initially, we will start with just one breakpoint and later in the tutorial add another. I'm going to start with an already setup StackBlitz demo, just so I don't have to go over any of the React setup. We want to focus just on building our application, not on setting it up. If you want to follow along by coding, you can fork this initial StackBlitz demo, otherwise just read along knowing that you can grab any StackBlitz example I provide throughout the course (there are four of them) to play with the code. Each StackBlitz demo will contain the end product of all of the steps we have talked about up until that point.

The demos have a few dependencies, [react-media-hook](https://github.com/streamich/react-use-media) which we use to track a single breakpoint. We use [react-responsive-image](https://github.com/mikefey/react-responsive-image) to render images using the picture tag at different resolutions. I will also be using the [KendoReact Menu](https://www.telerik.com/kendo-react-ui/components/layout/menu/) as mentioned before it has a horizontal and vertical mode that we can switch when we hit our small to medium breakpoint.

Take a look at the StackBlitz demo below, we can talk about what's going on next.

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-layout-hello-world-1?file=main.js&amp;view=editor&amp;ctl=1"></iframe>  

## The Starting Point for Our Tutorial

So with this first example in StackBlitz, we already have a lot of stuff going on. We are using a kendo-theme for the Menu, this is normal if you plan on working with the suite of components, but just understand that it will only style any KendoReact components that we add and nothing else. We also have a `custom.css` file which is exactly what it says, custom styles. For now we just have some global styles for our app container, a `.navbar` and `.main` style will be used specifically for navigation and our main content. Finally we have a `site-container` class that will act as a Flexbox container and set direction for it's items inside of it. With this concept in Flexbox we will create basic layout that we can easily change depending on breakpoints that we setup later.

If you are new to Flexbox, I suggest [A Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/), an article from CSS Tricks to explain the basics of Flexbox. Otherwise continue on!

Let's start with the `main.js` file. This file's main purpose is to load the App shell or App component, a functional component named `App`.

If we then focus our attention to the render method of the `App` component, we will see that we have a very basic layout of two div's encapsulated in a container div. This setup is so that we can take advantage of Flexbox for the main layout.

With Flexbox we can have a container div and two divs inside of it. The container class needs a few class rules telling it to display it's inner contents as Flexbox. We will specify that the direction will be `column`.

    .container {
      display: flex;
      flex-direction: column;
    }

Think of 2 boxes stacked on top of each other, if they are perfectly square, they would continue stacking and making a longer column as you add more. The items will be laid one on top of the other (stacked like a column).

![](https://i.imgur.com/NKRf9Xp.png)

We will apply this pattern to our example, but we only want two container items, one will be our top navigation and we will restrict it's height, the other will be our content area.

![](https://i.imgur.com/s8bTMlb.png)

With the navigation bar at the top and a content area at the bottom. This layout here is pretty easty to achieve with Flexbox and zero media queries.

But I would like my navbar to go from being a top bar to a side bar when I hit a specific width (415 pixels), this is not a standard or anything, but I feel that most devices that hit this number or higher are not a mobile phone. The bigger deal is to get a few breakpoints setup so you can test your layout, the breakpoints can always be tweaked.

In order to see a change when we hit 415 pixels, we need to activate a media query. this is done by meeting it's requirements. Take the following CSS:

    @media screen and (min-width: 415px){
      .site-container {
        flex-direction: row;
      }
    }

It's one line of CSS, but it switches our Flexbox container to display it's contents in a row format, let's see what this looks like now..

![](https://i.imgur.com/gETn0MG.png)

Not exactly what we wanted, but we are already getting somewhere, by changing the direction of our flex-direction to row, we are now displaying the items within the container side by side, which is the effect I was going for. But I want the left menu column to only be 120 pixels wide and the main content area that just says "Hello World", we want that to take up the rest of the browser width.

Luckily with Flexbox this is super simple. We can add the following code to the media query and these rules will take effect once we hit that breakpoint at 415 pixels.

    .site-container > * {
      flex: 1;
    }

That `flex: 1` is a bit confusing, I know. I actually recommend some reading on this part of Flexbox because, it's not super intuitive by just seeing this line of code, you see, `flex: 1` is actually shorthand for `flex: 1 1 0` which is what I am going to use so that the rule is as descriptive as possible.

A brief explanation of the `flex` property, is that when you say `flex: 1;`  
or `flex: 1 1 0;` you are setting the following properties:

`flex-grow: 1;`   Grow in same proportion as the window-size

`flex-shrink : 1;`   Shrink in same proportion as the window-size

`flex-basis : 0;`   If 2 divs are present, each div will take 50%.

I will also start adding the `webkit-flex` css prefixes for different browsers into the StackBlitz demos for good measure. I show them below once, but in the rest of the examples in this article, I will omit them for brevity.

    .site-container > * {
      -webkit-flex: 1 1 0;
      -ms-flex: 1 1 0;
      flex: 1 1 0;
    }

Now that we have our main content div taking up as much space as it can, if we just add a few properties like width and height to the navbar div, we will constrain it and our main content div will be forced to make up the difference. We can add the following CSS to the media query:

    .navbar {
      padding-top: 0.75em;
      max-width: 120px;
      min-height: 100vh;
    }

This is great, Based off of a media query, we made our two sections layout in a different flex direction, but our KendoReact MenuWrapper component needs a copy of the current media query so that it can make a decision to either display the menu horizontally like it does by default or display it vertically when it hits that 415 pixel boundary. You can see the docs for the menu component and the [vertical mode](https://www.telerik.com/kendo-react-ui/components/layout/menu/vertical/).

The way we do this, is that we will create a Hook inside the `main.js` more specifically, the `App` component and we will import `useMediaPredicate` from the package `react-hook-media` a popular React hook that in a sense, creates a subscription to the media query that our component will constantly listen for changes. We can set it to a constant and pass that into the `MenuWrapper` as a prop, we'll call it `isMediumPlus` because it will be true if it's above 415 pixels and it will be false if it is under 415 pixels.

To do this, we need to import the package:

    import { useMediaPredicate } from 'react-media-hook';

Just inside the `App` component, we will set up the constant and name it something that describes what it is doing:

    const checkIfMediumPlus = useMediaPredicate(
      '(min-width: 415px)'
    );

The argument to the `useMediaPredicate()` method is the actual rule we want to check for. If the browser has a minimum width of at least 415 pixels, the return value is `true` otherwise `false`. We can then pass that property into the `<MenuWrapper />` component as a prop:

    <MenuWrapper isMediumPlus={checkIfMediumPlus} />

Now the only thing we have left do is to go into the `MenuWrapper` file and add the `isMediumPlus` prop to the functional component. To add the prop, we just add an parameter to the functional component, we also want to replace the value being passed into the `<Menu />` component itself to instead of being false, we pass the prop in.

    const MenuWrapper = ({isMediumPlus}) => {
      return (
        <div className="nav">
          <Menu
            items={items}
            vertical={isMediumPlus}
            style={{ display: 'inline-block' }}
          />
        </div>
      );
    }

We finally have everything we need in place so that when we make the transition from the small to medium breakpoint, when we trip that 415 pixel wide boundary, we actually re flow the flex items and set the menu to vertical so that it fits into the sidenav displaying in a vertical stack.

On an interesting note, if you inspected the KendoReact Menu in the developer tools, you will notice that it also uses Flexbox to position it's menus and buttons.

Here is the StackBlitz demo that shows the progress we have made:

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-layout-hello-world-2?file=main.js&amp;view=editor&amp;ctl=1"></iframe>  

In the next section we will add some images to our content area and display different images on small(mobile) vs medium browser widths. If the site is loaded on mobile it will only render the smaller image, but if loaded on medium or larger (415 pixels plus) it will render a different image as it's source.

By using the `<picture />` tag and `srcSet` we can create a more responsive experience and serve only the image we need at a particular size. What's important to me is answering a few questions:

How do I deliver high quality images? How do I ensure unnecessary bits are not being downloaded?

So when you are using plain HTML, using the picture tag is easy enough, in React though, I actually prefer working with a package called `react-responsive-image` that will give us a nice component that can help make using the `<picture />` element even easier!

After a quick install of `react-responsive-image`, we will actually render an image right above the text that says "Hello World". For demos sake, since we are rendering the contents of navbar and our main content area in the same file, we will just add our responsive image component directly to the `App.js` page.

Below are two images that I want to show. The one labeled small will be shown for sizes 0 through 414 pixels. The one labeled medium-up will be displayed on everything 415 pixels and larger.

<span>Small (`https://i.imgur.com/OxjKMBr.png`)</span>  
![](https://i.imgur.com/OxjKMBr.png)  

<span>Medium-Up (`https://i.imgur.com/sgz5R9d.png`)</span>  
![](https://i.imgur.com/sgz5R9d.png)  

First we will need to import the `ResponsiveImage` and `ResponsiveImageSize` components, this information is on the front page of `react-responsive-image` GitHub page. Create a constant for each size:

    import { ResponsiveImage, ResponsiveImageSize } from 'react-responsive-image';
    ...
    const small = 'https://i.imgur.com/OxjKMBr.png';
    const medium = 'https://i.imgur.com/sgz5R9d.png';

    const App = () => {
    ...

The way we use these two components together is that a `ResponsiveImage` component will have multiple `ResponsiveImageSize` components nested inside. Each `ResponsiveImageSize` represents a different image you want to show at a different resolution. Like I said I only want to think about 2 different images right now. One that displays on small and one on medium. Below is the code that will make it break at my desired 415 pixels, we will place it just above the paragraph tag that says "Hello World".

    <div className='main'>
      <ResponsiveImage>
        <ResponsiveImageSize
          minWidth={0}
          path={small}
        />
        <ResponsiveImageSize
          minWidth={415}
          path={medium}
        />
      </ResponsiveImage>
      <p>Hello World</p>
    </div>

We now have everything working together. At this point our project looks like the following StackBlitz demo:

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-layout-hello-world-3?file=main.js&amp;view=editor&amp;ctl=1"></iframe>  

We will do one more set of changes in this blog post, we will position the text and some informational content below the image on small and to the right of the image if we are on medium and up.

Let's create a div around the image and the text. Instead of "Hello World" we will render some useful information about KendoReact. By giving those divs that we wrapped around the image and the text some classes, we can create a new breakpoint at 600 pixels that lays out our content a little nicer at the larger resolution.

    <div className='kendo-image'>
      <ResponsiveImage>
        <ResponsiveImageSize
          minWidth={0}
          path={small}
        />
        <ResponsiveImageSize
          minWidth={415}
          path={medium}
        />
      </ResponsiveImage>
    </div>
    <div className='kendo-details'>
      <h1>KendoReact Components</h1>
      <p>Building UI for business apps is hard, even on React. Make it easy with our native React UI and DataViz components.</p>
    </div>

With this change I actually want to introduce a new image for our medium size. It will take the place of our `medium-up` image which we will rename to large. Our small image will stay the same. But this new medium image will be slightly larger but same format as the small image. Here it is along with the other images from before, we will need to update our constants that hold the value for each image using the images below:

<span>Small (`https://i.imgur.com/OxjKMBr.png`)</span>  
![](https://i.imgur.com/OxjKMBr.png)  

<span>Medium (`https://i.imgur.com/ZrM4G3j.png`)</span>  
![](https://i.imgur.com/ZrM4G3j.png)  

<span>Large (`https://i.imgur.com/sgz5R9d.png`)</span>  
![](https://i.imgur.com/sgz5R9d.png)  

    const small = 'https://i.imgur.com/OxjKMBr.png';
    const medium = 'https://i.imgur.com/ZrM4G3j.png';
    const large = 'https://i.imgur.com/sgz5R9d.png';

Finally we will add a new media query setting a breakpoint at 600 pixels and a few more styles to our `custom.css` file.

    .main {
      display: -webkit-flex;
      display: -ms-flexbox;
      display: flex;
      -webkit-flex-direction: column;
      -ms-flex-direction: column;
      flex-direction: column;
    }
    .kendo-image img {
      width: 100%;  
    }
    .kendo-details h2 {
      margin-top: 0.25em;
    }

We have added the regular styles in the code above, they will set the div with the class of `main` to also use Flexbox and act like a container, it's contents flex-direction will be column by default. Next we will add a new large sized media query as well as put some more CSS into the medium sized media query:

    @media screen and (min-width: 415px){
      ...
      .kendo-details {
        padding: 0 1em 0 0;
      }
    }

The code above simply adds padding to the div with the class name `kendo-details`. Now we are ready to add our final breakpoint to represent devices with a larger screen.

    @media screen and (min-width: 600px){
      .main {
        -webkit-flex-direction: row;
        -ms-flex-direction: row;
        flex-direction: row;
      }
      .kendo-details {
        padding: 0 1em 0 1.5em ;
      }
      .kendo-image img {
        min-width: 150px;
        max-width: 223px;
      }
    }

Here, we change the direction of the items inside the div with the class name of `main` as well, we add more padding to the div with the class name `kendo-details` and finally our div with the class name `kendo-image` and we target any images inside of it and ensure that when the screen is above 60 pixels that the image will not get any larger than 223 pixels wide (that's the actual width of the image) as well it will not go any smaller than 150 pixels.

We can now look at our final state of our demo in the StackBlitz below. This demo should show all of our progress up until this point and in fact we are way better off now to start building a real application now that we have some of these basic responsive practices down.

<iframe width="100%" height="400" src="https://stackblitz.com/edit/react-layout-hello-world-4?file=main.js&amp;view=editor&amp;ctl=1"></iframe>  

Play around with the demo and resize the window from small to large to see how the different media queries change the direction our divs layout at each stage.

Please let me know in the comments if you would like to learn more about responsive design in React as we have only scratched the surface. These are the basics and also some of the more modern techniques in building responsive web pages, but by no means can we claim to be responsive ninjas yet. Maybe a second article continuing form this point is in order? Let us know in the comments!