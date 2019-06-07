<span class="featured">We recently hosted a webinar that highlighted the latest features in the R2 2019 release of KendoReact. Below is a summary of the webinar as well as answers to some of the questions that were asked.</span>

The [KendoReact](https://www.telerik.com/kendo-react-ui) R2 2019 release is packed with new components and features. To get access to these features, one simply needs to install the latest version of the individual KendoReact packages. The [latest bits can be seen here](https://www.telerik.com/kendo-react-ui/components/changelogs/ui-for-react/), but we also cover all updates that have been released since our last webinar (R1 2019)!

![KendoReact](https://i.imgur.com/98vqeAu.png)

In case you missed it, here's a summary of the top highlights that we covered during the webinar:

*   [Xxxx](Xxxx)
*   [Xxxx](Xxxx)
*   [Xxxx](Xxxx)
*   [Xxxx](Xxxx)
*   [Xxxx](Xxxx)
*   [Xxxx](Xxxx)
*   [Xxxx](Xxxx)

A more in depth review of the latest features can be read in our [What's New in KendoReact R2 2019](https://www.telerik.com/blogs/whats-new-in-kendoreact-with-r2-2019) article by Carl Bergenhem!

## KendoReact R2 2019 Webinar

Hosts: [Eric Bishard](https://twitter.com/httpjunkie), [John Bristowe](https://twitter.com/johnbristowe) and [Carl Bergenhem](https://twitter.com/carlbergenhem). Don't worry if you didn't get a chance to watch it live. We've posted it to our YouTube channel. In fact, you can watch it now!

<iframe width="560" height="315" src="https://www.youtube.com/watch?v=FJr2eUT0tf0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen=""></iframe>

## Webinar Prize Winner

During the webinar, we asked attendees to ask questions and offered a free KendoReact license as a prize for the best one. The winner is **Harry Singh**. Congratulations and thanks for your great question!

## Webinar Questions and Answers

**Is KendoReact a wrapper of Kendo UI jQuery components or React components created from scratch?**
The KendoReact components have all been written completely from scratch specifically for React - no dependencies!

**Is there a KendoReact scheduled component? If not, will there be?**
It's on our immediate [KendoReact Roadmap](https://www.telerik.com/kendo-react-ui/roadmap/)! 

**Is there a more detailed development Roadmap.  I've found this (https://www.telerik.com/kendo-react-ui/roadmap/) but I'd really like to see something more detailed if possible?**  
We will be updating this roadmap page to provide more details over the next couple of days!

**Is it possible to click a button that will add a new row to the grid and also removing a row from the grid when clicking on a remove button?**  
Our Grids support all types of data binding. It's completely possible to update and remove rows/items from a collection that is tied to the output of the grid.

**Are there any plans to add an accessibility checker to the WYSIWYG editor, so that end users can make sure their edits are accessible??**  
Currently, this is not on the KendoReact Roadmap, if you could elaborate on our public [feedback portal](https://feedback.telerik.com/kendo-react-ui).

**Any plans to bring react native into the mix?**  
Currently, we do not have immediate plans for React Native UI components, but we certainly are chatting about React Native and what is possible from a UI standpoint, It's questions like this that keep these ideas fresh in our head, Thank you for participating today and asking great questions!

**Is there any nested grid available in Kendo react?**  
Yes, you can check out the [Master-Detail Grids demo](https://www.telerik.com/kendo-react-ui/components/grid/advanced-features/hierarchy/)  

**Can you remove the obligatory placeholder (e.g. "day/month/year") from the date inputs?**  
I think what you want to do is 'format' that date input placeholder differently. In order to do that, you can check out the [Placeholders Documentation](https://www.telerik.com/kendo-react-ui/components/dateinputs/dateinput/placeholders/) page.

**About how difficult is it to integrate KendoReact into an ASP .NET C# MVC project?** 

Anywhere that you can run React, you can run KendoReact components. However, I have a few links you can check out on YouTube that are not ancient and show how to setup React in ASP.NET MVC ([one](https://www.youtube.com/watch?v=myoghjBrTbU), [two](https://www.youtube.com/watch?v=bnFgGYooDCM), [three](https://www.youtube.com/watch?v=myoghjBrTbU).

**Is there a drop target to go along with the new draggable?**  
No, it's fairly easy to track the last coordinates of the Draggable selected and when released by the user. The ability to set those coordinates I have exposed in a [Draggable StackBlitz Demo](https://stackblitz.com/edit/kendoreact-r2-2019-draggable?file=app/main.jsx) altered version of our draggable demo. I do understand if this is not what you are looking for and can say that if you have ideas for the Draggable API, please visit our public [feedback portal](https://feedback.telerik.com/kendo-react-ui).

**Can we format the date in the textbox for DateTime control. Currently it's showing as dd/mm/yyyy but suppose if I want to show it as dd/MMM/yyyy after date selection?**  
I have set up a [StackBlitz DateTime Demo](https://stackblitz.com/edit/kendoreact-r2-2019-date-time-picker-format?file=app/main.jsx) to show exactly how to do this, the DateTimePicker has a prop named format, which you can simply pass the string`dd/MMM/yyyy` and you get the three letter month instead of the two digit month. 

**Is the Virtual scroll for the KendoReact Grid pagination server side or client side?**  
It can be both. Depends on where you are loading your data from and how you want to handle it. The Grid itself does not necessarily bind directly to your server-side logic, so whatever you have in terms of a data fetching setup (full client-side, or server-side) will work for virtualization.

**Is there any option available to take a screenshot like capturing screen on button click and ask to attach and send an email?**  
No, but if this is something you feel would make a great component as part of KendoRact, let us know on the public [feedback portal](https://feedback.telerik.com/kendo-react-ui).

**Does the pure Kendo React grid now implement all the functionality of the jQuery grid wrapper?**  
At this point, it would be some smaller features here and there, but overall we cover the same features (if not more when thinking about column virtualization) and you should be safe to migrate over.

**Is that Kendo React component [StoryBook](https://storybook.js.org/) available somewhere? (I missed the link if there was one)?**  
John Bristowe has that [on his private repo](https://github.com/jbristowe/kendoreact-storybook), so you should go fork it and open up the project locally, it's pretty cool and a great way to learn StoryBook!

**I use the Kendo UI for jQuery and Kendo UI for Angular, but I am not able to find the same component in react ?**  
All of these libraries are evolving naturally based on feedback. If a component is missing definitely let us know by submitting feedback on our public [feedback portal](https://feedback.telerik.com/kendo-react-ui).

**Any way to subscribe to your releases so we know the latest and greatest first thing?**  
I'd recommend the [KendoReact changelog](https://www.telerik.com/kendo-react-ui/components/changelogs/ui-for-react/).

**We use Kendo jQuery right now will I be able to seamlessly transition to the react editor?**  
There's a lot of feature parity between the Editor widget in Kendo UI for jQuery and the Editor component in KendoReact. Most of the features are available for both libraries.

**The Date Time Picker and Date Pickers and Time Pickers have that default value of month/day/year is there any way to make that empty, its kind of an eye sore in my app that it has a placeholder text and my others just have the label for the input?**  
Currently we always show the placeholder. We'd love to implement it so make sure to list this as a feature request in our public [feedback portal](https://feedback.telerik.com/kendo-react-ui).

**Where can I see more about columnVirtualization?**  
You can check it out on our [Grid Page](https://www.telerik.com/kendo-react-ui/components/grid/columns/column-virtualization/)

**We have been developing a project since 2017 when only Kendo React Wrappers available. What do you suggest - whether we should re-write it with components or will keep it that way?**  
You may not need to re-write those parts that work. You could keep your[Kendo Wrapper Components (deprecated)](https://docs.telerik.com/kendo-ui/third-party/react#react) the way they are and then use our native components for the new bits. It's fine to use them both in the same project, but we strongly advise using the new [KendoRact components](https://www.telerik.com/kendo-react-ui/components/) for all new development!

**Concerning the KendoReact Input component - If I set the value prop then it becomes read-only. I can't use defaultValue props as defaultValue can only be set once on load, on subsequent rendering through the state changes the default value is the same. Any fix over that in this release?**  
Once setting the value prop, the component enters a controlled state. In order to keep the component in a controlled state, you must handle the `onChange()` event and pass the new value property.

**when we use wrappers and components together won't be there a CSS conflict?**  
The components share CSS. One theme can work across multiple Kendo libraries :)

**What would you suggest as a UI testing framework which best fits my react app development along with Kendo UI?**  
We believe one of the better testing libraries out there for React developers is Kent C Dodd's [React Testing Library](https://github.com/testing-library/react-testing-library). There are videos on Egghead to help you get acquainted with it, as well there is a [good blog post](https://kentcdodds.com/blog/introducing-the-react-testing-library) on the authors' blog!

**What about a wizard or progress bar component?  Do you have those in KendoReact?**
We do not have them added yet, but the progress bar is at least on our short list and should arrive later in 2019! As for the wizard component we recommend submitting this as a feedback item to our public [feedback portal](https://feedback.telerik.com/kendo-react-ui).

**I wrote a web app when KendoReact it first came out ( version 0.4.0 ), are there any instructions upgrading from 0.4.0 to 3.1.0? Or can I just update the library and it should work?**
We now require React 16.8 or latest version of react. Let us know if you're having any problem and we'd be happy to help. Otherwise, the most notable changes in our components were updates to the API and properties of [KendoReact Grid](https://www.telerik.com/kendo-react-ui/components/grid/). 

**Do you have any options for adding any type of animations to the components?**
We have a dedicated Animation package which is used internally across [all KendoReact components](). You can also use them as a standalone component. https://www.telerik.com/kendo-react-ui/components/animation/

**Are there any plans to add a Drawer Component to KendoReact?**
Yes! More news in the coming months on this and other components and feature news. Keep an eye on the [KendoReact changelog](https://www.telerik.com/kendo-react-ui/components/changelogs/ui-for-react/) also!

**Have recent grid updates added features that make it easier to work with the Grid in Responsive designs, such as on the fly hiding of columns?**
Carl B: Certainly! It's very easy to work with a column collection to determine what to show or hide to control this. We're actively working in a sample to make this easier to follow with responsive scenarios but there's no issue with doing that already today. If you need some assistance in this definitely reach out to our support team for help!

Eric B: Since props can be bound to state that is dynamic and representative of the current breakpoint, we can make decisions off these values and update the render. This gives me the opportunity to shut things off, change the way they are displayed, etc. But nothing added to the grid that has to do with rendering it responsively. We are always tweaking the performance of our components and we strive to make them work well at any resolution and/or device.

**Is there a place on the Kendo React website that lists the Kendo release and which minimum React release that is supported??**
Right now this is a bit hidden across various articles, but we will make this easier over the next couple of weeks by creating a "system requirements" page to help not only with the React version but any other items we can think of (browser support, etc.). We want to ensure that this info is easier to find :)

**What is the Kendo YouTube channel?**  
[Kendo UI TV](https://www.youtube.com/user/kendouiTV)

## Thank You

Thanks to everyone who joined us for the webinar, we received a lot of great feedback. We hope you love the new components, features and improvements we've made to KendoReact. Leave feedback through our [Feedback Portal](https://www.telerik.com/support/feedback) or in the comments below.