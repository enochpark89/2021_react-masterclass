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

# 3.3 Optional Props

- Add a border color to the circle. 
- If you want to make the optional prop, you just need to put a question mark(?) after

Summary:
1. App will send two arguments called borderColor and bgColor.
2. Circle will receive the props and make sure that it follows the CircleProps checking required props. 
3. Circle function will send two props into the container.
  - You set the optional props by coding below
```js
<Container bgColor={bgColor} borderColor={borderColor ?? bgColor}>{text}
</Container>
```
# 3.4 State

- you can use useState to set the current state or variable. 
```js
// Set the current state of 1; counter is the current state; setCounter is what user uses to set the new state.
const [counter, setCounter] = useState(1)
// set a new counter by using setCounter.
setCounter(2)
```
- Case 1: when the type is decalred on the useState it will remain the same and typescirpt will expect the same type throughout the page. 
```js
// this will give an error because setValue would expect a boolean.
const [value, setValue] = useState(true);
setValue(2);
// If you want to avoid an error, you can set either or as below
const [value, setValue] = useState<number|string>(0);
setValue(2);
```
# 3.5 Form

- Implement a form using Typescript. 
- 
```tsx
import React, { useState } from "react";

function App() {
  const [value, setValue] = useState("");

// onChange event created
  const onChange = (event: React.FormEvent<HTMLInputElement>) => {
    // event.value is called.
    const {
      currentTarget: { value },
    } = event;
    //event.value is called value; value used on setValue to set a new state.
    setValue(value);
  };

  // onSubmit event is created. 
  const onSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    // once submitted, event will preventDefault() - refresh and it will print the current value along with "hello" string.
    event.preventDefault();
    console.log("hello", value);
  };
  return (
    <div>
      <form onSubmit={onSubmit}>
        <input
          value={value}
          onChange={onChange}
          type="text"
          placeholder="username"
        />
        <button>Log in</button>
      </form>
    </div>
  );
}
export default App;

```
# 3.6 Theme

- We saw themes and it is cool because it allows you to toggle between the dark mode and the light mode. 
- We installed a type definition which is the file that explain to typescript about the styled-components and other packages. 
Steps to install typescript
URL:
https://styled-components.com/docs/api#typescript


1. Install a type defintion
- explain to typescript what is the styled component. 
2. Create a declaration file. 
- it finishes in d.ts.
- one that is in the github also finish it. It is in github so you can download. 
- we need to extend and add in little code. 
- create a file called src/styled.d.ts
  a. copy paste what is in the styled-component-typescript link above.
  b. set the shape of your theme. 
```ts
import "styled-components";

// declare a module and create in interface called DefaultTheme.
declare module "styled-components" {
  export interface DefaultTheme {
    textColor: string;
    bgColor: string;
    btnColor: string;
  }
}
```
- create theme.ts; create light and dark theme.
```ts
// import DefaultTheme from styled.d.ts
import { DefaultTheme } from "styled-components";

// Create light and dark themes.
export const lightTheme: DefaultTheme = {
  bgColor: "white",
  textColor: "black",
  btnColor: "tomato",
};

export const darkTheme: DefaultTheme = {
  bgColor: "black",
  textColor: "white",
  btnColor: "teal",
};
```
- import both style.d.ts and theme.ts from index.tsx and utilize the exports.
index.tsx
```ts
import React from "react";
import ReactDOM from "react-dom";
import { ThemeProvider } from "styled-components";
import App from "./App";
import { darkTheme, lightTheme } from "./theme";

ReactDOM.render(
  <React.StrictMode>
    <ThemeProvider theme={darkTheme}>
      <App />
    </ThemeProvider>
  </React.StrictMode>,
  document.getElementById("root")
);
```

# 3.7 Recap:

- Introduction to TypeScript.
1. Difference between TypeScript and JavaScript
- TypeScript is like a superset of JavaScript. 
- In order to specify the type of anything, we have to set the type for each value and what it will return. 
- SyntheticEvent - React version of event. 
  - There are list of events that you can look up
  - You can use form event. 
- sometimes, you are going to download that you do not have the typescript declaration or explanation.
- most of the time, if you are using a popular library, it will be in the repository called DefinitelyTyped. 
- another way of installing is using npm install --save-dev @types/<name of the pacakage>

# 4.0 Create Coin tracking API

- Create a coin tracking that shows many new information about the crypto currency.

- You can use *react query* to fetch the data. 

- First, create in a regular way and second, you have to know what problems were addressed in react query. 

- Install react router dom

```
npm i react-router-dom react-query
```

*Please install @5.2 react-dom because otherwise, it wouldn't work.*

- UseParam will allow you to grab the related name in URL. 

# 4.1 Styles

- Since there are some default sytles in REact, we want to get rid of things and start from 0 because otherwise, we have to cope with different default styles. 

- You can use import styled-reset.
- It is same as using reset style. 

```js
function App() {
  return (
    <>
      <GlobalStyle />
      <Router />
    </>
  );
}
```
- createGlobalStyle will apply the style to the whole program. 

- React team released something called fragment <> which is the ghost appearance that is not doing any styles. 

- you can set the global font style.
- you can look up the Google font for help since they have nice style options. 

- you can write a theme from the flatuicolors.com - choose a pallete. 
- Change btn to AccentColor. 
- 

- Two things that I need to know how to do. 
  1. Import a globalstyle and reset css.
  2. Set the globalfont. 

# 4.2 Home - Pt1

- Set up the Home page with Coins details

Coins.tsx
```ts

```
- you can use the cryptocurrency website to create a API that presents the general imformation and put it on the project. 


# 4.3 Home part Two 

- fetch the data from the actual API.
- CoinPaprica 
- added max-width and margin and the margin will act like a mobile app. 

- In order to bring the data, you have to add the interface of the data. 

```js
interface CoinInterface {
  id: string;
  name: string;
  symbol: string;
  rank: number;
  is_new: boolean;
  is_active: boolean;
  type: string;
}
```

- Run code in a certain period of time = useEffect() - start or end 

- import UseEffect() so that it would only run in the beginning of the Coins API fetch
```js
function Coins() {
  const [coins, setCoins] = useState<CoinInterface[]>([]);
  const [loading, setLoading] = useState(true);
  useEffect(() => {
    (async () => {
      const response = await fetch("https://api.coinpaprika.com/v1/coins");
      const json = await response.json();
      setCoins(json.slice(0, 100));
      setLoading(false);
    })();
  }, []);
```

- The cool trick to execute it immediately.

```js
 useEffect(() => {
   // this part is executed immediately.
    (async () => {
      const response = await fetch("https://api.coinpaprika.com/v1/coins");
      const json = await response.json();
      setCoins(json.slice(0, 100));
      setLoading(false);
    })();
  }, []);
```

- Usually, it grabs 9000 coins but you are only going to take 100. 
```
a.slice(0,5) - cut the array.
```

- Create a loading state
```js
  const [loading, setLoading] = useState(true);
  ......
   {loading ? (
        <Loader>Loading...</Loader>
      ) : (
        <CoinsList>
          {coins.map((coin) => (
            <Coin key={coin.id}>
              <Link to={`/${coin.id}`}>{coin.name} &rarr;</Link>
            </Coin>
          ))}
        </CoinsList>
      )}
```

Final

Coins.tsx
```js
import { useEffect, useState } from "react";
import { Link } from "react-router-dom";
import styled from "styled-components";

const Container = styled.div`
  padding: 0px 20px;
  max-width: 480px;
  margin: 0 auto;
`;

const Header = styled.header`
  height: 15vh;
  display: flex;
  justify-content: center;
  align-items: center;
`;
const CoinsList = styled.ul``;
const Coin = styled.li`
  background-color: white;
  color: ${(props) => props.theme.bgColor};
  border-radius: 15px;
  margin-bottom: 10px;
  a {
    padding: 20px;
    transition: color 0.2s ease-in;
    display: block;
  }
  &:hover {
    a {
      color: ${(props) => props.theme.accentColor};
    }
  }
`;
const Title = styled.h1`
  font-size: 48px;
  color: ${(props) => props.theme.accentColor};
`;

const Loader = styled.span`
  text-align: center;
  display: block;
`;

interface CoinInterface {
  id: string;
  name: string;
  symbol: string;
  rank: number;
  is_new: boolean;
  is_active: boolean;
  type: string;
}

function Coins() {
  const [coins, setCoins] = useState<CoinInterface[]>([]);
  const [loading, setLoading] = useState(true);
  useEffect(() => {
    (async () => {
      const response = await fetch("https://api.coinpaprika.com/v1/coins");
      const json = await response.json();
      setCoins(json.slice(0, 100));
      setLoading(false);
    })();
  }, []);
  return (
    <Container>
      <Header>
        <Title>코인</Title>
      </Header>
      {loading ? (
        <Loader>Loading...</Loader>
      ) : (
        <CoinsList>
          {coins.map((coin) => (
            <Coin key={coin.id}>
              <Link to={`/${coin.id}`}>{coin.name} &rarr;</Link>
            </Coin>
          ))}
        </CoinsList>
      )}
    </Container>
  );
}
export default Coins;
```

