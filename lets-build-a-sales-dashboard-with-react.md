---
title: Let's Build a Sales Dashboard with React
summary: Follow along as we mock-up, design and lay out a sales dashboard with native React components from KendoReact, complete with a responsive grid, data, charts and more.
keywords: JavaScript, Kendo UI for React, KendoReact, React, Tutorial, Web Development
---

Building line of business web apps can be challenging, even with modern frameworks like React. Fortunately, UI libraries like Kendo UI can make this easier. In this tutorial, we are going to utilize [KendoReact](https://www.telerik.com/kendo-react-ui/components/), a library of native UI components built specifically for React. If you have ever used component libraries from Progress, you will feel right at home with KendoReact. However, if you have never heard of Kendo UI, this tutorial will demonstrate what can be done quickly with the library.

## Building the Sales Dashboard in KendoReact

For this article, we'll build a sales dashboard for a fictitious company. We'll use an existing dashboard available on Github built with KendoReact: [kendo-react-sales-dashboard](https://github.com/telerik/kendo-react-sales-dashboard). My goal is to show you how to build a similar dashboard from scratch.

![KendoReact Dashboard](https://i.imgur.com/4R9iyFL.png "KendoReact Dashboard")

Our sales dashboard will show the top selling products for the country store each quarter of the year, broken down by month. I will introduce the data for each component as we build them.

This project covers very basic concepts in React and KendoReact using [Create React App](https://www.telerik.com/blogs/hello-create-react-app-2.0) with native React components. We will also do some basic layout with HTML and CSS and hope to build off of this tutoiral in the futures with more advanced concepts.

## Getting Started

We need to ensure that we [have Node installed](https://nodejs.org/en/download/), version 7 or higher as the latest version of [Create React App](https://github.com/facebook/create-react-app) makes this a requirement. Having Node installed will allow us to use npm to download Yarn Package Manager. If you are new to Create React App, you can brush up on the latest with this article: ([Hello, Create React App!](https://www.telerik.com/blogs/hello-create-react-app-2.0)) written to get folks up to speed with this tool for creating React applications using zero configuration.

* * *

### Ensure Yarn is Installed:

Yarn is used as the default package manager in Create React App. Install it using:

    $ npm install yarnpkg -g

If you have any issues installing Yarn on Windows, just download and run the `msi` installer [here](https://yarnpkg.com/en/docs/install#windows-stable).

* * *

    $ npx create-react-app kendo-react-sales-dashboard
    $ cd kendo-react-sales-dashboard
    $ yarn start

Once Create React App is started you can check what our app looks like in the browser:

![CRA View](https://lh3.googleusercontent.com/A7gMYJS8ZIjHQf_2nYlS282sEw6Dktny0Yg9ybFQlROVSvUKmEJQVuB_pXdjoHNweue3rfHSoZF8bw "CRA View")

Now we can add packages to help create a basic layout for our dashboard. KendoReact has a Material theme that we can pull in as a package for layout. We will also need to bring in a few KendoReact buttons, which will give you an idea of how easy it is to pull the bits and pieces in to get started. Since Create React App uses yarn out of the box and to me it feels like it's a little faster for installing packages, I'm going to use all yarn commands in this tutorial:

    $ yarn add @progress/kendo-theme-material
               @progress/kendo-react-layout
               @progress/kendo-react-buttons

Before we get too far, I want to share my idea of what this app will look like, I have completed a basic sketch using a tool called [Balsamiq](https://balsamiq.com/) showing how the component layout will be arranged.

![Balsamiq Mockup](https://lh3.googleusercontent.com/tobYXIcPrCOpiEmk0Y0q9nW6ynQu33hOLca3uj3rp818eVVE9WBSdK3JBBnbZofL10WPKQOCZJahEA)

Typically a designer and a UX specialist will develop a design prototype to give the developers a much better idea of design direction, but we are on an MVP budget, so for the purpose of our tutorial this Balsamiq mock-up will be our guide. The Material design theme we use will give us nice looking type and polished UI styles with zero effort. Customizing these components is possible, but we will stick with the default.

A follow up I like to do once I have a mock-up like this, is to outline each component and arrange those outlines into a row and column friendly representation. I will use that to understand what structure of `<div>` elements and classes I will need. In the layout below, we have two rows, the first containing the Heading and buttons. Everything else will go in a new row below. The second row is split up into two columns. And inside the right column will be another set of two rows, the first having three columns and the next having just one column.

![Balsamiq Layout](https://lh3.googleusercontent.com/OlY8bzpvztfqYkD9p2bhHtg2h6BPvdazUmf-JCFNQeh4dzv2pU_w2Zcd_hGfclKIWGc7Bqd8_ifAKA)

Now that we have these sketches we can build the markup using `<div>` elements and assign classes indicating how many of the maximum 12 units each column will make up. In the next section, I'll introduce you to the markup structure that will house the components.

## The HTML

Considering the layout we saw above, I have created a hierarchy of `div`s each given a `className` in the traditional _“12 column responsive grid”_ fashion, and simplified that idea in a visual aid. In React we use the attribute `className` instead of `class` anytime we are defining CSS classes in JSX. For brevity, I have referenced only the `xs` breakpoint for each `<div>`, but in the Gist I have of the breakpoints required to ensure our layout doesn't shift as we resize the page.

![MockupHTML](https://d585tldpucybw.cloudfront.net/sfimages/default-source/blogs/2018/2018-10/mockuphtml.png?sfvrsn=d3a8cfe2_1 "MockupHTML")

Each of the custom tags I have put in this image above are just placeholders used for visual representation, so don't copy this HTML verbatim. Again this is just to help us understand the structure we will need.

You will see many tags in the HTML that we will eventually replace with the actual component or HTML we need. Below is the actual code that I want you to copy into your `App.js` page to get us started.

I'm also going to give you some CSS code to past into your `App.css` file. Go ahead and replace the CSS in your `App.css`file with the Gist below.

Finally, add bootstrap. To keep things simple, add a link to the [Bootstrap CDN](https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css) to the `public/index.html` file. Add it just underneath the **shortcut icon**:

    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" />

This contains some styles not only to help with some of the HTML that we just pasted in. Your page also looks a little crazy right now, but in reality everything is there in place for layout for us to move to the next step, which will require getting some data ready and adding our first Kendo UI components (buttons).

## Adding Buttons

We already have a few buttons on the page, but we want to change those to Kendo UI buttons because it will allow us to bring in our first Kendo UI components and Kendo UI Material theme. We already have the dependencies added so let's go into our `App.js page` and add the `Button` & `savePDF` imports just underneath the `import ReactDOM` line at the top of the `App.js` page:

    import ReactDOM from 'react-dom';
    import { Button } from '@progress/kendo-react-buttons';
    import { savePDF } from '@progress/kendo-react-pdf';

We can wire up the **Export to PDF** button. Let's install these packages with Yarn to get that done.

    $ yarn add @progress/kendo-react-pdf
               @progress/kendo-drawing
               @progress/kendo-react-buttons

Now change both `<button>` tags (like below) to use an uppercase B:

    <Button>Share</Button>
    <Button>Export to PDF</Button>

Run the app using `$ yarn start` if not already running. You should be at least seeing the text and the buttons now.

## Export to PDF

A lot of times we simply want the user to be able to print everything on the page to a PDF file. In order to do this, we can use the package just imported to do all the heavy lifting.

Add the following code to your App Component Class in `App.js`:

    constructor(props) {
      super(props);
      this.appContainer = React.createRef();
    }

    handlePDFExport = () => {
      savePDF(ReactDOM.findDOMNode(this.appContainer), { paperSize: 'auto' });
    }

With that code in place, we need to bind `this.appContainer` to an object, which is a reference to the HTML element that contains the area we want to print to PDF.

Because we want to print the entire sales dashboard, we will place an `ref` attribute on the outer most `<div>` in our JSX. You can locate it by it's _**className**_: `app-container`:

    <div className="app-container" ref={(el) => this.appContainer = el}>

The [`ref` attribute](https://reactjs.org/docs/refs-and-the-dom.html) allows us to assign an `HTMLDivElement` representing the contents of the `<div>` element it is placed on, to a local property.

Next, we will want to ensure that we are calling the `handlePDFExport()` function from the `onClick` event. Let's also disable the other button for the time being.

    <Button disabled>Share</Button>
    <Button onClick={this.handlePDFExport}>Export to PDF</Button>

Let's now test our button to ensure everything is working. When the button is pressed, you should get a prompt to download a PDF file. Upon opening the PDF you should see the entire contents of our page. You can imagine what would happen if we put this attribute on another `<div>` in our page. At that point the button would only print the contents of the `<div>` element. We will revisit this idea once we get the Grid working and create a button that only prints the data grid.

One thing I want to point out before moving on is that in React, when we want to call a function inside our JSX like we did on the `onClick` handler, we simply assign that function name to the attribute. No need for quotes invocation parenthesis, just the name of the function like below:

    onClick={this.handlePDFExport}

But wait? Our buttons look all… meh! We forgot something. We need to bring in our Kendo UI Material theme now that we are actually using some Kendo UI components on the page. Once we import the right CSS file, all of the other components we need to bring in will also benefit from this styling.

Import the Material Theme at the bottom of our imports on `App.js` just above the import for `App.css`.

    import '@progress/kendo-theme-material/dist/all.css';

And let's not forget that we will need to pull in this theme using yarn in order for that import to work.

    $ yarn add @progress/kendo-theme-material

Let's also bring in a class that will give our buttons some spacing. It's already defined in the styles we have added to the `App.css` file. On the div that surrounds our buttons, add `buttons-right` to the `className`. The buttons and their containing div should now look like this:

    <div className="col-xs-3 col-sm-3 col-md-3 col-lg-3 col-xl-3">
      <Button disabled>Share</Button>
      <Button onClick={this.handlePDFExport}>Export to PDF</Button>
    </div>

Now you should see your buttons taking on a Material Design style.

![Material Themed Buttons](https://lh3.googleusercontent.com/lJXFzsVGDWWapYMRcOeQrjeuHrIc-uOorgq0HEHlwhH7e7KrfEUmcS_qfddDfaboTdZoDFKQV5uCbQ "Material Themed Buttons")

## Share Dialog

Let's wire up the share button now. In a real production application this would talk to a service that could be used to send an email to someone in order to share the dashboard link, but we are just going to make it print to the console.

In the constructor for our `App.js` file, lets create an object to hold state. This state object is understood by React to be a special object. Under the hood, React treats this object differently.

    constructor(props) {
      super(props);
      this.appContainer = React.createRef();
      this.state = {
        showDialog: false
      }
    }

Let's create a function inside the `App` class, underneath the `handlePDFExport()` function. As I mentioned [React state](https://reactjs.org/docs/state-and-lifecycle.html) objects are special, they have an API used specifically for interacting with it. For instance, if we want to change the state in any way, we should not access the object directly and assign new values. Instead we use the `setState` method for updating the state. This will schedule an update to a component's state object. When state changes, the component responds by re-rendering.

    handleShare = () => {
      this.setState({
        showDialog: !this.state.showDialog
      })
    }

> _**PRO TIP:**_ To execute a function, or verify if the state updates correctly, we can pass a function as a second argument (callback) to `setState()`, the function will be executed once the state is updated. Find out more and [explore the React docs for state](https://reactjs.org/docs/react-component.html#other-apis-1).

    handleShare = () => {
      this.setState({
        showDialog: !this.state.showDialog
      }, () => console.log(this.state))
    }

We also need to update the button to use this function. We will further add a distinguishing feature by setting primary to `true`. Behind the scenes, our component takes that `true` value and gives the button a `primary` style:

    <Button primary={true} onClick={this.handleShare}>Share</Button>

So this button toggles a boolean value in our state object, which is typically a good way to hide and show modals, pop ups or hidden areas of the page. But we need to create a hidden area that will reveal itself when this button is clicked. As we saw from our setState callback, each time we press the **Share Button** that value is flipped. This HTML block that we are going to add should be replaced by the code below:

    <h4 style={{display : 'none'}}>Dialog Shown/Hidden with Logic</h4>

Replace with the following code:

    {this.state.showDialog &&
      <Dialog title={"Share this report"} onClose={this.handleShare}>
        <p>Please enter the email address/es of the recipient/s.</p>
        <Input placeholder="example@progress.com" />
        <DialogActionsBar>
          <Button primary={true} onClick={this.handleShare}>Share</Button>
          <Button onClick={this.handleShare}>Cancel</Button>
        </DialogActionsBar>
      </Dialog>
    }

Let's unpack what we just added: we brought in a new KendoReact component called `<Dialog>` which is wrapped in an expression that will hide or show the area based on the `state.showDialog` value being flipped. The best way to think of this is that our `<Dialog>` component equates to a truthy value. It's similar to saying:

    { this.state.showDialog && true }

So because it's paired up with the `this.state.showDialog`, if both equate to true, the Dialog displays. However, if `this.state.showDialog` is false, the output of the `<Dialog>` component is not revealed. Again this is just a way to think about this statement if for any reason it looks weird to you.

The `<Dialog></Dialog>` component will not work without importing it from the `react-dialogs` package, so let's get that added and imported:

    $ yarn add @progress/kendo-react-dialogs
               @progress/kendo-react-inputs
               @progress/kendo-react-intl

And we'll also import those packages in our `App.js`. Our imports should now look like this:

    import React, { Component } from 'react';
    import ReactDOM from 'react-dom';

    import { Dialog, DialogActionsBar } from '@progress/kendo-react-dialogs';
    import { Input } from '@progress/kendo-react-inputs';

    import { Button } from '@progress/kendo-react-buttons';
    import { savePDF } from '@progress/kendo-react-pdf';

    import '@progress/kendo-theme-material/dist/all.css';
    import './App.css';

I noticed something missing when I clicked on our new buttons. Material Design UI I have worked with in the past utilizes a ripple effect on certain UI elements. Buttons definitely show this ripple effect and I am not seeing it on ours. This is because Kendo UI provides this as a separate package, which I think is a good idea because I may or may not want the additional code brought into the CSS and JavaScript if I don't want to use it. Let's add and import this `<Ripple>` as a component that will wrap our application:

    $ yarn add @progress/kendo-react-ripple

With that done, you can now import `Ripple` into the `App.js` page just above the **Dialog** and **DialogActionsBar** import:

    import { Ripple } from '@progress/kendo-react-ripple';

Next, we want to add a `<Ripple />` container around the `<div>` element of the `app-container` so that all `Button` and other components will get the ripple effect applied to them as a child of `<Ripple />`:

    class App extends Component {
      constructor(props) { /* ... */ }
      handlePDFExport = () => { /* ... */ }

      render() {
        return (
          <Ripple>
            <div className="app-container" ref={(elem) => this.appContainer = elem}>
              { /* ... */ }
            </div>
          </Ripple>
        );
      }
    }

    export default App;

Now when you click and drag outside the button hit state and release, you will experience the effect without activating the button's `click` event.

![Ripple Effect](https://lh3.googleusercontent.com/Z7FC6bPNAdyjgW32cvpuEG4KQ5Ghd4-_rtGRAynSFv4Udj-yJ1ZQZ_uNxSegDOjtXW8rJYp-Rsc7MQ "Ripple Effect")

## Mmm, Donut Charts

I'd like to start bringing in the `Chart` component. It has the least amount of data associated with it, so it's a logical next step and easy to implement.

Let's add the component (commented out), replacing the `<h4>` element placeholder. Find the line of code that reads:

    <h4>Donut Chart Container</h4>

And replace it with:

    {/* <DonutChartContainer /> */}

![Create a Components Directory](https://lh3.googleusercontent.com/RSBGY_xZE2KdOb--QLcmQNeluO76xbfoEWY_aAPTKxAA0_F0WOarv80XeQMgtdZ_6cAgppY-GBNiDQ "Create a Components Directory")

Next, let's add a directory for all of our container components and call it `components`, and inside create our first container component of many named: `DonutChartContainer.js`. We will continue with this naming convention for each of our KendoReact components.

We also need to bring in the package for the [KendoReact Charts](https://www.telerik.com/kendo-react-ui/components/charts/):

    $ yarn add @progress/kendo-react-charts

Next, copy the code that I have modified from the Kendo UI documentation into `DonutChartContainer.js` from the Gist below:

The KendoReact charts provide a vast set of features for building rich data visualizations. To learn more about them, feel free to check out the [Charts API](https://www.telerik.com/kendo-react-ui/components/charts/api/).

![Create Data Directory](https://lh3.googleusercontent.com/nefnuKMuR7IHwbyWciU6xIoYXcGmXyJMs8PIOHFSTE7bgQWK86TH7Z3Op7KnHVXgO0__CaCcy3g_tg "Create Data Directory")

The first thing we want to create for the `Chart` is some dummy data. Like I said before, all of our components will need data. Let's create a directory named `data` as a sibling to our `components` directory. Inside that directory create a file named: `appData.js`.

Remember, the idea is to show what percentage of food (by category) has sold in Q4\. That specific data is what we will use to populate the donut chart. We'll need some type of label and percentage value.

*   `foodType` category of foods sold in Q4 at all stores
*   `percentSold` percentage represented as a decimal sold in all stores in Q4

Copy the code below into the `appData.js` file:

    export const donutChartData = [
      { 'foodType': 'Beverages', 'percentSold': 16.5 },
      { 'foodType': 'Condiments', 'percentSold': 24 },
      { 'foodType': 'Produce', 'percentSold': 13 },
      { 'foodType': 'Meat/Poultry', 'percentSold': 16.5 },
      { 'foodType': 'Seafood', 'percentSold': 20 },
      { 'foodType': 'Other', 'percentSold': 10 }
    ];

In the `App.js` file, we need to add an import:

    import { DonutChartContainer } from './components/DonutChartContainer';

... and uncomment the `{/* <DonutChartContainer /> */}` in the HTML.

    <DonutChartContainer />

Now our component should be working. Let's make a change so that you understand how we can format the label for the Donut Chart. Right now we are only displaying the category because we specified that in our component configuration.

Inside the `DonutChartContainer.js` file, Change the `labelTemplate` function to:

    const labelTemplate = (e) => (e.category + '\n'+ e.value + '%');

![enter image description here](https://lh3.googleusercontent.com/8Lb0skzqJZEsfgR7aHCqYCqYHSusicoGB-LLUsfhyOeYARnNLP2XUEkULYudNDas1g87z1EefvwQ7w "Desired Donut")

Here is our beautiful Donut, it even looks tasty! When we use the Donut Chart, we interact with a `<ChartSeriesLabels>` component. The `content` input accepts a function that returns a string. It's that simple. It fills each section (categories in our case) with rich goodness. Using just what we know about JavaScript, we can achieve some better formatting and I think we may want to use `e.percentage` instead of `e.value`. You can get details on the fields we can tap into in our [ChartSeriesLabels documenation](https://www.telerik.com/kendo-react-ui/components/charts/api/ChartSeriesLabelsProps/#toc-content).

I have modified the template function to achieve a more desirable display and by choosing percentage I guarantee I will always get each category representing its portion of the total. This is in case maybe we decide to use data that doesn't equal 100 as a total for all values.

    const labelTemplate = (e) => (e.category + '\n'  + (e.percentage*100) +'%');

The display has not changed here, I just wanted to use `percentage` instead of `value`.

## Raising the Bar Chart Component

The next logical step is to create a bar `Chart` which represents a monthly breakdown of the percentages from each individual month from Q4 2018\. The donut `Chart` showed the average percentage over the entire quarter, but our bar chart will show each month of that quarter. Below is the data we need to add to our `appData.js` file. You will notice that our data corresponds to the Donut Chart as well, so the user can easily see the relationship.

    export const barChartQ4Months =['October', 'November', 'December'];
    export const barChartMonthlyPercentages = [
      { name: 'Beverages', data: [14, 16, 19.5] },
      { name: 'Condiments', data: [24, 23.5, 24.5] },
      { name: 'Produce', data: [12.5, 12.5, 14] },
      { name: 'Meat/Poultry', data: [16, 18, 17] },
      { name: 'Seafood', data: [21.5, 20, 17] },
      { name: 'Other', data: [7, 12, 11] },
    ];

With the data in place, we can add a new container component to our `components` directory. Create a file named `BarChartContainer.js`.

Replace the `<h4>` element placeholder. Find the line of code that reads:

    <h4>Bar Chart Container</h4>

And replace it with:

    {/* <BarChartContainer /> */}

Next, copy the code that I have modified only slightly from the Kendo UI documentation examples and put it into `BarChartContainer.js` from the Gist below:

Place an import in at the top of the page, just above our CSS imports in `App.js`:

    import { BarChartContainer } from './components/BarChartContainer';

... also in `App.js`, uncomment `{/* <BarChartContainer /> */}` in the HTML.

    <BarChartContainer />

Do a quick visual confirmation to ensure that your bar chart lines are using the same colors as the Donut Chart. Everything should line up because our data for each chart is in the same order. If you were building an API to serve this data, that would be something you would want to ensure does not get messed up.

That may have been the easiest one yet to setup. The container page is very straight forward as we are not dealing with any state. We still like to have that layer of abstraction in our project though.

The way I like to think about this component, is that I look at my shape of data. We have an array of months, each one of those months will translate into a category on the barchart. We also have an array of objects. Each of these object has a `name` field that corresponds with our categories of food. It will also have a data field. So for each month (category on the bar chart), we iterate over the first index of every data fields array. Each iteration builds a bar whose height corresponds to the index's value. Again this happens for each month.

My tip to anyone working with this chart is to take that example and become familiar with how each tag inside the `<Chart>` component plays into that story of how I broke the data down. We have a [Legend](https://www.telerik.com/kendo-react-ui/components/charts/api/ChartLegendProps/), [ChartCategoryAxis & Items](https://www.telerik.com/kendo-react-ui/components/charts/api/ChartCategoryAxisItemProps/), ChartSeries & Items, [ChartValueAxis & Items](https://www.telerik.com/kendo-react-ui/components/charts/api/ChartValueAxisItemProps/) and of course the encompassing component, the [Chart](https://www.telerik.com/kendo-react-ui/components/charts/series-types/bar/) itself.

The opportunity for hacking on these charts is definitely here as well. Check out this article on [Data Visualizations with Kendo UI](https://developer.telerik.com/featured/6-rules-for-awesome-data-visualizations-with-kendo-ui/) fro some really cool ideas for using the different charts, including our friend Mr. Bar Chart. Setting that to the side for now, let's proceed onward.

## Adding the Grid Component

The `Grid` container is by far one of our most used and requested components in Kendo UI.

A list of products will serve as our data for our grid. We'll copy the gist below and paste it into `appData.js`. This will serve as the top 10 products of Q4, which are the heart of the data we are building the dashboard around. In a more advanced situation, the `Grid` could be populated by an search with autocomplete and more products could be filtered or searched, etc. The thing I love about Kendo UI is that most of the stuff I can dream up is just a few imports away and takes little wiring up.

Before doing anything, I want to show you what packages I add before using the `Grid`:

    $ yarn add @progress/kendo-data-query
               @progress/kendo-react-dateinputs
               @progress/kendo-react-dropdowns
               @progress/kendo-react-grid
               @progress/kendo-react-inputs
               @progress/kendo-react-intl

That should cover all of the items we need for our gird component. Two of these we already have installed, but that's only because KendoReact components sometimes have dependencies that are also present in other components. There is no harm in running the install again.

Next, Let's add the data to our `appData.js` file:

Looking at the data, the most important fields in our data objects are the product's ID, name, category, price, in-stock and discontinued fields. I brought in a little more data than we needed. This was in hopes that I could get you to play around with displaying different fields and experimenting with the grid itself.

The main components for a KendoReact `Grid` are the actual `<Grid>` element which contains child `<Column>` components, each mapping to a specific field from our data object.

I want to give you a quick visual of the code for this component, so if I only wanted to display the ID, name and category from our data set, I could very easily and almost from memory build that component:

    <Grid style={{height:'300px'}} data={gridData}>
      <Column field="ProductID" title="ID" />
      <Column field="ProductName" title="Name" />
      <Column field="Category.CategoryName" title="Category Name" />
    </Grid>

And that would look like this rendered on the page:

![Basic Grid](https://lh3.googleusercontent.com/H00ow4ioymVwPBkvbhCO4MBCAynwUfAEOZufj_joXrExAM0ewToN0oz7PcE3MA_sB3xCFgBP0-78fA "Basic Grid")

Next, open the `App.js` file and add the component by replacing the `<h4>` element placeholder. Find the line of code that reads:

    <h4>Grid Container</h4>

And replace it with:

    {/* <GridContainer /> */}

Implementing the `Grid` is that simple. In our project, we are going to use a few more properties and some more column sizing than you saw in the example above. Copy the entire component from the gist below and put it into a new file named `GridContainer.js`:

Add the import:

    import { GridContainer } from './components/GridContainer';

And now uncomment the reference to the component:

    <GridContainer />

![Grid Container Version One](https://lh3.googleusercontent.com/tdew-UBYtqoRjiXo5CtbUd7DYwy_dk86xyv25eIlpLyGpNwJEFtwaxWl4911k32YBrIqwT9lLHgiIA "Grid Container Version One")

At this point, we have the `Grid` component working, but I am already thinking about some of the things I want to do with this `GridContainer.js` component, and it will involve managing state. Although I don't want to bring in anything like Redux at this point, I may have to switch from using a stateless functional component to using a class based component. But before we go there, I want to point out that so far we have used only stateless functional components to create our components. I would like to take a few moments to explain why and give you a quick primer on two ways of creating components in React.

### Stateless Functional Components

Up until now we have been using stateless functional components, or in other words, components that are defined as a function. They only take a single props object argument and do not hold any of their own state - they don't have life cycles. Until now we have not required any local state for our container components. They serve only as simple containers for our Kendo UI components. The separation is good for organization, but that's it. I want to quickly show you another way of writing a functional component using the ES6 arrow function, that will allow us to omit the keywords, `function` and `return`, and the curly braces. Using this method a component could look like this:

    const HelloContainer = ({ data}) => (<div>Hello, {data.name}!</div>);

Very useful if we are creating simple container components without any state, and I should note that forcing yourself to use these types of components whenever possible is something you should always strive to do.

### Class Components

Class components benefit from being able to have a constructor and manage their own state. The syntax looks like this:

    class HelloContainer extends React.Component {
      render() {
        return <div>{this.props.name}</div>;
      }
    }

If you would like to learn more about the many ways of creating components in React, which is above and beyond this tutorial, [check out this video from Michael Chan](https://www.youtube.com/watch?v=YaZg8wg39QQ).

So far we have not done anything special with the `GridContainer.js` requiring us to use the class method of creating components. Let me show you where I go from knowing I can use a stateless functional component, to realizing I need a class based component that can handle state.

### Embed Sparkline as Content for a Grid Column

I want to add a new `<Column />` to this component, and I want to show you a cool trick that will allow us to inline a [KendoReact Sparkline](https://www.telerik.com/kendo-react-ui/components/charts/sparkline/) by [customizing the the KendoReact Grid's `cell`](https://www.telerik.com/kendo-react-ui/components/grid/cells/) content. To do this we will need to create a randomized set of data to use for the `Sparkline` component. We can then insert that random data array into the already existing `gridData` object for each item and make it a property called `PriceHistory`.

Let's start by converting this component into a class-based component and importing the `Sparkline` component. Let's swap out our component with the following gist:

Copying in that new code, we went from using `export const` to using `export default class`, or we went from stateless functional component to class based component. In doing so, we encountered an error. We need to update our import statement in `App.js`.

    import GridContainer from './components/GridContainer';

[Learn more about when to use curly braces when importing in ES6](https://stackoverflow.com/questions/36795819/when-should-i-use-curly-braces-for-es6-import/36796281#36796281).

We added some code to modify the data and add random numbers to an array. We'll create a function, `processData()` for this purpose and add it to the `GridContainer`:

    processData = (data) => {
      data.forEach((item) => {
        item.PriceHistory = Array.from({length: 40},() => Math.floor(Math.random()*100));
        return item;
      })
      return data;
    }

The property, `PriceHistory`, is now available when the `Grid` is rendered. We can see this by placing a `debugger;` statement before the `return data;` line in our new function and then opening the Chrome DevTools and inspecting that `data` object. Now we just need a `Sparkline` that can use the new `PriceHistory` property.

We are going to build another component inside our `GridContainer.js` file because this new component will only be used here in this file. Just under the import statements, create a new exported class with the following code:

    class SparkLineChartCell extends React.Component {
      render() {
        return (<td><Sparkline data={this.props.dataItem.PriceHistory} /></td>)
      }
    }

Next, add the new column to the `Grid` component, just above the discontinued column:

    <Column field="PriceHistory" title="Price history" cell={SparkLineChartCell} />

Just in case you have any issues I have created [a gist](https://gist.github.com/httpJunkie/7a8a1f14e5d5fdc90065efe29d457ec0) for `GridContainer.js`, showing what it should look like at this point. And just like that, we have `Sparkline` component rendering inside of a column in each `Grid` row:

![Grid Container Version Three](https://lh3.googleusercontent.com/wG4ku4srR2hDsF-JnfuAZ2v0eWWl4yXCqZtO3FXIGanh_eQANCLds_HGLzNP54SaWVcv5Y9b1jEf0w "Grid Container Version Three")

## Adding PanelBar Navigation

Before getting started, we need to install a package:

    $ yarn add @progress/kendo-react-layout

The data is very straightforward. Let's copy that into the `appData.js` file. The shape of the data is an object with two top level nodes containing arrays as values.

Let's add the `PanelBarContainer` component. Once it's completely implemented, we will be able to use it to affect some of the other states in the application to demonstrate some interactivity. But first we need to get the component working and we need to bring in some additional styles for the Teammate's section of the `PanelBarContainer`. Copy the code in this Gist and add it to the bottom of the `App.css` page:

Now we just need to copy the Gist below and paste into our `PanelBarContainer.js` component:

Once that's done being copied into `PanelBarContainer.js`, we need to add the import to `App.js` for the `PanelBarContainer`:

    import PanelBarContainer from './components/PanelBarContainer';

And replace the `<h4>` element for the `PanelBarContainer`:

    <PanelBarContainer />

We will also need to add some profile images for each team member, I have created a small zip file that has some images already sized correctly that you can use: `profile_images.zip`.

After you have downloaded those images, add them to a `public/img` directory in your project for any static files like logos, graphics, images, etc. The public directory is the right place for these.

Our new component should look like this:

![Panel Bar](https://lh3.googleusercontent.com/OyymscEafIoYJqMHI9UUdTj-3kV-e3iIm1cXMWnPTbwdhw89WeA2O4A8HsczsVPi1bo0EisZiEgjmA "Panel Bar")

At this point we have done a lot of work, and the dashboard is laid out in a manner that will look decent on medium and large sized screens (960px and up). It also can do some adjusting to lower resolution screens, but the team member section in particular could use some additional media queries to help accommodate lower resolutions.

A few things that we could do to expand this demo is add some interactivity, or refactor to work with Redux, and we could also build an API to serve up our data. And I'd like to implore you to explore these options and let us know what you think about our components in the comments section. Also let us know if you would like to see this demo taken further with more advanced concepts we could build.

### Try Out KendoReact

We've accomplished all this with the help of [KendoReact](https://www.telerik.com/kendo-react-ui/), which we've built from the ground up with native UI components so you can build beautiful React apps quickly. Feel free to download a [free 30 day trial today](https://www.telerik.com/download-login-v2-kendo-react-ui) and explore everything KendoReact can do.

[Start My KendoReact Trial](https://www.telerik.com/download-login-v2-kendo-react-ui)