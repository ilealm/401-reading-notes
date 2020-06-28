[ HOME ](README.md)
# Read 39 - React III

To get started with React Router in a web app, you’ll need a React web app. If you need to create one, we recommend you try Create React App. It’s a popular tool that works really well with React Router.
```
npx create-react-app demo-app
cd demo-app
```

#### Installation
`npm install react-router-dom`

##### 1st Example: Basic Routing and Nested Routing
In this example we have 3 “pages” handled by the router: a home page, an about page, and a users page. As you click around on the different `<Link>s`, the router renders the matching `<Route>`.

This example shows how nested routing works. The route /topics loads the Topics component, which renders any further `<Route>`'s conditionally on the paths :id value.


```
import React from "react";
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link,
  useRouteMatch,
  useParams
} from "react-router-dom";

export default function App() {
  return (
    <Router>
      <div>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/topics">Topics</Link>
          </li>
        </ul>

        <Switch>
          <Route path="/about">
            <About />
          </Route>
          <Route path="/topics">
            <Topics />
          </Route>
          <Route path="/">
            <Home />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}

function Home() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function Topics() {
  let match = useRouteMatch();

  return (
    <div>
      <h2>Topics</h2>

      <ul>
        <li>
          <Link to={`${match.url}/components`}>Components</Link>
        </li>
        <li>
          <Link to={`${match.url}/props-v-state`}>
            Props v. State
          </Link>
        </li>
      </ul>

      {/* The Topics page has its own <Switch> with more routes
          that build on the /topics URL path. You can think of the
          2nd <Route> here as an "index" page for all topics, or
          the page that is shown when no topic is selected */}
      <Switch>
        <Route path={`${match.path}/:topicId`}>
          <Topic />
        </Route>
        <Route path={match.path}>
          <h3>Please select a topic.</h3>
        </Route>
      </Switch>
    </div>
  );
}

function Topic() {
  let { topicId } = useParams();
  return <h3>Requested topic ID: {topicId}</h3>;
}
```

### Primary Components
There are three primary categories of components in React Router:

routers, like `<BrowserRouter>` and `<HashRouter>`
route matchers, like `<Route>` and `<Switch>`
and navigation, like `<Link>`, `<NavLink>`, and `<Redirect>`
We also like to think of the navigation components as “route changers”.

All of the components that you use in a web application should be imported from react-router-dom.

`import { BrowserRouter, Route, Link } from "react-router-dom";`

A `<BrowserRouter>` uses regular URL paths. These are generally the best-looking URLs, but they require your server to be configured correctly. Specifically, your web server needs to serve the same page at all URLs that are managed client-side by React Router. Create React App supports this out of the box in development, and comes with instructions on how to configure your production server as well.
A `<HashRouter>` stores the current location in the hash portion of the URL, so the URL looks something like http://example.com/#/your/page. Since the hash is never sent to the server, this means that no special server configuration is needed.

#### Route Matchers
There are two route matching components: Switch and Route. When a `<Switch>` is rendered, it searches through its children `<Route>` elements to find one whose path matches the current URL. When it finds one, it renders that <Route> and ignores all others. This means that you should put `<Route>`s with more specific (typically longer) paths before less-specific ones.

If no `<Route> `matches, the `<Switch>` renders nothing (null).

#### Navigation (or Route Changers)
React Router provides a `<Link>` component to create links in your application. Wherever you render a `<Link>`, an anchor (`<a>`) will be rendered in your HTML document.

```
<Link to="/">Home</Link>
// <a href="/">Home</a>
```


# Styling and CSS
How do I add CSS classes to components?
Pass a string as the className prop:
```
render() {
  return <span className="menu navigation-menu">Menu</span>
}
```

It is common for CSS classes to depend on the component props or state:
```
render() {
  let className = 'menu';
  if (this.props.isActive) {
    className += ' menu-active';
  }
  return <span className={className}>Menu</span>
}
```

#### Can I do animations in React?
React can be used to power animations. See ***React Transition Group***  and ***React Motion*** or ***React Spring***, for example.

#  Next.js App

the React Framework. Next.js provides a solution to all of the above problems. But more importantly, it puts you and your team in the pit of success when building React applications.


##### Create a Next.js app
To create a Next.js app, open your terminal, cd into the directory you’d like to create the app in, and run the following command:

`npm init next-app nextjs-blog --example "https://github.com/vercel/next-learn-starter/tree/master/learn-starter"`

##### Run the development server
```
cd nextjs-blog
npm run dev
```


## Sources
[React Router](https://reacttraining.com/react-router/web/guides/quick-start)
[Styling and CSS](https://reactjs.org/docs/faq-styling.html)
[ Next.js App](https://nextjs.org/learn/basics/create-nextjs-app)