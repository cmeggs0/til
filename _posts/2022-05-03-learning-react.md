# Time to learn React through Scrimba

## Static Pages in React

- Learning the basics
### Setting up React
- https://reactjs.org/docs/cdn-links.html
    - Script tags to load react in the head of our html docs
    - React and react dom libaries
- https://reactjs.org/docs/add-react-to-a-website.html#quickly-try-jsx
    - Pull in babel as well through type="text/bable" in any html script tag
- Now have access to ReactDOM variable
**Alternatively**
- Add react and react-dom dependencies in Scrimba
- import React from "react"
- import ReactDOM from "react-dom"
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
### Components
- One of the main benefits of React is creating components which are effectively JS functions
- PascalCase instead of camelCase
- Allows us to break our code into pieces and reassemble to create a sum that is greater than it's parts
- Can nest components within other components
- Can call <Component /> like an html element
- Many ways to organize components, establish convention and be consistent
- One way is to do through files, but remember
```js
// on component file
import React from "react"
export default function Component () {
    return (<h1>Component Content</h1>)
    }
// on app file (to use component)
import Component from "../components/Component"
```
- use className to allow for easy style editing in css
### Props
- Consider adding parameters to function
- Props are similarly placeholders in components that allow the recycling of the component
- {} to use JS within JSX elements
```js
function App() {
    const firstName = "Joe"
    const lastName = "Schmoe"
    return (
        <h1>Hello {firstName} {lastName}!</h1>
    )
}
// returns Hello Joe Schmoe!
```
**Syntax**
- Can create properties (props) within each component
```js
// when calling
<Component 
    property1="property1input" 
    property2="property2input" 
/>
// When constructing component
export default function Component(props) {
    return (
        <div>
            <p>{props.property1}</p>
            <p>{props.property2}</p>
        </div>
    )
}
```
- Can call on it like a JS object
- Can destructure object immediately instead of calling props by using {}
```js
export default function Component({property1, property2}) {
    return (
        <div>
            <p>{property1}</p>
            <p>{property2}</p>
        </div>
    )
}
```
- Can pass in non-string prop by propertyNonString={4, true, etc.}
```js
<img src={`../images/${props.img}`} className="card--image" />
```
- Above code allows us to insert props element into JSX string
**Mapping Array to JSX elements**
```js
export default function App() {
    const jokeElements = jokesData.map(joke => {
        return <Joke
            key={joke.id}
            setup={joke.setup} 
            punchline={joke.punchline} />
    })
    return (
        <div>
            {jokeElements}
        </div>
    )
}
```
- Will get a warning unless we set unique keys
### Conditional Rendering
```js
{props.openSpots === 0 && <div className="card--badge">SOLD OUT</div>}
```
- Surround with {} and use straight JS
- Or can set logic in function before return ()
**Refactoring**
- Can pass all props in one go
```js
export default function App() {
    const cards = data.map(item => {
        return (
            <Card
                key={item.id}
                item={item}
            />
        )
    })
// When returning props
<img src={`../images/${props.item.coverImg}`} className="card--image" />
```
- Note, need to still include key
