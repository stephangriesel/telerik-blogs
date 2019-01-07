---
published: true
title: Using Charts and React Hooks
summary: The fifth and final post in the series uses the Chart component from KendoReact and shows how to work with React Hooks.
keywords: JavaScript, Kendo UI, Kendo UI for React, KendoReact, React, Web Development
---

Welcome back to our [Getting Started with KendoReact](https://www.telerik.com/blogs/kendo-react-getting-started-blog-series) series! In the fifth and final entry in this series, Eric Bishard illustrates how to use the Chart component from KendoReact and work with React Hooks. See what KendoReact can do for you, the React developer!

Back to the [fourth post](https://www.telerik.com/blogs/kendoreact-customizing-components) of the series.

* * *

# Pt 5\. KendoReact Charts and React Hooks

We are going to add a [Chart](https://www.telerik.com/kendo-react-ui/components/charts/chart/) directly below the the existing Grid component. The link I just gave you for the chart is a great place to get a better understanding of the different ways you can customize it. Now, when we want to add any type of chart (sprakline, pie, donut, whatever), we start by installing the Kendo Chart package and another dependency called `hammerjs`

    npm install @progress/kendo-react-charts hammerjs

One thing I want to do here is use the latest addition to the React library (Hooks), but we'll need to update our React packages to use 16.7 Alpha. Let's install that now:

    npm install react@next react-dom@next

If you ever want to get the absolute latest bits from React, that's what you should run. Also, we will now see changes in our package.json from:

    "dependencies": {
        [...]
        "hammerjs": "^2.0.8",
        "react": "^16.6.0",
        "react-dom": "^16.6.0",
        "react-scripts": "2.0.5"
      }

    "dependencies": {
        [...]
        "hammerjs": "^2.0.8",
        "react": "^16.7.0-alpha.0",
        "react-dom": "^16.7.0-alpha.0",
        "react-scripts": "2.0.5"
      }

React Hooks give functional components in React the ability to work with React State, perform side effects to state change and tap into React Context. We will simply be using it to manage some simple state inside a functional component. This is what we as developers have wanted from React—it solves problematic issues with Classes and `setState` IMHO. It also allows you to get away from classes in the majority of situations you can run into while building components. If you can get your head around Hooks, you will have much less need for classes in React.

Instead of creating another hunk of HTML and components inside the `App.js` page, let's import a component and move our next block of code outside of the `App.js` page.

In React, this is as simple as creating a file—we'll call ours `PieChartContainer.js` and we will put some very basic functional component structure code in there:

    export default function PieChartContainer() {
      return (
        <div>
          <span>KENDO PIE CHART</span>
        </div>
      );
    }

In the `App.js` page, let's now add an `import` and bring the component into the JSX:

    import PieChartContainer from './PieChartContainer';
    ...
    <PieChartContainer />

Now we can work on bringing in the few imports we need for using Hooks and Kendo Chart component. As well, we will need the HTML that will replace the placeholder div we have in place now.

Here are the imports we will need:

    import React, { useState } from 'react';
    import { Button } from '@progress/kendo-react-buttons';
    import { Chart, ChartSeries, ChartSeriesItem } from '@progress/kendo-react-charts';
    import 'hammerjs';

The first order of business inside the `PieChartContainer` functional component is to set up the default state and handlers for some inputs I'm going to place on the page. Each input will correspond to a state value, and we will have another state value that upon some event, we can update an array of all three pie chart series values. This object will be used eventually in our Pie Chart.

    const [graphProtein, setGraphProtein] = useState(0);
    const [graphCarbs, setGraphCarbs] = useState(0);
    const [graphSugars, setGraphSugars] = useState(0);
    const [seriesData, setSeriesData] = useState([
      graphProtein,
      graphCarbs,
      graphSugars
    ]);

    const handleGraphProteinChange = (e) => {
      setGraphProtein(isNaN(e.target.value) ? 0 : e.target.value)
    }
    const handleGraphCarbsChange = (e) => {
      setGraphCarbs(isNaN(e.target.value) ? 0 : e.target.value)
    }
    const handleGraphSugarsChange = (e) => {
      setGraphSugars(isNaN(e.target.value) ? 0 : e.target.value)
    }
    const handleSeriesDataChange = (e) => {
      setSeriesData([graphProtein, graphCarbs, graphSugars])
    }

We will also replace the span placeholder element on our page with the following code, which I created as a precursor to putting our chart on the page. I wanted to make sure I understood what I expected from the user and how I could take those inputs and translate them into a condensed array of each value to feed into the chart, this is just how I work things out when I'm manually prototyping:

    <div>
      <p>Protein Amount: -
        <input value={graphProtein} onChange={handleGraphProteinChange} />
      </p>
      <p>Carb Amount: -
        <input value={graphCarbs} onChange={handleGraphCarbsChange} />
      </p>
      <p>Sugar Amount: -
        <input value={graphSugars} onChange={handleGraphSugarsChange} />
      </p>
      <Button primary={true} onClick={handleSeriesDataChange}>Update Pie</Button>
      <p>
        Protein Value is: {graphProtein}, 
        Carbs Value is: {graphCarbs}, 
        Sugars Value is: {graphSugars},
        Series Data is: {seriesData}
      </p>
    </div>

Now let's drop in some basic code to get the chart displaying on the page, I took some code from the KendoReact Charts component example and modified to fit my needs:

    <div className="food-graph">
      <Chart seriesDefaults={this.state.seriesDefaults} series={this.state.series}></Chart>
    </div>

We need to pass some `state` into the chart. We will have a `series` and `seriesDefault` that we will bind to our properties on the `state` object.

I'm going to give you some more HTML to add directly above the chart and it's surrounding `food-graph` div and create a sibling div for `food-graph-inputs.` We're going to enable our users to add some numbers to three sections of our chart, each of which will be a pie chart to represent those numbers. This allows us to visualize the difference between the proteins, sugars and carbs from our grid.

    <div className="food-graph-inputs">
      <p>Protein Amount: - 
        <input type="text" onChange={this.handleProteinChange} />
      </p>
      <p>Carb Amount: - 
        <input type="text" onChange={this.handleCarbChange} />
      </p>
      <p>Sugar Amount: - 
        <input type="text" onChange={this.handleSugarChange} />
      </p>
    </div>

And with these changes made, we will need to update our `state` object to supply the default values for `series`, `seriesDefault`, `graphProtein`, `graphCarb` and `graphSugar`. Our state should end up looking like the object below:

    this.state = {
          data: this.getNutrition(initialFilter),
          filter: initialFilter,
          habitId: 0,
          habitName: '',
          habitIteration: 0,
          habits: [],
          habitsOptions: [
            'Drink 1 cup of water',
            '1 Hour of Coding',
            '10 pushups',
            'Eat Your Fruits and veggies',
            '1 hour of Reading',
            '10 minutes of Meditation',
          ],
          series: [{data: [1,1,1]}],
          seriesDefaults: { type: 'pie'},
          graphProtein: 0,
          graphCarb: 0,
          graphSugar: 0
        }

We need a few functions to handle any changes to the `protein`, `carb` and `sugar` input changes, each will also need to call a `handleGraphChange()` function after setting their own state. Let's add those four functions now at the bottom of all of our function handlers.

    // Chart Functions
      handleProteinChange = (event) => {
        this.setState({ graphProtein: event.target.value });
        this.handleGraphChange();
      }
      handleCarbChange = (event) => {
        this.setState({ graphCarb: event.target.value });
        this.handleGraphChange();
      }
      handleSugarChange = (event) => {
        this.setState({ graphSugar: event.target.value });
        this.handleGraphChange();
      }
      handleGraphChange = () => {
        this.setState({ 
          series: [{
            data: [
              this.state.graphProtein,
              this.state.graphCarb,
              this.state.graphSugar
            ]
          }]
        });
      }

* * *

This is the end of the series! Did you miss any of the five posts? Check out the [overview post](https://www.telerik.com/blogs/kendo-react-getting-started-blog-series) and get caught up.