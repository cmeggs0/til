# Time to learn React through Scrimba

## Static Pages in React

- Learning the basics
- https://reactjs.org/docs/cdn-links.html
    - Script tags to load react in the head of our html docs
    - React and react dom libaries
- https://reactjs.org/docs/add-react-to-a-website.html#quickly-try-jsx
    - Pull in babel as well through type="text/bable" in any html script tag
- Now have access to ReactDOM variable
```js
ReactDOM.render(<h1>Hello, everyone!</h1>, document.getElementById("root"))
```
- First part is what we want to show up
- Second part is where we want it to show up
### Benefits of React
1. Allows us to write composable code
    - Meaning, basically we can break down code into manageable flexibly chunks
2. It's Declarative
    - What should be done? Tell me what to do, and I'll get it done
    - Vs Imperative, how it should be done? Describe each step of the way how to do something
```js
const h1 = document.createElement("h1")
h1.textContent = "Hello world"
h1.className = "header"
document.getElementById("root").append(h1)
// Versus
ReactDOM.render(<h1 className="header">Hello world<h1>, document.getElementById("root"))
```
3. It's a hireable skill
4. It's actively maintained by skilled people
**JSX**
- React created JSX, a flavor of React that looks and acts like html
- There are some differences like className
- More fundamentally, it creates a JS objects that react can interpret into html elements
- Can save a whole bunch of JSX into a variable, then use it
- .render can only render one parent element, cannot have multiple sibling elements
```js
const navBar = (
    <nav>
        <h1>My Website</h1>
        <ul>
            <li>Pricing</li>
            <li>About</li>
            <li>Contact</li>
        </ul>
    </nav>
)

ReactDOM.render(navBar, document.getElementById("root"))
```
