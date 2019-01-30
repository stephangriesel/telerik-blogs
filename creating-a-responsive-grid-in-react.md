---
published: true
title: Creating a Responsive Grid in React
summary: In this article go beyond basic media queries and layouts and leverage Flexbox to do responsive grid layouts first by hand and then using a popular React package called react-flexbox-grid!
keywords: Guide, JavaScript, React, Responsive, Tutorial 
---

In our first article we started by learning how to setup some basic layout in our React application using Flexbox to go responsive, we played around with some npm packages to help with images and breakpoints, we also showcases the KendoReact Menu component and by the end we had a fairly responsive demo that we could build on. Today we do just that, we keep building and working to refactor and make better what we already built as well as learn some new techniques around rolling our own responsive grid, so that we understand the concepts, we then replace that code with the use of react-flexbox-grid.

Our starting point will be the StackBlitz demo that we left off with in our previous article:

[STACKBLITZ DEMO 04](https://stackblitz.com/edit/react-layout-hello-world-4)

Our application to start with should look like the image below:

![](https://i.imgur.com/etEIlNo.gif) 

It's not going to win any awards, but we are not really focusing on look and feel yet, we are still getting our sea legs in this constantly moving and resizing responsive world.