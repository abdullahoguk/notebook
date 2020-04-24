# React

https://btholt.github.io/complete-intro-to-react-v5

## Pure React

* Creating a component 

  ```js
  MyCoponent = function(props){
      return React.createElement(
        Parent,
          { prop1:"foo" },
          [React.createElement("h1", {}, props.name), childComp2,] )
  }
  ```
  
  

```js
//Create a componet called Pet
const Pet = (props) => {
  return React.createElement("div", {}, [
    React.createElement("h1", {}, props.name),
    React.createElement("h2", {}, props.animal),
    React.createElement("h2", {}, props.breed)
  ]);
};
//Create a componet called App parent is a div and childs are 1 h1 and 3 Pet Componet 
const App = () => {
  return React.createElement("div", {}, [
    React.createElement("h1", {}, "Adopt Me!"),
    React.createElement(Pet, {
      name: "Luna",
      animal: "Dog",
      breed: "Havanese"
    }),
    React.createElement(Pet, {
      name: "Pepper",
      animal: "Bird",
      breed: "Cockatiel"
    }),
    React.createElement(Pet, { name: "Doink", animal: "Cat", breed: "Mix" })
  ]);
};

//Create a new instence of App Componet and render into Div with the id of "root"
ReactDOM.render(React.createElement(App), document.getElementById("root"));
```

## JSX and Function Componenets

- The below code equivalent to component pet we created above

```jsx
import React from "react";

const Pet = function(props){
  return (
    <div>
      <h1>{props.name}</h1>
      <h2>{props.animal}</h2>
      <h2>{props.breed}</h2>
    </div>
  );
};

export default Pet;
```

- App Component

```jsx
import React from "react";
import ReactDOM from "react-dom";
import Pet from "./Pet";

const App = () => {
  return (
    <div>
      <h1>Adopt Me!</h1>
      <Pet name="Luna" animal="dog" breed="Havanese" />
      <Pet name="Pepper" animal="bird" breed="Cockatiel" />
      <Pet name="Doink" animal="cat" breed="Mix" />
    </div>
  );
};

ReactDOM.render(<App />, document.getElementById("root"));
```

* Rendering multiple components based on a collection of data (Key should be specified to get more performance on re-rendering of  a collection of components)

```jsx
 {ANIMALS.map(animal => (
      <option key={animal} value={animal}>
        {animal}
      </option>)
   )
 }
```



## Hooks (for function components)

### States

* To use and set state in a function component

* A basic modifiable text input

  ```jsx
  // in SearchParams.js
  import React, { useState } from "react";
  
  // creates a state called location and its setter function and sets a default value 
  const [location, updateLocation] = useState("Seattle, WA");
  
  // replace input
  <input
    id="location"
    value={location}
    placeholder="Location"
    onChange={e => updateLocation(e.target.value)}
  />;
  ```

* Don't put hooks into conditional statements (ifs ...)

### Effects 

- Effects run after every re(render). 
- Effects can take the place of *most* life cycle methods, like `componentDidMount` and `componentDidUpdate` in previous versions of React.

```js
//useEffect(function, array) 
// An effect that fetch breeds of current selected animal 
useEffect(() => {
    setBreeds([]);
    setBreed("");
    pet.breeds(animal).then(({ breeds }) => {
      const breedStrings = breeds.map(({ name }) => name);
      updateBreeds(breedStrings);
    }, console.error);
  }, [animal]); // array of variables to filter that effect to run on specific variable change
//in this case, this effect only runs when animal state changes
//if you give an empty array, it will run only once
```

- 

* Custom Hooks



## Router 

Reach router 

## Class Components

you can use arrow function on callback/events to bypass binding context 



## Context

Global store, replaces redux

## Portals 

