---
published: true
title: How to Add React Form Validation
summary: Get up to speed creating your own custom form validation in React components.
keywords: JavaScript, React, Forms, validation
---

This article will take you through the basics of working with forms in React and using controlled state inside of components. We also use the concept of encapsulation and cover how to build your components with classes then we convert that same code to use functional components and Hooks!

Our starting point will be a simple Create Account form in a modal:

![Initial Form](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/initialform.png?sfvrsn=c14c7780_0 "Initial Form Look and Feel")  

It's simple enough yet still have different types of requirement for name, email and password.

I will be adding some CSS and HTML in the starter StackBlitz demo that is pre-styled as teh tutorial mostly focuses on forms and validation.

The `<dialog>` modal was considered, but not used in this tutorial, you can find information on how to use in all browsers with a polyfill [here](https://alligator.io/html/dialog-element/). But this way of building modals does not work in all browsers, so we will use a regular div or semantic tag that makes sense for the job.

If you are here to learn specifically how to use form validation with the [KendoReact](https://www.telerik.com/kendo-react-ui/components), that is a different topic and can be found here: [Getting Started with KendoReact Form validation](https://www.telerik.com/kendo-react-ui/components/forms/getting-started/).

Instead we are going to learn about custom validation using basic forms and our own logic, I feel this is the right place to start, as React developers we need to know how to do these things ourselves, that knowledge will come in hand when using out of the box components, but in our React learning series we'd rather tackle this issue on our own from scratch.

This is a beginner to intermediate tutorial and you should have familiarity with HTML, CSS and some knowledge of how to use React. Let's get started. We are going to start with the following StackBlitz demo:

[react-forms-validation-start](https://stackblitz.com/edit/react-forms-validation-start?file=index.js)

One of the things to notice in the form I have setup for you is that we have specified three different types of inputs. We have a `fullName`, `email` and `password` input. It's very important to use the right type on each input as the behavior it provides is what users expect with a professional form. It will assist their form fillers and allow for an obfuscated password which is also pretty standard.

We are going to build up from this point and add some custom code to help submit and validate the form. Currently the form does not submit or work in anyway, it is has only been styled.

The first thing we want to add is a constructor to our in the **Register component**:

    constructor(props) {
      super(props);
      this.state = {
        fullName: null,
        email: null,
        password: null,
        errors: {
          fullName: '',
          email: '',
          password: '',
        }
      };
    }

Here we have a piece of state for each form input as well as an object called `error:` which will hold the text for our error messages that we will display to the user if they enter an invalid input.

Let's start with the `handleChange()` function. All this function is responsible for is to check if we are in a good or bad state for that form input entry. This function will contain a switch statement. If I put my cursor in the `fullName` field and since we are using the `onChange` prop attribute in our inputs, this function will get called and pass our function an event. This event will have a `name` and a `value` property inside of an event object. We are going to first [destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) and pluck those values out of the `event.target` object and assign them to local variables(`name` and `value`).

So the line of code below:

    const { name, value } = event.target;

is equivalent to:

    let name = event.target.name;
    let value = event.target.value;

With that out of the way and assuming that you have some experience with basic switch statements our entire `handleChange()` function should come right before the render inside of our **Register class**:

    handleChange = (event) => {
      event.preventDefault();
      const { name, value } = event.target;
      let errors = this.state.errors;

      switch (name) {
        case 'fullName': 
          errors.fullName = 
            value.length < 5
              ? 'Full Name must be 5 characters long!'
              : '';
          break;
        case 'email': 
          errors.email = 
            validEmailRegex.test(value)
              ? ''
              : 'Email is not valid!';
          break;
        case 'password': 
          errors.password = 
            value.length < 8
              ? 'Password must be 8 characters long!'
              : '';
          break;
        default:
          break;
      }

      this.setState({errors, [name]: value}, ()=> {
          console.log(errors)
      })
    }

The code above will enter into the correct switch case depending on which input you are typing in. It will check that you have entered the correct length for that input or in the case of the email, it will check a RegEx that we still need to create and ensure that it matches the regular expression that checks for a proper enough email format.

We will not get into Regular Expressions, however; I got my expression from a [StackOverflow answer](https://stackoverflow.com/questions/46155/how-to-validate-an-email-address-in-javascript#answer-46181) which showcases a few decent RegEx solutions for validating emails. We will use the RegEx string I got from that StackOverflow answer.

Just above our **Register class** we can add a `const` that holds this RegEx and then we can call `.test()` on that RegEx string to see if our input matches and returns true, otherwise we will add an error message to our local copy of our error state.

    const validEmailRegex = 
      RegExp(/^(([^<>()\[\]\.,;:\s@\"]+(\.[^<>()\[\]\.,;:\s@\"]+)*)|(\".+\"))@(([^<>()[\]\.,;:\s@\"]+\.)+[^<>()[\]\.,;:\s@\"]{2,})$/i);

The RegEx is nearly impossible to read, but rest assured it covers most cases that we want to check including accepting unicode characters. Understand that this is just a test we perform on the front end and in a real application you should test the email on the server-side with legit validation depending on your requirements.

This is a great spot to stop and check our work, in fact most of our validation is already working, if we go into our console for this page we can see what error messages are being created up until we satisfy each inputs validation:

![Validate Full Name](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/validate-fullname.gif?sfvrsn=4846e806_0 "Validate Full Name")  

As you can see, as soon as we enter our first character in the `fullName` input, we get an error message. The `fullName` input requires that we enter at least 5 characters. We see that in our console up until we meet the criteria, then the error message disappears. Although we will not continue logging these errors in the console, we will pay attention in future code to the fact that we either have an error message or not. If so, we will figure out a better way of displaying this to the user.

We have come pretty far in just a short amount of time, if you are following along your StackBlitz demo should be similar to the following StackBlitz below which is exactly where we have left off, if not, take a few minutes to look over the demo below and either update your own work or fork a new copy from the demo below:

[react-forms-validation-01](https://stackblitz.com/edit/react-forms-validation-01?file=index.js)

Our next order of business is to handle a form submission and provide a function that upon form submission can check to see if we have any error messages present to show the user. If so, we will stop them from being able to successfully submit.

Considering our `handleChange()` function is already updating our local component state with errors, we should already be able to check for validity upon form submission with a simple function we will call `handleSubmit()`. But first I want to remove the `consloe.log` statement inside the `setState` call. Let's update that line at the bottom of the `handleChange()` function to read:

    this.setState({errors, [name]: value});

Now, we will create the new `handleSubmit()` function and for the time being, we will console log a success or fail message based on the validity of the entire form. Add the following code just below the `handleChange()` function.

    handleSubmit = (event) => {
      event.preventDefault();
      if(validateForm(this.state.errors)) {
        console.info('Valid Form')
      }else{
        console.error('Invalid Form')
      }
    }

In our handler for the submit event, we need to stop the event from bubbling up and trying to submit the form to another page which causes a refresh and then posts all of our data appended to the web address. The line of code that does this is `event.preventDefault()` and if you have not used it before, you can read up on it here: [React Forms: Controlled Components](https://reactjs.org/docs/forms.html#controlled-components). This is one of the better resources that explains why it's needed in a React (SPA) form.

As you can see from the code above, we also need to add a function called `validateForm` in which we call out to in order to check validity, we then display a console message of valid or invalid. We will add this function just below the RegEx we created:

    const validateForm = (errors) => {
      let valid = true;
      Object.values(errors).forEach(
        // if we have an error string set valid to false
        (val) => val.length > 0 && (valid = false)
      );
      return valid;
    }

At this point we should be able to fill out the entire form and check validity.

![Validate Form](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/validate-form.gif?sfvrsn=8d99c9a1_0 "Validate Form")  

We are getting close to the home stretch, we have a form that submits and determines if we have met the criteria for each input and we have the ability to return a valid or invalid state. This is good!

Inside of our **Register component's** render and before the return, we need to destructure our `this.state.errors` object to make it easier to work with.

    const errors = this.state;

This will allow us to write some pretty simple logic below each input field that will check if the error message for that field contains a message, if so we will display it! Let's write our first one underneath the `fullName` input.

    {errors.fullName.length > 0 && 
      <span className='error'>{errors.fullName}</span>}

Now lets do the same underneath the next two inputs, first the email input:

    {errors.email.length > 0 && 
      <span className='error'>{errors.email}</span>}

And next we will do the password input:

    {errors.password.length > 0 && 
      <span className='error'>{errors.password}</span>}

And just like that we should have our entire form working and alerting the user to any errors so long as we have touched the individual inputs. The current logic should keep from showing our error messages until we start typing in the input as well, if we back out of an input and remove all text that we have typed, the error messages will remain as they have been touched and are now invalid. Let's take a look at the form in action:

![Final Form](https://d585tldpucybw.cloudfront.net/sfimages/default-source/default-album/final-form.gif?sfvrsn=df51bc12_0 "Final Form") 

A few things you could above and beyond what we have done here, is to instead of adding a span underneath the input when the form becomes invalid, we could have the span always there and just display it using a CSS class if it's invalid. What's the difference? Well it would help to get rid of the jump when the error message arrives and disappears.

Also we could just have a large section at the bottom that displays all known errors only upon hitting the submit button. These are all great ideas and things you should explore on your own now that you have a better understanding of how to validate a form.

I want to give a few shout outs to resources I used along the way to develop this form. First and foremost, the React documentation is always my first stop to figure this stuff out. But I also was heavily influenced by a few YouTubers and pulled bits and pieces from several tutorials to create this one. First is a channel called [Code Life](https://www.youtube.com/channel/UC9nBRXEi-gthsZf8BBhp_Jw) who was the biggest inspiration for this form, I do some things differently than him and provide you with working StackBlitz demos, but I must give his channel a huge plug because I feel his methods of setting up validation is easiest to understand and learn. Also I have a few other YouTube channels that have helped me learn so many new things in React and I'm planning a part two that utilizes hooks instead of using classes. The channels that have really helped me understand Hooks better are [Ben Awad](https://www.youtube.com/user/99baddawg), [Kent C Dodds](https://www.youtube.com/user/kentdoddsfamily) and [Traversy Media](https://www.youtube.com/user/TechGuyWeb). Please check out these channels and let them know if their content helps you out as much as it did me!

Finally, I want to link below to the final version of our form so that you can take it from here and maybe add some better styles and additional validation if you like. Thanks for taking the time to learn here with me and remember that we have KendoReact components that make form validation a breeze, try them out [here](https://www.telerik.com/kendo-react-ui/components)!

[react-forms-validation-02](https://stackblitz.com/edit/react-forms-validation-02?file=index.js)