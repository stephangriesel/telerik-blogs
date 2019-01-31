## React

React is continuing to dominate the web in 2019. A pretty clear measurement, npm downloads show numbers that indicate Ract is not only holding it's position as the most downloaded and used SPA framework, but it actually shows a healthy growth.

If your not too familiar with React, I would tell you that what sets it apart from other front end frameworks is it's commitment to doing one thing very well. Building Components and managing their state. Most other frameworks like Angular and Ember try to give you everything you need right out of the box, however; React does not try and do this. React focuses on the component model. They let the developer choose their own solution for routing and data models and by doing this it makes the framework more flexible in design and because of these features a higher rate of adoption.

React isn't really a framework, but it's definitely getting frameworkesque features as of late. Lazy loading components, built in state management with added support from React Hooks and things like Suspense are all features I point at to show we are getting these. But it's looked at as more of a solution to one part of the web development process. That one thing it does really well is giving you the abiluty to build components that share state. It is the king of reusable components and it's rather ccontroversial at first but much more respected form of writing HTML using JSX which puts your markup right inside your JavaScript is something that many think should be made a web standard.

![](https://i.imgur.com/JruoIDx.png)

Check out for yourself and play around with the npm trends graph to see how your favorite libraries stack up. The above graph is a screenshot from npm trends where I ran one of the most common trend analysis when it comes to front end frameworks, pitting [React vs Angular vs Vue](https://www.npmtrends.com/angular-vs-ember-source-vs-react-vs-vue) against each other. 

We can see that when it comes to npm downloads, React really does appear to be ahead of the pack. But 2019 will be interesting with the adoption of Vue picking up and amazing stuff coming from the Angular team. In my opinion, this healthy competition is a win/win for everyone. 

As mentioned, React has picked up a gang of support in 2018, but what I would note is that it's actually been on this steady increase since 2014. This next chart is pulled from a talk called ["npm and the future of JavaScript"](https://www.youtube.com/watch?v=mSQh0gcDXkc&t=1168s) and shows React next to Express and Webpack. I wanted to show it's abosolute growth over a longer period of time and this chart helps us to see that relative to other packages seeing similar and in some cases even more growth than React. 

![](https://i.imgur.com/CXCC8XE.png)

I have looked at a lot of the data from StateOfJS.com, StackOverflow surveys, but npm downloads and comparrisons to other frameworks feel like the best indication that React continues to be a force in the JavaScript developer community.

I'm really a big on using npm stats to determine the popularity of the different packages I use in my JavaScript applications, but there are other surveys and polls out there that can help us understand where React has come from 2018 and where it's going in 2019. Specifically, the StateOfJS.com.

This report has valuable information around JavaScript and as a professional it can aid in decision making or just make you happy 😄 or sad 😥 about your favorite framework.

No reason to be sad here though, as React developers we couldn’t be happier with the results. My favorite part of the survey and the place where it's evident to see React is on fire and a force to be reckoned with, is the Front-end Frameworks - Overview.

![](https://i.imgur.com/rezQE5a.gif)

In the image above we can see what frameworks are popular and used or would like to be used by the survey participats. React is a force in the "Used it, would use again" category, but agian, we see that Vue and Angular also have a good showing. I would also say that this survey must be taken with a grain of salt as I feel teh data set may be heavily answered by React developers, partially due to the authors' background and the community the survey stems from. But it's still something we should take into consideration when guaging React's overall popularity.

Another interesting graphic from this survey data is "Most liked aspects of React", which also helps to shine a light on areas where we can improve in React.

![](https://i.imgur.com/2HhmKGj.png)

I think that most issues for why developers dislike React is being addressed somehow in the 2018 releases 16.3 to 16.7. I don’t really feel React has a steep learning curve and I know that the experience is getting better with improvements to the API and tooling around React. 

I spoke in [Bulgaria at the DevReach 2018](https://youtu.be/MfAxhBMTkuQ?t=506) conference about the improvements to React over the course of 2018 and what I think they mean for the future of React. So it’s reassuring to see that the reasons I love React are also reasons others have said they like it too.

You can see more information from the [StateOfJs.com](https://StateOfJs.com) I would like to provide one more graphic, because even though React shows well in this survey, we need to know what things we can make better in the long run so that we continue to see React doing well in the overall JavaScript ecosystem.

<!-- WIP BELOW THIS SECTION  -->

### A State Management Revolution

From the earliest versions of React, there's always been a way of handling state that encouraged a one way data model. But using setState was always tricky for newcomers to React. Even after learning the ropes, it was still possible to introduce bugs when using React Core's own state solution.

![](https://i.imgur.com/XIttY3e.png)

Because setState is asynchronous and the fact that it causes unnecessarry renders in certain situations, and for the fact that sometimes developers didn't know when to use setState vs manage state on their own, it was misunderstood and at a certain point developers would flat out stop using it.

In 2017 and 2018, React Fiber was introduced as React 16, in fact we are still on this same semver major version number now with 16.7 just recently being released. But when the version number was bumped to 16, we got an entire rewrite of the React engine and this rewrite was codenamed React Fiber.

Most of the information around the reason for the rewrite are jammed into several talks that took place at [React Conf 2017](https://www.youtube.com/playlist?list=PLb0IAmt7-GS3fZ46IGFirdqKTIxlws7e0), but this rewrite paved the way for something that I believe will change the way we write React code in 2019. The community has embraced [React Hooks](https://reactjs.org/docs/hooks-intro.html).

Because of the nature of React's one way data flow, and it's close relation to the library Redux, React released an alpha in November of 2018 that redefined how to work with state using the `useState`, `useEffect` and `useReducer` hooks and snatched a play right out of the Redux pattern. This introduction of Hooks is probably the most important and notable change in React and will create the most impact on React in 2019.

Before the introduction of Hooks we had the concept of class components which you could use to build components that needed to manage state and have lifecycle methods and other things that could only be done in classes. One of the drawbacks to prolificly using classes in React or anywhere for that matter is how `.this` is treated. One would have to bind functions and do extraneous work to both provide interaction in the component as well as manage state.

We also had the idea of functional stateless components which provided a much more concise ES6 style syntax for React components boasted no more `.this` keyword and other benefits. It also set the scene for React components to become worldclass. More on that later. When you would create these types of functional stateless components, it typically meant that they would only recieve input (props) and not manage any state. Event though you could not use React's built in state, it was obvious how powerful writing components this way could be, but for the time being the drawbacks were that you couldn't interact with React's state and you couldn't include lifecycle methods. 

To quote Cory House in a [2016 hackernoon article](https://hackernoon.com/react-stateless-functional-components-nine-wins-you-might-have-overlooked-997b0d933dbc): "React stateless functions offer the most elegant approach I’ve seen for creating a reusable component in any popular framework". And it was true. 

React had a hot issue on it's hands in creating Hooks. You see, they had given us a more pure way to write components in a more functional syntax and that required the React developer to think more about composition. Which components will be smart, which ones dumb, etc. This was great to have a period of time where what you could do with these functional components was minimal, it kept you honest and lean.

When React Hooks became available it menat that you could now use Hooks to tap into that React state and lifecycle methods and get all the other benefits as well. The new tools you would use to do this are: `useState` and `useEffects`, they also provided a Hook called `useReducer` which enabled a Redux style pattern for simple UI state management. We now have an abstraction around the `setState()` feature that can incorporate actions, reducers and we can manage that internal UI state in a similar fashion to how we manage our data and it's state within the application.

Back to the first release of 2018, we had something called Context API finally get shipped, it meant we could share data using a provider and allow a tree or groupd of components in our application share the same context. The initial implementation used tags that would allow you to wrap a number of components and provide them all with this context. As you can imagine this was a step in the right direction, but in colex scenarios this can start to breakdown having to wrap providers and consumer tags around areas of the code where you wanted to have access to that context.

Hooks brought us the `useContext` hook and overnight we all breathed a sigh of relief.

Long live Hooks, it's a revolution in React this year, if you don't believe me, wait and see. I write about all of these Hooks and show you the before and after as well as how to work with each of them in the following articles:

[](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects)
[](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context)
[](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context)








### The Biggest Impact on React Considering JavaScript

React has always done things a little bit different than anyone else. The most popular state management library in JavaScript is Redux, which is completely seperate from React in the fact that it is framework agnostic, you can use it with Angular, Vue, React, Vanilla JS, whatever. It's one of the reasons why Redux is so popular, as well we has other tools that although not tied to React, owe their popularity to the fact that they are standard tools for most people building React applications. GraphQL is the along with Redux are finding a great footing in 2019 and dominate usage because of the fact that they are not specific to React.

This is a huge win for the JavaScript community and ecosystem, having tools that are agnostic but also help make up a strong ecosystem around React gets a kind of double bump factor. They are used because they are standard in React, but again their utility is seen by other folks not even using React.

### What Major Changes did 2018 Bring?

In 2018 we bore witness to a major masterplan laid out release by release by the React team. It should be noted that each release was a minor release, meaning the semver in the fact that we never bump the major number of the release which is synonomous with wide breaking changes. Everything they did, they did as minor releases. This is important to note because, in order to roll out the changes that I am going to tell you about and breaking the old way of doing things, the React team ensured that each new features released were, for the most part, backwards compatible and work side by side with existing features.


Below is the React minor releases from 2018

- 16.3 (Mar 29th, 2018)
- 16.4 (May 23rd, 2018)
- 16.5 (Sep 5th, 2018)
- Create React App 2 (Oct 01, 2018)
- 16.6 (Oct 23, 2018)
- 16.7 (Dec 19, 2018)

[NPM Future of JavaScript Slides](https://slides.com/seldo/npm-future-of-javascript#/7):
- JS Facts: JavaScript is the most important programming language in the world
- npm is the package manager for JavaScript
- npm is especially for JavaScript developers
- 97% of the code in a normal webapp comes from npm
- 

### React Facts
- 60% of npm users say they use React
- 
