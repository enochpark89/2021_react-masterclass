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

- Themes is 
