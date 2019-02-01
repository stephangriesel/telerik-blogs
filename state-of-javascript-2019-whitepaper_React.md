## React

React is continuing to see growth in 2019. A pretty clear measurement is npm downloads which show numbers that indicate React is not only holding it's position as the most downloaded and used SPA framework, but continues to show healthy growth. There are a lot of things I think contribute to this consistent growth but the main thing I believe is React's consistency over the years.

What sets React apart from other front-end frameworks is it's commitment to doing one thing very well. That one thing is components, their composition and managing their state. Other frameworks take a different and more all inclusive approach or try to help the developer get straight to working with the framework with minimal setup, both are features that help propel those frameworks. React, however; is laser focused on the component model. They let the developer choose their own solution for routing and data models and other acoutramonts and by doing this it makes the framework more flexible helps to create a higher rate of adoption.

React isn't really considered a framework, specifically because it's choice to focus on the components, but it's definitely getting framework-esque features as of late. Lazy loading components, built in state management with support from React Hooks and things like Suspense are all features I point out to show we are entering framework territory. But React is looked at as more of a solution to one part of the web development process and even these things I speak about that come out of the box are centered around building reusable components. 

One of React's decisions early on was to use something called JSX, rather controversial at first, it's proven to be a superior form of writing HTML for React components and puts your markup right inside your JavaScript. 

If JSX and React's component model could make for a brilliant model for building universal components in HTML and JavaScript. That very topic is talked about in one of the [latest React Podcast episodes](https://reactpodcast.simplecast.fm/33), saying that React could become transcendent rather than slowly decay like most frameworks by taking the component model that they have introduced and getting it added as a first class construct in browser manufacturers. They note that this is not impossible. But by doing so React could become defacto web technology and achieve transcendence!

With all of the work done around React's components and making them super simple to write using functional components and ES6 style syntax. One could see this transcendence idea come to life, but let's not get too ahead of ourselves yet, most libraries and frameworks have a shelf life of 3 to 5 years. React is knocking at that door now, the question is, will it become transcendent unlike any other frontend framework or will be phased out eventually by new frameworks like Vue?

### React's Range of Application
React's range of applications is wide. You can use it for building desktop apps, mobile apps and of course web apps. Most web frameworks have a hard time breaking into this cross genre development area. Between React, React-Native and even things like [Preact](https://preactjs.com/) (a light version of React), we are seeing React gain the ability to go wherever it wants and it's because of the decisions to not strive to be a framework, it doesn't need a router, data model or anything out of the box that does not contribute to working with components. This is a major attribute of React versus it's closest competitors.

![](https://i.imgur.com/JruoIDx.png)

Check out for yourself and play around with the npm trends graph to see how your favorite libraries stack up. The above graph is a screenshot from npm trends where I ran one of the most common trend analysis when it comes to front end frameworks, pitting [React vs Angular vs Vue](https://www.npmtrends.com/angular-vs-ember-source-vs-react-vs-vue) against each other. 

We can see that when it comes to npm downloads, React really does appear to be ahead of the pack, but this is just one metric. 2019 will be interesting with the adoption of Vue picking up and amazing stuff coming from the Angular team. In my opinion, this healthy competition is a win/win for everyone. In the past few years we have seen all of the major frameworks work with each other, but a healthy amount of competition as we know fuels innovation.

As mentioned, React has picked up a gang of support in 2018, but what I would note is that it's actually been on this steady increase since 2014. This next chart is pulled from a talk called ["npm and the future of JavaScript"](https://www.youtube.com/watch?v=mSQh0gcDXkc&t=1168s) and shows React next to Express and Webpack. I wanted to show it's absolute growth over a longer period of time and this chart helps us to see that relative to other packages seeing similar and in some cases even more growth than React. 

![](https://i.imgur.com/CXCC8XE.png)

A great metric to follow is npm downloads for comparisons to other frameworks and I think is a good indication that React continues to be a force in the JavaScript developer community and continues to be a pick from a popularity standpoint.

I think npm stats are the best thing we have to determine the popularity of the different JavaScript front-end frameworks, but there are other surveys and polls out there that can help us understand where React has come from 2018 and where it's going in 2019. Specifically, the [State Of JavaScript's 2018 survey](https://stateofjs.com).

This report has valuable information around JavaScript and as a professional it can aid in decision making or just make you happy 😄 or sad 😥 about your favorite framework.

No reason to be sad here though, React developers couldn’t be happier with the results. Check out the Front-end Frameworks - Overview.

![](https://i.imgur.com/zRbPVab.png)

We can see what frameworks are popular and used or would like to be used by the survey participant's. In the **"Used it, would use again"** category, React is strong, we see that other frameworks also have a good showing. I would also say that this survey must be taken with a grain of salt as I feel the data set may be heavily answered by React developers, partially due to the authors' background and the community the survey stems from. But it's still something we should take into consideration when gauging React's overall popularity and that still is a measurement many companies look at before making a decision on picking a framework or library, with good reason.

Another interesting graphic from this survey data is "Most liked aspects of React", which also helps to shine a light on areas where the users think the React team could improve upon.

![](https://i.imgur.com/2HhmKGj.png)

I think that most issues for why developers dislike React is being addressed somehow in the minor 2018 releases (16.3 to 16.7). I spoke in [Bulgaria at the DevReach 2018](https://youtu.be/MfAxhBMTkuQ?t=506) conference about the improvements to React over the course of 2018 and what I think they mean for the future of React. So it’s reassuring to see that the reasons I love React are also reasons others have said they like it too.

To get a better overview of how React fared in this State of JavaScript 2018 survey, I have done a rather extensive review and given my own thoughts in a blog post titled: [A React State of Mind (State of JavaScript Survey 2018)](https://www.telerik.com/blogs/a-react-state-of-mind-state-of-javascript-survey-2018)

### A State Management Revolution

From the earliest versions of React, there's always been a way of handling state that encouraged a one way data model. But using setState was always tricky for newcomers to React. Even after learning the ropes, it was still possible to introduce bugs when using React Core's own state solution.

![](https://i.imgur.com/XIttY3e.png)

Because setState is asynchronous and the fact that it causes unnecessary renders in certain situations, and for the fact that sometimes developers didn't know when to use setState vs manage state on their own, it was misunderstood and at a certain point developers would flat out stop using it.

In 2017 and 2018, React Fiber was introduced as React 16, in fact we are still on this same semver major version number now with 16.7 just recently being released. But when the version number was bumped to 16, we got an entire rewrite of the React engine and this rewrite was code named React Fiber.

Most of the information around the reason for the rewrite are jammed into several talks that took place at [React Conf 2017](https://www.youtube.com/playlist?list=PLb0IAmt7-GS3fZ46IGFirdqKTIxlws7e0), but this rewrite paved the way for something that I believe will change the way we write React code in 2019. The community has embraced [React Hooks](https://reactjs.org/docs/hooks-intro.html).

Because of the nature of React's one way data flow, and it's close relation to the library Redux, React released an alpha in November of 2018 that redefined how to work with state using the `useState`, `useEffect` and `useReducer` hooks and snatched a play right out of the Redux pattern. This introduction of Hooks is probably the most important and notable change in React and will create the most impact on React in 2019.

Before the introduction of Hooks we had the concept of class components which you could use to build components that needed to manage state and have lifecycle methods and other things that could only be done in classes. One of the drawbacks to prolifically using classes in React or anywhere for that matter is how `.this` is treated. One would have to bind functions and do extraneous work to both provide interaction in the component as well as manage state.

We also had the idea of functional stateless components which provided a much more concise ES6 style syntax for React components boasted no more `.this` keyword and other benefits. It also set the scene for React components to become world class. More on that later. When you would create these types of functional stateless components, it typically meant that they would only receive input (props) and not manage any state. Event though you could not use React's built in state, it was obvious how powerful writing components this way could be, but for the time being the drawbacks were that you couldn't interact with React's state and you couldn't include lifecycle methods. 

To quote Cory House in a [2016 Hacker Noon Article](https://hackernoon.com/react-stateless-functional-components-nine-wins-you-might-have-overlooked-997b0d933dbc): "React stateless functions offer the most elegant approach I’ve seen for creating a reusable component in any popular framework". And it was true. 

React had a hot issue on it's hands in creating Hooks. You see, they had given us a more pure way to write components in a more functional syntax and that required the React developer to think more about composition. Which components will be smart, which ones dumb, etc. This was great to have a period of time where what you could do with these functional components was minimal, it kept you honest and lean.

When React Hooks became available it meant that you could now use Hooks to tap into that React state and lifecycle methods and get all the other benefits as well. The new tools you would use to do this are: `useState` and `useEffects`, they also provided a Hook called `useReducer` which enabled a Redux style pattern for simple UI state management. We now have an abstraction around the `setState()` feature that can incorporate actions, reducers and we can manage that internal UI state in a similar fashion to how we manage our data and it's state within the application.

### What Major Changes did 2018 Bring?

In 2018 we bore witness to a major master plan laid out release by release by the React team. It should be noted that each release was a minor release, meaning the semver in the fact that we never bump the major number of the release which is synonymous with wide breaking changes. Everything they did, they did as minor releases. This is important to note because, in order to roll out the changes that I am going to tell you about and breaking the old way of doing things, the React team ensured that each new features released were, for the most part, backwards compatible and work side by side with existing features.

We also saw an update to React's most popular CLI tool Create React App, which we covered in detail in our [Hello Create React App 2.0](https://www.telerik.com/blogs/hello-create-react-app-2) article back in October of 2018.

Below is the React minor releases from 2018

- [16.3 (Mar 29th, 2018) New Lifecycles and Context API](https://reactjs.org/blog/2018/03/29/react-v-16-3.html)
- [16.4 (May 23rd, 2018) Pointer Events](https://reactjs.org/blog/2018/05/23/react-v-16-4.html)
- [16.5 (Sep 5th, 2018) React Profiler and Suspense](https://reactjs.org/blog/2018/09/10/introducing-the-react-profiler.html)
- [Create React App 2 (Oct 01, 2018)](https://reactjs.org/blog/2018/10/01/create-react-app-v2.html)
- [16.6 (Oct 23, 2018) Lazy, Memo & contextType](https://reactjs.org/blog/2018/10/23/react-v-16-6.html)
- [16.7 (Dec 19, 2018) Bug fixes and patches (No Hooks yet)](https://reactjs.org/blog/2018/12/19/react-v-16-7.html)

The first release of 2019 should be React 16.8 including the infamous React Hooks we are all waiting for, but don't let that keep you from using them. You can always install the latest React alpha using:

```
npm install react@next react-dom@next
```

Back to the first release of 2018, we had something called Context API finally get shipped, it meant we could share data using a provider and allow a tree or group of components in our application share the same context. The initial implementation used tags that would allow you to wrap a number of components and provide them all with this context. As you can imagine this was a step in the right direction, but in complex scenarios this can start to breakdown having to wrap providers and consumer tags around areas of the code where you wanted to have access to that context.

Hooks brought us the `useContext` hook and overnight we all breathed a sigh of relief.

Long live Hooks, it's a revolution in React this year, if you don't believe me, wait and see. I write about all of these Hooks and show you the before and after as well as how to work with each of them in the following articles:

[React Hooks - State & Effect](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-state-and-effects)
[React Hooks - Context](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-context)
[React Hooks - Reducers](https://www.telerik.com/blogs/how-to-use-basic-react-hooks-for-reducers)

As well, if you are using the KendoReact library in your web development and are looking for a Hooks version of your favorite StackBlitz demos for KendoReact, I have a growing list of demos I have converted to use Hooks over on Dev.to: [KendoReact Components (Functional Hook Style)](https://dev.to/httpjunkie/kendoreact-components-functional-hooks-style-2h2e) as well as an article that encourages developers to get started with Hooks ASAP: [Can I Use react Hooks yet?](https://dev.to/httpjunkie/can-i-use-react-hooks-yet-35o9)

### The Biggest Impact on React Considering JavaScript

React has always done things a little bit different than anyone else. The most popular state management library in JavaScript is Redux, which is completely separate from React in the fact that it is framework agnostic, you can use it with Angular, Vue, React, Vanilla JS, whatever. It's one of the reasons why Redux is so popular, as well we has other tools that although not tied to React, owe their popularity to the fact that they are standard tools for most people building React applications. [GraphQL](https://graphql.org/) is the along with Redux are finding a great footing in 2019 and dominate usage because of the fact that they are not specific to React. Look specifically for GraphQL to make a major contribution to JavaScript and become a prolific way of building APIs in 2019.

This is a huge win for the JavaScript community and ecosystem, having tools that are agnostic but also help make up a strong ecosystem around React gets a kind of double bump factor. They are used because they are standard in React, but again their utility is seen by other folks not even using React. This year will be nothing short of amazing when it comes to the adoption of these technologies.