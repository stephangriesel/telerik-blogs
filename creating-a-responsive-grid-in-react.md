---
published: true
title: Creating a Responsive Grid in React
summary: In this article go beyond basic media queries and layouts and leverage Flexbox to do responsive grid layouts first by hand and then using a popular React package called react-flexbox-grid!
keywords: Guide, JavaScript, React, Responsive, Tutorial 
---

In our first article we started by learning how to setup some basic responsive layout in our React application using Flexbox and media queries. We used a React Hooks npm package to help with breakpoints and another package for helping with responsive images (picture tag), we also showcases the KendoReact Menu component and by the end we had a fairly responsive demo that we can build on in this article. No different from UI, layout takes time and baby steps, we can keep building and working to refactor and make better what we already built as well as learn some new techniques around responsive layout and slowly incorporate those ideas. The next thing we should work on in this application is bringing in some type of responsive grid. I would like to use another npm package to do this, it's called react-flexbox-grid.

Our starting point will be a StackBlitz demo which is simply a fork of the demo where we left off in the last article. I would recommend making a fork of this demo if you plan to follow along. Otherwise, just read on and understand that you can open up any of the demos I provide to play with the code at any stopping point in the article. I will provide several demos at various points in this article.

[STACKBLITZ RESPONSIVE GRID DEMO 01](https://stackblitz.com/edit/react-responsive-grid-1)

Our application to start with should look like the image below:

![](https://i.imgur.com/etEIlNo.gif) 

It's not going to win any awards, but we are not really focusing on look and feel yet, we are still getting our sea legs in this constantly moving and resizing responsive world. And we have already learned some very basic layout techniques to build on. With that said, in this part of the blog series I want to focus on creating a responsive grid that we can use in our application so that we don't have to bring in something like Bootstrap just to use their grid.

I'm going to mockup something that we can try and build that will utilize this grid for many breakpoints. The idea will be a grid of logos of companies that use our product. This is a pretty standard thing that companies do on their website and the same concept can be applied to many different uses. I first need to get a number of logos that we can use from Imgur. We will display these images in a grid showing 4 wide at a large resolutions, 3 wide at medium resolution and 2 wide at a small resolution.

I'm going to fork our demo and start working on our first set of changes.

First order of business is to add the package we want to use for a flexbox grid solution: `react-flexbox-grid`.

Next we need to create a list of companies in a json file that we can repeat over. And would would be wise to just get a list of names to repeat on the page for every company. Our `companies.json` files will simply contain an array of objects. Each object is a company, it has a name and url for an image. I will upload an image for each company to Imgur.com that we can use for our URL.

We add a `companiesList.json` file.

```
[
  { "name": "Nasa", "image": "https://imgur.com/RTFOOHR" },
  { "name": "Microsoft", "image": "https://imgur.com/yln0oYC" },
  { "name": "Phillips", "image": "https://imgur.com/ZHKnVr8" },
  { "name": "Fox", "image": "https://imgur.com/Hrzbo49" },
  { "name": "Sony", "image": "https://imgur.com/Ld5Ux3g" },
  { "name": "IBM", "image": "https://imgur.com/rg7RAdm" },
  { "name": "Toshiba", "image": "https://imgur.com/aj9vfmu" },
  { "name": "Volvo", "image": "https://imgur.com/hTkpXvw" }
]
```

We need to create a `Companies.jsx` page. These component files don't have to use the `.jsx` format, they could just as well be a `.js` file. I typically use `.jsx` for any new component that returns JSX. Otherwise, I use `.js` that is a convention of mine and you do not have to follow it.

```
import React from 'react';
import companyList from './companiesList.json.json';

const Companies = () => {
  return (
    <div className="companies">
      {companyList.map(co => <div>{co.name}</div>)}
    </div>
  );
}

export default Companies;
```

Nothing too complex here, we import react and our company list. We create a functional component that simply maps over the companies list and sticks the name value inside of a div. This is repeated for each company and now we can think about how we will go from this, to building a flexible grid for each of the images instead.

Now let's add the following import to the `main.js` page:

```
import Companies from './Companies';
```

And display our Companies component below our information about Kendo. The div with the class name of `kendo-details` will now look like the code sample below:

```
<div className='kendo-details'>
    <h2>React Components</h2>
    <p>Building UI for business apps is hard, even on React. Make it easy with our native React UI and DataViz components.</p>
    <h2>Companies Using Kendo</h2>
    <Companies />
</div>
```

At this point in time and if you have been following along, your demo will match the StackBlitz below:

[STACKBLITZ RESPONSIVE GRID DEMO 02](https://stackblitz.com/edit/react-responsive-grid-2)

## Let's Talk About the Images

The images in this list are `600 x 600 px` and we don't want to show them at that resolution, so I wanted to just loop over the names to ensure our logic and code was working. I actually want to have a different image for each breakpoint, but let's take baby steps to get there. This would mean having 600 pixels be the size of our images to show above large breakpoints. 300 pixels would be the size of our images above the medium breakpoint and until the large breakpoint. And finally, our images on small would be 150 pixels wide.

But for now, we can just resize them to take up 100% of their space.


