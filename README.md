# Welcome to React with Next.js

Hi there! This workshop is an introduction to [React.js](https://reactjs.org) using [Next.js](https://nextjs.org). It assumes you have some familiarity with HTML and JavaScript, as well as programming functions like functions, objects, arrays, and classes, but you should be able to follow along regardless. If you're having trouble, feel free to ask in the Big Red Hacks Discord or in person!

Source adapted from a Hack Club tutorial.

# Requirements

This workshop requires the following dependencies:

- **Visual Studio Code**
- **[npm] https://nodejs.org/en/**
- **[Yarn] https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable**
- **Access to github


## Intro to React

HTML, as you’re likely familiar, is the way you declare what content goes on your webpage. We’re now moving past just webpages toward building interactive apps. Traditional web apps have regular HTML, then use JavaScript to manually update the HTML when data changes. Consider getting a new message on Facebook: when there's a new message, the site automatically inserts the new message into the list without you having to reload the page.

React is a framework built by engineers at Facebook a few years ago to make building complex web apps way easier. We’re going to start super simply, using React to make a regular-looking website, then start adding more complex functionality. Here are five terms you should know:

- **JSX.** Some engineers came up with a way to write HTML inside JavaScript. It sounds crazy, but it uses almost the same syntax as regular HTML (deep inside it’s fancy syntax for JavaScript functions that create HTML elements). The simplest JSX: `<p>Hi!</p>`. You can also use JavaScript inside JSX. So if you’ve got `const name = 'Zach Latta'` in your JS file, you can write `<h1>Welcome, {name}</h1>`, and on your page it’ll show `Welcome, Zach Latta` in a heading.
- **Components.** React apps are built with the idea of components, which are pieces of your application that encapsulate all their stuff—data, state (see below), styling, subcomponents. Everything is a component, from just one tag (the `p` tag above is a component) to entire sections of a webpage. For example, if you created a component called "Welcome"—`const Welcome = () => <h1>Welcome!</h1>`—you could then write `<Welcome />` somewhere else in your app to load that component. This is a simple component, but you can imagine if that were a whole section of your site, being able to render it multiple times in different locations would be super useful. You can compose components together to create complex interfaces.
- **Props.** Short for “properties”, props are how you pass data between components. These are “inputs” that you can use inside the component. Let’s update the `Welcome` component we just talked about with props: `const Welcome = ({ name }) => <h1>Welcome, {name}!</h1>`. Here, we’re saying we have a component called `Welcome` and it accepts an input called `name`. You can use the curly braces inside a component to “embed” JavaScript values, in this case the `name` prop’s value. Props are passed just like HTML attributes: `<Welcome name="Zach Latta" />`.
- **State.** This is data in your app. That might be the fact that a dropdown menu is open, or not. If you need information to decide how you render your site, it goes in state. We’ll get to using state later.

### Components

Let’s make a more complex component now, with several props. Imagine you’re building a news website or a blog, so you need to show a list of articles with consistent styling.

```js
const Article = ({ title, author, preview }) => (
  <div>
    <h3>{title}</h3>
    <p>By {author}</p>
  </div>
)
```

Now you can use it like this:

```js
<Article title="Hello Hack Club!" author="@lachlanjc" />
```

(Thinking ahead—instead of just using components one-at-a-time like this, imagine downloading a list of articles, then rendering this Article component for each one. Well, that’s how news websites work!)

JSX tip: when you’re passing a string (text) value to a prop, you can use quotes, just like in HTML, but if you’re passing JavaScript, you use curly braces. If articles had multiple authors, we’d pass an array:

```js
<Article title="Hello Hack Club!" author={['@lachlanjc', '@zachlatta']} />
```

[(Want to read more about JSX?)](https://reactjs.org/docs/introducing-jsx.html)

## Next.js

So far we’ve just been looking at React. [Next.js](https://nextjs.org) is a framework built to make building React-based web apps way easier. It handles setting up multiple pages, starting a server, and a bunch of super complex setup in the background. [A whole bunch](https://nextjs.org/showcase/) of major companies use it—it even powers parts of GitHub.

You’ve been reading long enough; let’s open up your development environment. Get started with a super simple template from next.js. Open command line or terminal and enter the following line from the folder you want your project to be in. Feel free to change "my-next-app" to any project name you want.
```npm init next-app my-next-app```

Next open the project in Vscode.

Looking around the project, there are three important files:

- `pages/_app.js`. This is a router file Next.js uses to render each page. Next.js uses the App component to initialize pages.
- `pages/index.js`. To make a page on your site with Next.js, instead of an `index.html` file, we’ll have a `pages` folder and put `index.js` inside of it. Want an /about page? Add `about.js`.
- `package.json`. In a JavaScript-based project, we set up this file to define dependencies known as “packages”—bundles of code from other developers we need for our project to run. You’ll see we’re requiring `next`, `react`, & `react-dom` (that last one’s the “adapter” to run React on the web). 

At its most basic, a page with Next.js (so a file like `pages/index.js`) looks like this. What gets rendered on the page goes inside the “default export” of the file.

```js
export default () => <h1>Welcome!</h1>
```

### Making your first Next.js page

Let’s try out that component we were using above:

```js
const Article = ({ title, author, preview }) => (
  <div>
    <h3>{title}</h3>
    <p>By {author}</p>
  </div>
)

export default () => (
  <main>
    <h1>Articles</h1>
    <Article title="Hello Hack Club!" author="@zachlatta" />
    <Article title="Workshops are cool" author="@lachlanjc" />
  </main>
)
```

Hey, look at that! Try adding your own. Your site should immediately update.

### Linking to a new page

Let’s make a second page, and add a link to it.

First up, the link. We need a way to make that link, but Next.js has our back here. At the top of the file, add `import Link from 'next/link'`. You’ve just imported your first React component, and can use it!

```js
import Link from 'next/link'

const Article = ({ title, author, preview }) => (
  <div>
    <h3>{title}</h3>
    <p>By {author}</p>
  </div>
)

export default () => (
  <main>
    <h1>Articles</h1>
    <Article title="Hello Hack Club!" author="@zachlatta" />
    <Article title="Goodbye Hack Club :(" author="@lachlanjc" />
    {/*Try adding another article!*/}
    <Link href="/shopping">
      <a>Let’s go shopping</a>
    </Link>
  </main>
)
```

The `Link` component makes whatever we click on go that page, then the `<a>` tag is the actual HTML element that’ll appear on our page.

### Building a shopping list page

Now, that doesn’t go anywhere yet. Click on “New file” and enter `pages/shopping.js`. We’re going to make a quick shopping list!

In your mind, imagine with this HTML will look like: (`ul` makes a bulleted list, if you haven’t used it before)

```html
<h1>Shopping List</h1>
<ul>
  <li>Apples</li>
  <li>Oranges</li>
  <li>Pears</li>
  <li>Strawberries</li>
</ul>
```

If we were going to only ever have those items on the page, it’d be the exact same thing in Next, wrapped in the `export default` code we saw on the first page.

However, declaring the `<li>` elements over & over is getting tiresome. Let’s move the list of items into a JavaScript array (`['thing', 'second thing']`, etc), then “map” through each item and put it in the HTML.

```js
const items = ['Apples', 'Oranges', 'Pears', 'Strawberries']

export default () => (
  <main>
    <h1>Shopping List</h1>
    <ul>
      {items.map((item) => (
        <li key={item}>{item}</li>
      ))}
    </ul>
  </main>
)
```

Hold up. You just made a huge shift in how you develop things: you went from writing the code for the website directly yourself, to _writing the code for the website to generate itself_. You define the data (in most “real” apps, you’d fetch the data from a server) and _how_ it should be shown on your site, but the site puts two and two together for the final product.

This opens the gateway to drastically more powerful and interesting websites. You can fetch the current temperature from a weather service and make a component to display it in. You can fetch some news headlines and display a list of articles with images. Yes yes yes!

### Adding interactivity to the list

We’re going to take this to the next level now, allowing users to add items to the list. We’ll need to use React’s state feature to keep the data and handle the “events” (user typing, user clicking the Add button).

First, let’s make a new component. Since this component uses “state” (values that change, usually via user interaction), we’re going to need React’s `useState` functionality (it’s one of the “React Hooks”). In `pages/shopping.js`, add this line at the top:

```js
import React, { useState } from 'react'
```

Now we need to make our component. We’ll need a text input, a button to add the item, and the same list of items. Notice that we now have a `return` call after the `export` but before the JSX for the page—you’ll need this for the next step.

```js
const items = ['…']

export default () => {
  return (
    <main>
      <h1>Shopping List</h1>
      <div>
        <input placeholder="New item" />
        <button>Add item</button>
      </div>
      <ul>
        {items.map((item) => (
          <li key={item}>{item}</li>
        ))}
      </ul>
    </main>
  )
}
```

Next up, we need to define some state on this component. Delete the `const items` line, and set up

```js
export default () => {
  const [items, setItems] = useState(['Apples', 'Strawberries'])
  const [newItem, setNewItem] = useState('')
  return (
    <main>
      <h1>Shopping List</h1>
      <div>
        <input placeholder="New item" />
        <button>Add item</button>
      </div>
      <ul>
        {items.map((item) => (
          <li key={item}>{item}</li>
        ))}
      </ul>
    </main>
  )
}
```

`newItem` is where we’ll keep the text the user enters into the text box. Now, all that’s left is to add some event handling:

```js
export default () => {
  const [items, setItems] = useState(['Apples', 'Strawberries'])
  const [newItem, setNewItem] = useState('')
  const changeNewItem = (e) => setNewItem(e.target.value)
  const addItem = () => {
    setItems((list) => [...list, newItem])
    setNewItem('')
  }
  return (
    <main>
      <h1>Shopping List</h1>
      <div>
        <input
          placeholder="New item"
          onChange={changeNewItem}
          value={newItem}
        />
        <button onClick={addItem}>Add item</button>
      </div>
      <ul>
        {items.map((item) => (
          <li key={item}>{item}</li>
        ))}
      </ul>
    </main>
  )
}
```

This is a little more complex, so let’s break it down:

1. `items` is our array of the items on the list (which `items.map` shows further down)
   - What we pass to `useState` is the default value, so before the user does anything, that’s the initial state.
   - `setItems` is a function React is generating for us for changing the value of `items`. The whole page is, underneath, a function (see the `() => {}` on the first line), so if you were to do `items = […]`, the next time React ran the function to render the page, the changes to the variable would disappear. To get around this, React keeps track of our state outside the context of just the functions for each component.
2. `newItem` & `setNewItem` work similarly, keeping track of the text the user types into the input box in a second chunk of React state.
3. `changeNewItem` is a function we wrote so that when the user types into the input box, we get the value of the input & set it to the state. (`e` is the raw JavaScript event, `target` is the HTML element the event happened to, then `value` is the current value of the element.)
4. `addItem` is the code that runs when the user presses the “Add item” button. It adds the `newItem` to the list of `items`, then clears the input box. (This works because we set the `value` of the state, so when we change the state, so does the element.)

One thing about React state is that it’s not “persistent”—the list won’t be saved if you come back another day—but there a bunch of ways to handle data storage later on.

## Deployment
Once done building your website, initialize, commit and push your directory to a github repository. To deploy to a website, login to [Vercel](https://vercel.com/login) with your github account. Vercel will then prompt you to connect a repo. After you connect your github repo, Vercel will give you a hosted link that automatically updates whenever you update the github repo! And there you have it, a running next.js website that's live on the web!

## Bonus: styling!

When you’re using CSS, every style you add applies to your whole website. This is handy when you’re getting started, but if you imagine working at Facebook, if one person makes the buttons styled a little differently, the entire website updates. With thousands of people working together, there’s no way they can all keep track of changes like that.

One of the really interesting features of Next.js is that you can encapsulate styling inside a React component. If you go back to `pages/index.js`, add a `<style>` tag just like this.

```js
export default () => (
  <main>
    <h1>Articles</h1>
    {/* the rest of your code... */}
    <style jsx>{`
      h1 {
        color: magenta;
      }
    `}</style>
  </main>
)
```

Open up your app: the homepage has a magenta heading, but critically, the heading on the Shopping page doesn’t! Magical. So, you can style components on the Shopping page separately too.

```js
<main>
  <h1>Shopping List</h1>
  {/* the rest of your code... */}
  <style jsx>{`
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      padding: 1em 0;
      border-top: 1px solid #eee;
    }
  `}</style>
</main>
```

Go crazy—try changing the fonts, colors, & whatever else!

## Conclusion

Over the course of this workshop, you went from not knowing what JSX was to deploying a two-page, interactive web app with it. Great work! This is just a starting point—you can keep adding to this app, but you can also follow countless other tutorials to use powerful plugins and build high quality prototypes incredibly fast.
