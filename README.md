# 2021_react-masterclass

# Our First Styled Component

- In order to create a styled component, you need to 
1. import styled component on your react.js
2. created styled.{whatever jsx compoennt you like}.
3. style that component. 


# Adapting and Extending

- Learn how to make component configurable and extendible. 
- if you want to make the background color to be configurable, we use props to send component.

```js

// we can send these properties over to the <Box> component from App() function.

const box = styled.div`
    background-color: ${(props)=> props.bgColor};
    width: 100px;
    height: 100px;

`;

function App() {
    return (
        <Father>
            <Box bgColor="teal" />
            <Box bgColor="tomato" />
        </Father>
    )
}

```

- you need to extend to minimize the copy and pasting of components that are similar. 

```js
const box = styled.div`
    background-color: ${(props)=> props.bgColor};
    width: 100px;
    height: 100px;

`;

// in order for us to extend to box to Circle, we have to use below styled()

const Circle = styled(Box)`
    border-radius: 50px;
`;


```

# 2.3 'As and Attr'

- If you do not want a button tag

```js
const FAther = styled.div`
    display: flex;
`;

const Btn = styled.button`
    color:white;
    background-color: tomato;
    border:0;
    border-radius:15px;
`;

const Link = styled(Btn);

function App() {
    return <Father>
        <Btn>Log in</Btn>
        <Btn as="a" href="/">Log in</Btn>
    </Father>;
}

```
- you can change the component with as-a as above. 

```js
const Input = styled.input.attrs({required:true})`
    background-color: tomato;
`;


// The attribute of of required is cluded in all Input components
function App() {
    return (
        <Father as="header">
            <Input />
            <Input />
            <Input />
            <Input />
            <Input />
        </Father>
    )
}

```

# 2.4 Animations and Pseudo Selectors

- We import helper {key} to create animations. 
- 
```js
const animation = keyframes`
    from {
        transform:rotate(0deg);
    }
    to {
        transform:rotate(360deg);
    }
`;

const Box = styled.div`

`;

- 

```js
import styled, { keyframes } from "styled-components";

const Wrapper = styled.div`
  display: flex;
`;

const rotationAnimation = keyframes`
  0% {
    transform:rotate(0deg);
    border-radius:0px;
  }
  50% {
    border-radius:100px;
  }
  100%{
    transform:rotate(360deg);
    border-radius:0px;
  }
`;

const Box = styled.div`
  height: 200px;
  width: 200px;
  background-color: tomato;
  display: flex;
  justify-content: center;
  align-items: center;
  animation: ${rotationAnimation} 1s linear infinite;
  // you can use span:hover as span:&
  span {
    font-size: 36px;
    &:hover {
      font-size: 48px;
    }
    &:active {
      opacity: 0;
    }
  }
```

# 2.7 Themes

- Local stage management and dark mode.
- Theme is an object that has all the colors. 
- It is useful to put all the colors in one object because you can change colors from that one object. 

*How do you create a theme?*

1. Create a ThemeProvider component.
2. Create props called theme and import darkTheme.
3. Final result

Final result:
index.js:
```js
import React from "react";
import ReactDOM from "react-dom";
// ThemeProvider is added from styled-components.
import { ThemeProvider } from "styled-components";
import App from "./App";

const darkTheme = {
  textColor: "whitesmoke",
  backgroundColor: "#111",
};

const lightTheme = {
  textColor: "#111",
  backgroundColor: "whitesmoke",
};

ReactDOM.render(
  <React.StrictMode>
  {/* The darkTheme is going to be imported. */}
  <ThemeProvider theme={darkTheme}>
      <App />
    </ThemeProvider>
  </React.StrictMode>,
  document.getElementById("root")
);
```
- Since one change of theme will change our app from the dark mode to light mode, we can make it into a toggle switch where users can modify the theme object.

# 3.0 TypeScript

- If you use typescript along with reactjs, it will make your develper experience so much easier because it will start noticing errors and notify you where the erros occured. 

*What is typesscript?*

- typescript is a progrmaming language that is based on javascript (derivative of javascript).
- It is almost the same because it is based on javascript. It builds on top of javascript. TypeScript copied everything from javascript and added new things on top. 
- TypeScript is a strongly typed programming language. It basically means that you communicate to the programming lanaguage what is the type of data before the code ran. 
ex1:
```js
const plus = (a,b)=> a+b
plus(2,2)
// output 4
// However, the type is not mentioned for each variable. 
plus(2, "hi")
// Let's see whether you want to let the javascript know that this is a wrong type. 
// With typescript, you are able to tell what is the type of data before the program runs so that typescript will tell you if anyone puts a wrong type. 
```

- typescript will also tell you about your mistake before the program is raun. 
ex2:
```ts
const user = {
  firstName: "Angela"
  lastName: "Davis",
  role: "Professor",
}
const plus = (a:number, b:number) => a+b;
```

# 3.1 Definately Typed
*How do you install typescript in creat-react app?* 

1. Start fresh and delete everything
```shell
npx create-react-app my-app --template typescript
# create new create-react-app with the typescript template.
```

2. Install typescript only
```shell
npm install --save typescript @types/node @types/react @types/react-dom @types/jest
```
- change file extension from .js to .ts
- if you run npm install, everything will be converted. 
- There might be an error complaining that it does not recognize the styled component. We need to fix that error. 
- Some library or packages are made in javascript. 
- Then, typescript will complain because they do not know that packages. 
  - even with error, there will be a recommendation along with the error message which is very nice !:)
Try `npm i --save-dev @types/styled-components` if it exists or add a new declaration (.d.ts) 

- after you run the commmand, everything is fixed. (It does nto complain about the styled component.)

@types is a very big repository and give famous packages and it gives the types for those packages so that you can work with typescript.

- project called definatelytyped that you can get most of the packages. There are other packages nodejs, nestjs etc.


# 3.2 Typing the props

- Going to explain how to type in the typescript.
- how to type or explain to typescript our react components. 
- type means you add types; when you add types to the component, you are explaining everything to typescript.
- first error, theme is missing. 

Showcase:

1. Create Circle.tsx

```ts
import styled from "styled-components"

const Container = styled.div``;

function Circle() {
  return <Container />;
}

export default Circle;
```

2. Create App.tsx

```ts
import Circle from "./Circle";

function App() {
  return (
    <div>
      <Circle />
    </div>
  );
}

export default App;
```

- We can use proptypes but without proptypes, we want to protect our component. 
- you can use interface to explain to typescript the shape of an object.

3. Create interface in Circle.tsx
```ts
interface CircleProp{
  // shape of an object is that bgColor has to be a string.
  bgColor: string;

}
```

Process:
1. App.tsx sends bgColor to Circle component 
2. Circle component now send bgcolor to Container. 
3. Create ContainerProps so that it may receive bgcolor.
- you ended up creating two interfaces ContainerProps and CircleProps.
4. After, you state that the styled component will receive an argument

```ts
const Container = styled.div<CircleProps>`
  width: 200px;
  height: 200px;
  background-color: ${(props) => props.bgColor};
  border-radius: 100px;
`;
```
