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
- Can use the spread syntax instead
```js
export default function App() {
    const cards = data.map(item => {
        return (
            <Card
                key={item.id}
                {...item}
            />
        )
    })
```
- Now spreading, we can revert to original syntax when returning props (eg. props.coverImg)
### Adding Event Listeners
- Similar to the html method: <div onclick="myFunction()"></div>
- In react: <button onClick={function()}>Click me</button>
    - onMouseOver, etc.
    - https://reactjs.org/docs/events.html#mouse-events - for full list
    - Drop parenthesis after function if we define function in component but outside of element container
 ```js
  function onClickReturn() {
        var randomMeme = memesData.data.memes[Math.floor(Math.random()*memesData.data.memes.length)];
        console.log(randomMeme.url)
    }
 ```
 - Returning a random element from an array with subarrays of data.memes
 - But we are stuck, as our url randomMeme variable is trapped within the function, and even if we move it outside, cannot update page
**How to update the page with element calling on new variable**
- Have to access React state:
```js
function App() {
    const [things, setThings] = React.useState(["Thing 1", "Thing 2"])
    
    function addItem() {
        const newThingText = `Thing ${things.length + 1}`
        setThings(prevState => [...prevState, newThingText])
    }
    
    const thingsElements = things.map(thing => <p key={thing}>{thing}</p>)
    
    return (
        <div>
            <button onClick={addItem}>Add Item</button>
            {thingsElements}
        </div>
    )
} 
```
### State
- Props are immutable, should never change within component, similar to parameters being passed into a function
- State refers to values that are managed by the component, similar to variable declared inside a function, but with added benefits. Any time have changing values that should be saved/displayed, you'll likely be using states.
- State will allow react to remember those values even when a component is rerendered
- React.useState() or can destructure in import React, {useState} from "react", then can just run useState()
- Whatever is in parentheses React.useState("whatever") becomes the first value in an array produced by useState
- Can use destructuring to more easily obtain values
```js
export default function App() {
    const [isImportant, func] = React.useState("Yes") // func is usually setIsImportant
    console.log(isImportant)
    return (
        <div className="state">
            <h1 className="state--title">Is state important to know?</h1>
            <div className="state--value">
                <h1>{isImportant}</h1>
            </div>
        </div>
    )
}
```
- The function allows us to change states
```js
export default function App() {
    const [count, setCount] = React.useState(0)
    
    function add() {
        setCount(count +1)
    }
// The above works, but not best practice    
    function add() {
        setCount(prevCount => prevCount + 1)
    }
// Should pass a callback function to set count, instead of using state directly
```
- Make sure to set state outside of function!
- Can use terbaries within {} in jsx
```js
<h1>{isGoingOut ? "Yes" : "No"}</h1>
```
- Cannot use .push or array modifiers to modify original array in State, instead used the spread operator
```js
setThingsArray(prevThingsArray => [...prevThingsArray, `item you want to add`])
// Can use on objects as well
export default function App() {
    const [contact, setContact] = React.useState({
        firstName: "John",
        lastName: "Doe",
        phone: "+1 (719) 555-1212",
        email: "itsmyrealname@example.com",
        isFavorite: false
    })
    
    let starIcon = contact.isFavorite ? "star-filled.png" : "star-empty.png"
    
    function toggleFavorite() {
        setContact(prevContact => {
            return {
                ...prevContact,
                isFavorite: !prevContact.isFavorite
            }
        })
    }
    
    return (
        <main>
            <article className="card">
                <img src="./images/user.png" className="card--image" />
                <div className="card--info">
                    <img 
                        src={`../images/${starIcon}`} 
                        className="card--favorite"
                        onClick={toggleFavorite}
                    />
                    <h2 className="card--name">
                        {contact.firstName} {contact.lastName}
                    </h2>
                    <p className="card--contact">{contact.phone}</p>
                    <p className="card--contact">{contact.email}</p>
                </div>
                
            </article>
        </main>
    )
}
```
- Cannot use onClick or other event listeners on custom components, instead use handleClick={pass in function in} and then in our component onClick={props.handleClick}

**Passing data to components**
- Only parents can access state from, but if we raise state into parent, we can pass to children through props
- Keep state as close to component as possible
- Multiple ways to change state
```js
export default function Box(props) {
    const [on, setOn] = React.useState(props.on)
    
    const styles = {
        backgroundColor: on ? "#222222" : "transparent"
    }
    
    function toggle() {
        setOn(prevOn => !prevOn)
    }
    
    return (
        <div style={styles} className="box" onClick={toggle}></div>
    )
}
```
- This way sets state for each individual box, known as derived state -> leads to multiple sources of truth, because we had state at the app level
- Better way to structure, is to hold state at the App level
```
export default function App() {
    const [squares, setSquares] = React.useState(boxes)
    
    function toggle(id) {
        setSquares(prevSquares => {
            return prevSquares.map((square) => {
                return square.id === id ? {...square, on: !square.on} : square
            })
        }) 
    }
// in our app component
// then at the component level we call it 
<div 
    style={styles} 
    className="box"
    onClick={()=>props.toggle(props.id)}
>
```
### Conditional Rendering
- A way to determine if something should or should not be displayed, or what choice should be displayed
- using && operator can be great: {messages > 0 && <p>You have {messages.length} unread messages</p>}
    - This will only display the message if both are true, but it goes in order from left to right
- Using ternaries is very useful when you want to change the value based on a condition
- If choosing between more than 2 things, can use if statement or switch statement. Could also use nested conditionals, but it can be harder to follow
### Forms
- A lot of good libraries
- Instead of waiting until the end of process, React gathers information as it is input
- https://reactjs.org/docs/forms.html - React forms documentation
- Generally make React the single source of truth, a "controller compoennt" rather than relying on html input form elements
- event is the implicit parameter on functions handling onChange inputs
- Give our inputs a name property
```js
export default function Form() {
    const [formData, setFormData] = React.useState(
        {firstName: "", lastName: ""}
    )
    
    console.log(formData)
    
    function handleChange(event) {
        setFormData(prevFormData => {
            return {
                ...prevFormData,
                [event.target.name]: event.target.value
            }
        })
    }
    
    return (
        <form>
            <input
                type="text"
                placeholder="First Name"
                onChange={handleChange}
                name="firstName"
            />
            <input
                type="text"
                placeholder="Last Name"
                onChange={handleChange}
                name="lastName"
            />
        </form>
    )
}
```
- We can handle multiple inputs by changing our state to an object
- Make sure you surround [event.target.name] with square brackets to make it the key

**Controlled Components**
- Make the state in React the single source of truth:
- add 'value={formData.firstName}' to the input form to make sure that it is reflecting the React state
- textarea is not self closing in html, but they have made it so in react
