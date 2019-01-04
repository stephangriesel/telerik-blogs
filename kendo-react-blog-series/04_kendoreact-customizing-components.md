---
title: Customizing Components
summary: In the fourth post, Eric demonstrates how to customize the Grid component.
keywords: JavaScript, Kendo UI, Kendo UI for React, KendoReact,React, Web Development
---

Welcome back to our [Getting Started with KendoReact](https://www.telerik.com/blogs/kendo-react-getting-started-blog-series) series! In the fourth entry in this series, Eric Bishard illustrates how to customize the KendoReact Grid component in a React application. See what KendoReact can do for you, the React developer!

Back to the [third post](https://www.telerik.com/blogs/kendoreact-adding-a-grid-dropdown-list-and-more) of the series.

* * *

# Pt 4\. Customizing KendoReact Components

The first thing that we're going to look into is the [NumericTextBox](https://www.telerik.com/kendo-react-ui/components/inputs/numerictextbox/). We do have a [DropdownList](https://www.telerik.com/kendo-react-ui/components/inputs/dropdowns/) first, but we already added the data for that list already.

Our NumericTextBox is not looking exactly how we want it to. Out of the box, there is no restriction on what numbers can be used, including negative numbers and decimals. We can't eat a negative amount of fruit and vegetables. As many times as I want to only halfway do my tasks, we don't want the value to be a decimal. This value will become a set of radio buttons for each habit that we create, so this value needs to be a whole number.

The first thing we need to do is formatting. To set the format to not allow decimals, we set a prop input ( `format` ) to 0\. There are other formats to choose from. For instance, you can add C to format the input as currency. `0` is all we need.

    <NumericTextBox format="0"/>

In the [documentation for the NumericTextBox](https://www.telerik.com/kendo-react-ui/components/inputs/numerictextbox/), there are all the different format types that you can explore. There's also an [API](https://www.telerik.com/kendo-react-ui/components/inputs/api/NumericTextBox/) that you can go through and check all the ways you can customize this input.

Next, we need to set `min` to zero so that our users cannot input any negative numbers, and just for the heck of it, we'll also set `max` to 22.

    <NumericTextBox
      format='0'
      min={0}
      max={22}
    />

Now that we have the NumericTextBox set up, let's run the app. With the built-in keyboard navigation, we can raise or lower the amount with the arrow keys so long as the number is between 1 and 22.

Next, we want to be able to click the add button and create a new habit. In order to make this work, we will need to add event listeners to our inputs and button to call handlers that will update our application, in turn creating a list of healthy habits.

Before we do that, let's add some information to our state: `habitName`, `habitId`, `habitIteration` and an array of `habits`. Our state object needs to be updated as follows:

    this.state = {
       data: nutrition,
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
       ]
     }

So we added a `habitName` with an empty string (intentionally left blank), and a `habitId` set to `0`. We're using this to set a key that we need for every list item. Then we added a `habitIteration` with an initial state of zero. Finally, we add a `habits` field initializing as an empty array.

> Remember, we are just prototyping. Understand that keeping all of our state inside the `App.js` file and updating state manually is definitely not something you want to do in a scalable production app, but my intention is to teach you the Kendo controls, not build a solid production web application. Just remember that in a real-world web app, you would want to incorporate a state management strategy and/or make our application modular by breaking the UI and logic up into many services, containers and presentational components.

Next, onto our handler functions. We will make a `handleNameChange` function, which takes the event from DropDownList as an argument. When this function is triggered we `setState()` to change our habit name. We'll set it to `event.target.value` . We're going to be doing the same with `handleIterationChange()`. Copy the code for the handlers below into your `App.js` file just underneath the constructor.

    handleNameChange = (event) => {
      this.setState({ habitName: event.target.value })
    }
    handleIterationChange = (event) => {
      this.setState({ habitIteration: event.target.value })
    }

Now that we have the handler functions for our event listeners, we can add the change listener to the dropdown list, and numeric text box as well the onClick event that will capture our form submission to add a habit. I also want to add a primary class to the button to make it pop on the page a little more (setting `primary={true}`). With these changes, anytime there's a change in the inputs, it should be immediately reflected in the state, which in turn will update our component. Let's update the inputs and button with these changes:

    <DropDownList
      data={this.state.habitsOptions}
      value={this.state.habitName}
      onChange={this.handleNameChange} />
    <NumericTextBox
      format='0'
      min={0}
      max={22}
      value={this.state.habitIteration}
      onChange={this.handleIterationChange} />
    <Button primary={true}>
      Add Habit
    </Button>

We will also need a list of habits to add to as well as a handler for the button `onClick` event. Let's add an event listener to our button right after we implement a `handleAddHabit()` handler function.

    handleAddHabit = (event) => {
      this.setState({
        habits: this.state.habits.concat([{
          key: this.state.habitId,
          name: this.state.habitName,
          iterations: this.state.habitIteration
        }]),
        habitId: this.habitId++
      });
    }

Since we have `habits` as an array, the first time we add a habit, it will simply add that habit to the array, but for each subsequent operation, we will want to concatenate the new habit being added with the previous habits already existing in the array. We are also adding an iterator as `habitId` so that each habit will have a unique key.

We have an empty `div` tag at the top of our page with a heading that says "Healthy Things"—this is where we will put our list of healthy habits. Copy the code below and replace the empty contents of that `div`.

    <ul key='all-habits'>
      {this.state.habits.map((habit) => [
        <li key={habit.key}>
          <h3>{habit.name}</h3>
          <div className='iterations-area'>
            {[...Array(habit.iterations)].map((iteration, index) => {
              return <input key={index} type='radio' />
            })}
          </div>
        </li>
      ])}
    </ul>

Now we should see our list populated with the information that the user put into our inputs and a radio button for however many times they want to do that habit. This way, they can check them off as they go. Below is a preview of what you should be seeing at this point:

![Add Habit Version One](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/addhabitversionone.gif?sfvrsn=121f2d96_1 "Add Habit Version One")  

The next thing we're going to do is work on making our grid not only look a little bit better, but also add some functionality by giving it the ability to filter. Since we have this never ending grid, we're going to set the height by adding the code below to the `Grid` tag. We save that, and now we no longer have the crazy long grid.

    <Grid data={this.state.data} style={{ maxHeight: '500px' }}>

Now we'll be adding the filtering for our grid. If you recall, in the section where we [installed the Grid and related dependencies](#install-grid-dependencies), one of the packages we installed was a data query module. We installed this module for the specific purpose of filtering our data in our grid. You see, I was thinking ahead for ya! Like I said, it's already available to us through the kendo-data-query package, let's import it!

    import { filterBy } from '@progress/kendo-data-query';

With that in place, we can create a constant right above our state initialization in the constructor. This will serve as an initial filter (default state of the filter), upon our application loading for the first time:

    const initialFilter = {
      logic: 'and',
      filters: [{
        field: 'Description', 
        operator: 'contains',
        value: 'Apple'
      }]
    };

Everything we have setup in this `initialFilter` is something the user will have control over when they are interacting with our grid. The API, and more importantly examples for this, can be found on the [Data Query Overview](https://www.telerik.com/kendo-react-ui/components/dataquery/#toc-filtering). But in short, we are specifying our [logic](https://www.telerik.com/kendo-react-ui/components/dataquery/api/CompositeFilterDescriptor/#toc-logic) to be `and` as opposed to `or`. `field`, (the data item field to which the filter operator is applied) will be **Description** (our first column in the grid), and our [operator for comparison](https://www.telerik.com/kendo-react-ui/components/dataquery/api/FilterDescriptor/#toc-operator) will be **contains** where the description value is **"Apple".**

While we are dabbling in the constructor, we also need to change the `state.data` assignment to come from a function that takes `initialFilter` as an argument returning a data set where `initialFilter` has already been applied to it. After making that change, our state object will look like this:

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
      ]
    }

Considering we have introduced a new function that we have not yet created, let's do that now.

    getNutrition = (filter)  => filterBy(nutrition, filter);

That is enough to get the initial state of the grid working, but we also want the grid itself to be filterable through user interactions. To get this working, let's skip down to the actual `<Grid>` component in our JSX and set a few more things up. Update the `<Grid>` start tag to the following:

    <Grid data={this.state.data} style={{maxheight: '500px'}}
      filterable={true} filter={this.state.filter}
      onFilterChange={this.handleFilterChange}>

Here we have set `filterable` to `true` enabling filtering for the component, `filter` which will point to `state.filter` , and we will also need a handler for the change event `filterChange` . Let's go ahead and set that up because after adding the code above, we now have an error.

    handleFilterChange = (event) => {
      this.setState({
        data: this.getNutrition(event.filter),
        filter: event.filter
      });
    }

So if we take a look at our application, we now have a grid that has filter functionality. For instance, if we change `Apple` in our editable filter to `Orange`, we will see that change take effect immediately in our grid filtering on food descriptions that contain the word `Orange`.  

* * *

Continue to the [fifth post](https://www.telerik.com/blogs/kendoreact-using-charts-and-react-hooks) of the series—_it's not live quite yet, but you'll be able to find it soon!_