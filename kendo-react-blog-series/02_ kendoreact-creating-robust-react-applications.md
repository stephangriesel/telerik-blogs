---
title: Creating Robust React Applications
summary: This second post in the series gets us started with KendoReact and provides a better understanding of how to build robust applications in React.
keywords: JavaScript, Kendo UI, Kendo UI for React, KendoReact,React, Web Development
---

In this second post of the [Getting Started with KendoReact](https://www.telerik.com/blogs/kendo-react-getting-started-blog-series) series, Eric Bishard helps you better understand KendoReact so you can build more robust applications. See what KendoReact can do for you, the React developer!

Back to the [First Post](https://www.telerik.com/blogs/kendoreact-what-can-it-do-for-you) of the series.

* * *

## Pt 2\. Creating Robust Applications with KendoReact

The first thing that we're going to do today is use [create-react-app](https://github.com/facebook/create-react-app). Then, we'll locate the components we're going to use from the [KendoReact site](https://www.telerik.com/kendo-react-ui/components), and install them using node package manager.

We will also install the Kendo [default theme](https://www.telerik.com/kendo-react-ui/components/styling/theme-default/).  
![KendoReact Default Theme](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/default-themea5f7c40fb19a4cfbbfdd4ab5bbade752.png?sfvrsn=fd2e954c_1 "KendoReact Default Theme")

We first build out the project using create-react-app. [If you are new to Create React App, check out this article to learn more](https://www.telerik.com/blogs/hello-create-react-app-2). Otherwise, let's open our terminal and globally install it (if needed):

    npm install create-react-app -g

Once installed we can run `create-react-app `anytime we want, let's do just that.

    create-react-app kendo-react

We'll mostly be working in the `src` directory. Remember you can always refer to the ;[KendoReact documentation](https://www.telerik.com/kendo-react-ui/components/) to get more information about all the components. For this project we'll be working with [Buttons](https://www.telerik.com/kendo-react-ui/components/buttons/), [DropDowns](https://www.telerik.com/kendo-react-ui/components/dropdowns/), [NumericTextBox](https://www.telerik.com/kendo-react-ui/components/inputs/numerictextbox/) and [Grid](https://www.telerik.com/kendo-react-ui/components/grid/) components.

First, let's just install the buttons. We see that in the [Buttons documentation](https://www.telerik.com/kendo-react-ui/components/buttons/#toc-installation) that we have an Installation section that let's us know how to get started. We just need to install the Buttons library with npm by running:

    npm install @progress/kendo-react-buttons

That will save the package to the project's `package.json` and all Kendo packages follow this same naming convention:

    npm install @progress/kendo-react-<componennt-name>

Now lets install the rest of the packages we need: DropDowns, NumericTextBoxes and also the [internationalization package](https://www.telerik.com/kendo-react-ui/components/globalization/i18n/), which is required for globalization features in KendoReact components.

    npm install @progress/kendo-react-grid @progress/kendo-data-query @progress/kendo-react-inputs @progress/kendo-react-intl @progress/kendo-react-dropdowns @progress/kendo-react-dateinputs @progress/kendo-react-pdf @progress/kendo-drawing

Now we can go ahead and talk about the theme. In order to get some nice, modern styling, we need to install one of [these themes](https://www.telerik.com/kendo-react-ui/components/styling/). For this project, we actually won't be doing any customization in CSS, we'll solely rely on the styling from the theme. If you do want to customize, you can use the [Progress Theme Builder](https://themebuilder.telerik.com/). This builder lets you customize your theme for any Kendo UI component library. You can use Material, Bootstrap or your own custom settings using those themes as a starting point.  

For today, we are actually just going to install the default theme. All we are going to do is run:

    npm install @progress/kendo-theme-default

This package is now added to your `package.json` and also resides in your `node_modules` directory and we can include it in React with a simple import. Next, we import the theme CSS into our `App.js` page:

    import '@progress/kendo-theme-default/dist/all.css';

Before getting started on the Kendo components, you can delete the contents of `App.css`, the `logo.svg` and its import statement at the top of the `App.js` file. While we're editing the `App.js` file, let's replace the HTML (JSX) with the following:

    <div> <h1>KendoReact Grid</h1> </div>

* * *

Check out the [](https://www.telerik.com/blogs/kendoreact-creating-robust-react-applications)[third post](https://www.telerik.com/blogs/kendoreact-adding-a-grid-dropdown-list-and-more) of the series, [KendoReact: Adding a Grid, Dropdown List and More](https://www.telerik.com/blogs/kendoreact-adding-a-grid-dropdown-list-and-more).