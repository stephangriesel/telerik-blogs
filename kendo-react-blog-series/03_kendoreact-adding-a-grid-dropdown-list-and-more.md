---
published: true
title: Adding KendoReact Grid, Dropdown List and More
summary: In the third part of our Getting Started with KendoReact series, Eric Bishard shows off how to use some of our most popular KendoReact components in a React app.
keywords: JavaScript, Kendo UI, Kendo UI for React, KendoReact, React, Web Development
---

Welcome back to our [Getting Started with KendoReact](https://www.telerik.com/blogs/kendo-react-getting-started-blog-series) series! In the third entry in this series, Eric Bishard shows off how to use some of our most popular KendoReact components in a React application. See what KendoReact can do for you, the React developer!

Back to the [second post](https://www.telerik.com/blogs/kendoreact-creating-robust-react-applications) of the series.

* * *

# Pt 3. Adding Grid, Dropdown List and More

I want to address the components that we're planning to use in this project. First of all, we're going to be making a place where users can add a healthy goal and and add a value for the number of iterations for the healthy habit. Kind of like a to-do list, but with a number of times to complete, for the number of times we add that we want to do this task, we will get a radio button rendered for us to check.  

Then, we will be creating a grid that contains nutritional information about fruits and vegetables, which we will later work on filtering in different ways. Let's get started with the forms and components needed for the to-do list. We will first be playing with the Grid, DropDowns, NumericTextBox and Buttons.

### Documentation for Each Component

[Grid](https://www.telerik.com/kendo-react-ui/components/grid/), [DropDowns](https://www.telerik.com/kendo-react-ui/components/dropdowns/), [NumericTextBox](https://www.telerik.com/kendo-react-ui/components/inputs/numerictextbox/), [Button](https://www.telerik.com/kendo-react-ui/components/buttons/)

Let's import the components into our pages. First, we'll add the grid and it's associated components inside of our `App.js` file. The `DropDownList`, `NumericTextBox`, `Grid` and`GridColumn`. By scoping out the documentation, it's apparent I will need the following import statements.

    import { DropDownList } from '@progress/kendo-react-dropdowns'; import { NumericTextBox } from '@progress/kendo-react-inputs'; import { Button } from '@progress/kendo-react-buttons'; import { Grid, GridColumn } from '@progress/kendo-react-grid';

Now that we have the imports we need, let's also get some data (nutritional information) to feed our Grid, the json with that data can be found here: [nutrition.json](https://github.com/tzmanics/kendoui-react-video-series/blob/master/src/nutrition.json), copy that code into a file named `nutrition.json`, and add that to our `src` directory.

> Copying from a GitHub file can be tricky. Visit the `nutrition.json `GitHub[](https://github.com/tzmanics/kendoui-react-video-series/blob/master/src/nutrition.json)link above and hit the edit icon on the page. This will create a fork of the file and open it in edit mode, this is the best way to copy the large amount of code inside without getting additional formatting we don't need.

After adding the `nutrition.json` file, we need to import it into our `App.js` file.

    import nutrition from './nutrition.json';

Next we add a constructor, giving us a place to assign our nutrition data to a property on our project's `state` along with some options for our drop-down. The constructor goes right above the render function in our App class:

    constructor(props) {
      super(props)
      this.state = {
        data: nutrition,
        habitsOptions: [
          'Drink 1 cup of water',
          '1 Hour of Coding',
          '10 pushups',
          'Eat Your Fruits and veggies',
          '1 hour of Reading',
          '10 minutes of Meditation',
        ]
      }
    }

Now let’s update our HTML in preparation for our nutritional information grid:

    <div className="App" >
      <h1>Healthy Things</h1>
      <div className='healthy-habits'>
      </div>
      <div className='add-habits'>
        <DropDownList data={this.state.habitsOptions} />
        <NumericTextBox />
        <Button>Add Habit</Button>
      </div>
      <div className='nutrition-grid'>
        <Grid data={this.state.data}>
          <GridColumn field='Description' title='Food' />
          <GridColumn field='Measure' title='Amount' />
          <GridColumn field='Protein(g)Per Measure' title='Protein' />
          <GridColumn field='Carbohydrate, by difference(g)Per Measure' title='Carbs' />
          <GridColumn field='Sugars, total(g)Per Measure' title='Sugars' />
        </Grid>
      </div>
    </div>

Let's also add a bit of padding to our `App` class, go into our `App.css` and add make sure the only CSS we have in that file for now is the CSS below:

    .App {
      padding: 1em;
      text-align: center;
    }
    .healthy-habits ul {
      list-style-type: none;
    }

Now we should have a dropdown, numeric textbox and an "Add Habit" button above our grid that is now populated with our nutrition data. Also take note how our data is mapped to each `GridColumn` using the `field` attribute.

Things are coming along, so let's take a look at what we have so far..

![Grid Version One](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/gridversiononeb6adb87e229d4d5b84cfab4b4abb1e11.gif?sfvrsn=f33f5508_1 "Grid Version One")  

* * *

Check out the [fourth post](https://www.telerik.com/blogs/kendoreact-customizing-components) of the series, [KendoReact: Customizing Components](https://www.telerik.com/blogs/kendoreact-customizing-components).