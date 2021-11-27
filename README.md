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

# 4.4 Route States
- use crypto icon to create get an icon to the coin detail. 

- in the Coins.tsx, you add an image. 
```js
<Link
  to={{
    pathname: `/${coin.id}`,
    state: { name: coin.name },
  }}
>
  <Img
    src={`https://cryptoicon-api.vercel.app/api/icon/${coin.symbol.toLowerCase()}`}
  />
  {coin.name} &rarr;
</Link>
```

- you can useLocation() hook to get the current state
  - location gets the key, pathname, search and states. 

- grab the state and get the name

Coin.tsx
```js
}
interface RouteState {
  name: string;
}
function Coin() {
  const [loading, setLoading] = useState(true);
  const { coinId } = useParams<RouteParams>();
  const { state } = useLocation<RouteState>();
  return (
    <Container>
      <Header>
        <Title>{state?.name || "Loading..."}</Title>
      </Header>
      {loading ? <Loader>Loading...</Loader> : null}
    </Container>
  );
}
export default Coin;
```

- State is created when you are in Coins screen (home)
- When you go somewhere, the state is sent from home to another screen. 
- It gives an error in the incognito mode because the name is undefined. 
- If somebody comes directly to the second page because it requires home > second page to retrieve the name from the state.

# 4.5 setState 

- When people click the coin, you want to show the data. 
- When you look at the coin website. 
- URL: `https://api.coinpaprika.com/v1/coins/{coinID}
- URL: 'https://api.coinpaprika.com/v1/tickers/
- In the usereffect() function, you call the API and get ready to present data.
```js
import { useEffect, useState } from "react";
import { useLocation, useParams } from "react-router";
import styled from "styled-components";

  function Coin() {
  const [loading, setLoading] = useState(true);
  const { coinId } = useParams<RouteParams>();
  const { state } = useLocation<RouteState>();
  const [info, setInfo] = useState({});
  const [priceInfo, setPriceInfo] = useState({});
  useEffect(() => {
    (async () => {
      const infoData = await (
        await fetch(`https://api.coinpaprika.com/v1/coins/${coinId}`)
      ).json();
      const priceData = await (
        await fetch(`https://api.coinpaprika.com/v1/tickers/${coinId}`)
      ).json();
      setInfo(infoData);
      setPriceInfo(priceData);
    })();
  }, []);
  return (
    <Container>
      <Header>
        <Title>{state?.name || "Loading..."}</Title>
      </Header>
      {loading ? <Loader>Loading...</Loader> : null}
    </Container>
  );
}
export default Coin;
```

# 4.6 Data Types

- you have to explain.
```
interface IInfoData {

}
interface PriceData {

}
```

*Tip: On the console, after you get data from API, you can store it to a global variable.*

*On TypeScript you have to specify data that you want to get in the interface*

Object.keys(temp1).join()

'id,name,symbol,rank,is_new,is_active,type,contract,platform,contracts,parent,tags,team,description,message,open_source,started_at,development_status,hardware_wallet,proof_type,org_structure,hash_algorithm,links,links_extended,whitepaper,first_data_at,last_data_at'

- if you want to select all the comma, 
1. Select comma
2. press control D until the end.

Result:
id:
name:
symbol:
rank:
is_new:
is_active:
type:
contract:
platform:
contracts:
parent:
tags:
team:
description:
message:
open_source:
started_at:
development_status:
hardware_wallet:
proof_type:
org_structure:
hash_algorithm:
links:
links_extended:
whitepaper:
first_data_at:
last_data_at

3. When each word is seperated by a comma, you use control shift L
(It doesn't work now)
4. Paste the type of everything.
Objects.value()
5. Do the same for temp 2

# 4.7 Nested Routes 

- Now that we have data, we can paint the data in the detail Coin page. 

- Write the CSS part

```js
const Overview = styled.div`
  display: flex;
  justify-content: space-between;
  background-color: rgba(0, 0, 0, 0.5);
  padding: 10px 20px;
  border-radius: 10px;
`;
const OverviewItem = styled.div`
  display: flex;
  flex-direction: column;
  align-items: center;
  span:first-child {
    font-size: 10px;
    font-weight: 400;
    text-transform: uppercase;
    margin-bottom: 5px;
  }
`;
const Description = styled.p`
  margin: 20px 0px;
`;

interface PriceData {
  id: string;
  name: string;
	function Coin() {
      ).json();
      setInfo(infoData);
      setPriceInfo(priceData);
      setLoading(false);
    })();
  }, [coinId]);
  return (
    <Container>
      <Header>
        <Title>
          {state?.name ? state.name : loading ? "Loading..." : info?.name}
        </Title>
      </Header>
      {loading ? (
        <Loader>Loading...</Loader>
      ) : (
        <>
          <Overview>
            <OverviewItem>
              <span>Rank:</span>
              <span>{info?.rank}</span>
            </OverviewItem>
            <OverviewItem>
              <span>Symbol:</span>
              <span>${info?.symbol}</span>
            </OverviewItem>
            <OverviewItem>
              <span>Open Source:</span>
              <span>{info?.open_source ? "Yes" : "No"}</span>
            </OverviewItem>
          </Overview>
          <Description>{info?.description}</Description>
          <Overview>
            <OverviewItem>
              <span>Total Suply:</span>
              <span>{priceInfo?.total_supply}</span>
            </OverviewItem>
            <OverviewItem>
              <span>Max Supply:</span>
              <span>{priceInfo?.max_supply}</span>
            </OverviewItem>
          </Overview>
          <Switch>
            <Route path={`/${coinId}/price`}>
              <Price />
            </Route>
            <Route path={`/${coinId}/chart`}>
              <Chart />
            </Route>
          </Switch>
        </>
      )}
    </Container>
  );
}
```

- Then, we write a more detailed page that shows the price and the chart.
- In order to do this, make two more files in the route

1. src/routes/chart.tsx
2. src/routes/Price.tsx

- Use nested route and the information to the next route will show below the previous route.

*How do you build tabs?*

- Since there are routes already, tabs are going to be link. We do not have to do onClick.
```js
// Using Link you can easily create a link switch.
<Link to="">
```

- We can do more CSS to make the button pretty and figure out ways to communicate with the user. 
- useRouteMatch - tells where the users are in a specific URL. 
- 
```
const priceMatch = useRouteMatch("/:coinID/price");
```
- Tab is going to have the prop that is called isActive: boolean
- Tab: your tab is acteive if you say by setting up isActive variable inside the <Tab>, you can create the chart or price depending on which one to choose. 

# 4.9 React Query part 

- We can save lots of code by changing user state into React Query. 
- Configure react query
```
npm i react-query
```
- Quickstart

1. Create query client
2. Create a provider pattern. 

- everybody inside the <QueryClientProvider> will have access to the queryClient

```tsx
ReactDOM.render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <ThemeProvider theme={theme}>
        <App />
      </ThemeProvider>
    </QueryClientProvider>
  </React.StrictMode>,
  document.getElementById("root")
);
```

- React Query will abstract all the logics that we implemented by ourselves. 

- For example, we have state for coin and loading. When the data is ready, we put the loading true or false depending on how we receive data. 

```ts
  const [coins, setCoins] = useState<CoinInterface[]>([]);
  const [loading, setLoading] = useState(true);
```

- you have to create a fetcher function. return the fetched promise. 
- Promise - async function - 

*Basically, it is getting the fetch part seperately using the fetch fucntion.*

useQuery hook > calls fetcher function > loading - put in isLoading > Once fetch function finish put the data into the second argument. 

Code reduction:


Before:

```ts
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

After:
```ts
  const { isLoading, data } = useQuery<ICoin[]>("allCoins", fetchCoins);
```

- React Query hook use fetcher function and put the data after it is loaded. 

- every time you go the page, you see the loading..., it means every time we are going, we are hitting the API. Everytime, we come back fromthe bitcoin screen, we are not seeing the loading. 

- React Query is caching the response. 

- Dev Tool - you can see what is in the cache.
  - you can use this to the query and the cache that is stored. 
  - It is very easy way to visulize your query and cache. 
```js
import { ReactQueryDevtools } from "react-query/devtools";
      <ReactQueryDevtools initialIsOpen={true} />
```

- Good to break the API URL into two using the BASE_URL. 

Break API into seperate functions

```js
const BASE_URL = `https://api.coinpaprika.com/v1`;

export function fetchCoins() {
  return fetch(`${BASE_URL}/coins`).then((response) => response.json());
}

export function fetchCoinInfo(coinId: string) {
  return fetch(`${BASE_URL}/coins/${coinId}`).then((response) =>
    response.json()
  );
}

export function fetchCoinTickers(coinId: string) {
  return fetch(`${BASE_URL}/tickers/${coinId}`).then((response) =>
    response.json()
  );
}

```

React Query demands differnt key for API function. 
- All the query needs to have a unique ID. 
- If you use two seperate useQuery, it will create two different unique IDs. 
- since loading should have different names too you can change them to infoLoading and tickersLoading.

# Recap

*What is react query and why should i use it?*
- it allows you to create a fetcher function and going to notify you whether the data is fetched or not.
- React Query has a very powerful caching mechanism. 



*How do you use React Query Developer tool?*

1. Import in app.tsx

```tsx
import { ReactQueryDevtools } from "react-query/devtools";
function App() {
  return (
    <>
      <GlobalStyle />
      <Router />
      <ReactQueryDevtools initialIsOpen={true} />
    </>
  );
}
```

*How do you use React Query?*

1. Import in index.tsx and apply globally.

```tsx
import { QueryClient, QueryClientProvider } from "react-query";
ReactDOM.render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <ThemeProvider theme={theme}>
        <App />
      </ThemeProvider>
    </QueryClientProvider>
  </React.StrictMode>,
  document.getElementById("root")
);
```

2. Create an api.ts that has fetcher functions

```js
const BASE_URL = `https://api.coinpaprika.com/v1`;

export function fetchCoins() {
  return fetch(`${BASE_URL}/coins`).then((response) => response.json());
}

export function fetchCoinInfo(coinId: string) {
  return fetch(`${BASE_URL}/coins/${coinId}`).then((response) =>
    response.json()
  );
}

export function fetchCoinTickers(coinId: string) {
  return fetch(`${BASE_URL}/tickers/${coinId}`).then((response) =>
    response.json()
  );
}
```

3. Use ReactQuery

```js
import { useQuery } from "react-query";
import { fetchCoinInfo, fetchCoinTickers } from "../api";


  const { isLoading: infoLoading, data: infoData } = useQuery<InfoData>(
    ["info", coinId],
    () => fetchCoinInfo(coinId)
  );
  const { isLoading: tickersLoading, data: tickersData } = useQuery<PriceData>(
    ["tickers", coinId],
    () => fetchCoinTickers(coinId)
  );
```


# 4.12 Price Chart

- Get the parameter from the router. 
- Coin screen is what is rendering form the chart. 
- There is no need to get it from the parameter becaues the coin screen has . 
- Using coinID, you can get the historical data of crypto currency. 
- Create the fetch function in the api.tsx.
- There is a parameter to getting the historical data from and to . 

Steps:
1. Create api.tsx
2. Take the coinID from the Coin.tsx.
2. useQuery to retrieve historical data form Chart.tsx
3. render <Chart> from the coin screen. 

# 4.13 Price Chart from Apexcharts.js

- you can create many chart using Apenxcharts. 
- There are a lot of documentation. You can build almost any charts that you want to use. 

*How do you install?*

- Refer to the documentation of the apexchart.
```
npm install --save react-apexcharts apexcharts
```

Steps:

1. Create an interface of the Historical crypto data. 
2. import ApexChart.
3. You can change many props in the ApexChart
  - fill: gradient
  - colors
  - tooltip: when you pot your mouse on top. 
4. Best way of learning ApexChart is to look at demos and see how they structured.

- Price can be made realtime
- You can change the **react helmet** to change the tab text. 
- You can put the head of the document <Helmet><Title>

# 5.0 Dark mode

- you can create a toggle swtich that changes the theme. 
- If you want to send the  

- Two diff component and two different that need access. That is able to modify the state. 

- global state is the state that is shared throughout the whole application. 
  - use loggedIn could be a global state because you might want to show different page based on their login status. 

w/o state management:
isDark: App -> Router -> Coin -> Chart

(isDark) - global they could get it if they want to. 
<- chart


# 5.1 Recoil

- State management can fix the problem of routes. 
- We have a traveling prop called isDark. 
- Instead, you can put the isDark value in the bubble. This value will be kept throughout the change of states. 
- You have to route isDark prop to pages where it is needed. 
- Recoil is the one that allows us to do something. 
- Recoil is really easy to understand. 
- Please watch the video - 
- Recoil - we create different atom. In the atom, you can save whatever props that you want. 
- If you have components that want information from the atom, you connect the component directly to the atom. 

- Check out the informative website:
https://www.youtube.com/watch?v=_ISAA_Jt9kI&ab_channel=ReactEurope



*How do you use recoil?*

Install package with npm:
```shell
npm install recoil
```
*Please refer to the official documentation*

**

- Learn how to connect component to atom. 


# 5.3 

- To modify the value of the atom, you can use setter function (setterFn) to send value to the ateom. 
```js
import { useSetRecoilState } from "recoil";
import { isDarkAtom } from "../atoms";
function Coins() {
  const setDarkAtom = useSetRecoilState(isDarkAtom);
  const toggleDarkAtom = () => setDarkAtom((prev) => !prev);
  const { isLoading, data } = useQuery<ICoin[]>("allCoins", fetchCoins);
  return (
    <Container>
      </Helmet>
      <Header>
        <Title>코인</Title>
        <button onClick={toggleDarkAtom}>Toggle Mode</button>
      </Header>
      {isLoading ? (
        <Loader>Loading...</Loader>

      .....
```

# 5.4 Recap:

- Atom makes the code simple.
- Problem: traveling props. 
- Sometimes unnecessary props traveled through the components. 
- Instead of having traveling props, we created atom. 
- atom is the piece of state that we can do 
  - get the value from the props and listen to atom.
  - modify the atom. 

- Get the value: useRecoilValue(<Atom name>)
```js
// value from atom is received to the local state called isDark.
const isDark = useRecoilValue(isDarkAtom);
```
- useSetRecoilState: set the value.
```js
// once you refer to the atem, you can use the modifier function to modify the value.
const setDarkAtom = useStateRecoilState(isDarkAtom);
// function as an argument
const toggleDarkAtom = () => setDarkAtom ((prev) => !prev)
// or setDarkAtom(false) - send modified value right away.

```

# 5.5 To Do set up

- Create a ToDoList

```js
function ToDoList() {
  const [toDo, setToDo] = useState("");
  
  // onChange event handler for inputs.
  const onChange = (event: React.FormEvent<HTMLInputElement>) => {
    const {
      currentTarget: { value },
    } = event;
    setToDo(value);
  };

  // onSubmit event handler for form.
  const onSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    console.log(toDo);
  };
  return (
    <div>
      <form onSubmit={onSubmit}>
        <input onChange={onChange} value={toDo} placeholder="Write a to do" />
        <button>Add</button>
      </form>
    </div>
  );
}
```

# 5.6 React Hook Form

- React Hook form can help make all event handlers into one line of code. 
- React Hook form is best way to work on forms.

- If toDo list characters are shorter than 10, we want to display an error. 
- If you want data from the user, we have to write a form and come up with the validation. It is not complex but it takes many steps to implements them.

- use readt-hook-form

- Installation
```
react-hook-form.
```

- useForm() function with the register will do everything for you. 
  1. onChange event handler + prop of onChange + setStates for free.


Before:
```js
/* function ToDoList() {
  const [toDo, setToDo] = useState("");
  const [toDoError, setToDoError] = useState("");
  const onChange = (event: React.FormEvent<HTMLInputElement>) => {
    const {
      currentTarget: { value },
    } = event;
    setToDoError("");
    setToDo(value);
  };
  const onSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    if (toDo.length < 10) {
      return setToDoError("To do should be longer");
    }
    console.log("submit");
  };
  return (
    <div>
      <form onSubmit={onSubmit}>
        <input onChange={onChange} value={toDo} placeholder="Write a to do" />
        <button>Add</button>
        {toDoError !== "" ? toDoError : null}
      </form>
    </div>
  );
} */
```

After:
```js
import { useForm } from "react-hook-form";
function ToDoList() {
  // register will register and watch will watch the value on your form.
  // console.log(watch()); This is going to watch all the value on my form. IT will print the values as users enter data.
  const { register, watch } = useForm();
  console.log(watch());
  return (
    <div>
    {/*By doing this we are registering all the input in the register state.*/}
      <form>
        <input {...register("email")} placeholder="Email" />
        <input {...register("firstName")} placeholder="First Name" />
        <input {...register("lastName")} placeholder="Last Name" />
        <input {...register("username")} placeholder="Username" />
        <input {...register("password")} placeholder="Password" />
        <input {...register("password1")} placeholder="Password1" />
        <button>Add</button>
      </form>
    </div>
  );
```

- It saves you a lot of time because all the data you receive will be registered as an object. 

# 5.7 Form Validataion

- using userForm() function you can just import handleSubmit to perform the validation. 

- onValid() will check after all the form data has been submitted. 


```js
<form
    style={{ display: "flex", flexDirection: "column" }}
    onSubmit={handleSubmit(onValid)}
  >
```

- HTML protection of required is not enough because the user can change the source code and submit a form. 

Using React-form to require an input.
```js
<input {...register("email", { required: true })} placeholder="Email" />
```

Set the minimum length:
```js
<input
  {...register("username", { required: true, minLength: 10 })}
  placeholder="Username"
/>
```

- formState:

- formState.error -> will show the error. 
- shows on the console what errors are. It does the error-handing.;

YOu can pass on the error message if you want. 

```js
<input
  {...register("password1", {
    required: "Password is required",
    minLength: {
      value: 5,
      message: "Your password is too short.",
    },
  })}
  placeholder="Password1"
/>
```

# 5.8 Form Errors

- To validate data, you can use regular expression. It is basically setting up criteria.

- ex:[^A-Za-z0-9.+%+-]

-*Please use regex101.com to check your reg ex.*

- you write the reg ex in the pattern as below

```js
{...register("email", {
    required: "Email is required",
    pattern: {
      value: /^[A-Za-z0-9._%+-]+@naver.com$/,
      message: "Only naver.com emails allowed",
    },
  })}
```

Steps:

1. import useForm from react-hook-form
2. create an input and ...register data.
3. set up required ot not validation
4. set up pattern > value, message 
5. Show error to the user 
```js
<span>{error?email?.message}</span>
```

Final code:
```js
<form
  style={{ display: "flex", flexDirection: "column" }}
  onSubmit={handleSubmit(onValid)}
>
  <input
    {...register("email", {
      required: "Email is required",
      pattern: {
        value: /^[A-Za-z0-9._%+-]+@naver.com$/,
        message: "Only naver.com emails allowed",
      },
    })}
    placeholder="Email"
  />
  <span>{errors?.email?.message}</span>
```

# 5.9 Custom Validation

*How do you trigger an error*

- Validation on your error is useful because you can check on DB for further information. 
- You want to check whether the user has put the correct password or not. 


*send an error when password1 and password2 (confirmation) are not same*

- use setError() function. 
```js
const onValid = (data: IForm) => {
if (data.password !== data.password1) {
  setError(
    "password1",
    { message: "Password are not the same" },
    // the form is going to focus on the first form. 
    { shouldFocus: true }
  );
}
```

- Validation could be an object with many functions. 



