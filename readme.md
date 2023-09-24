#React Interview Questions

## 1. Why should we not update the state directly?

- If we try to update the state directly then it won't re-render the component.
```bash

//wrong 
this.state.message="hello world"

```


- Instead use setState() method it schedules an update to a components state object.When state changes , the component responds by re-redering

```bash

//right
setState({message:"hello world"})

```

## 2. What is the purpose of callback function as an argument of setState()?
- The callback function is invoked when the setState finished and the components get re-rended.Since `setState()` is __asynchronous__ the callback function is used for any post action.

```bash
setState({message:"hello world"},()=>{console.log("The state and component re-rendered")})
```
__Note__ It is recommended to use LifeCycle method

## 3. How to pass a parameter to an event handler of callback?
- You can use an arrow function to wrap around an event handler and pass parameters.
```bash
<button onClick={()=>{handleClick(id)}}>Button Name</button>
```

## 4. What is the use of refs?
- The ref is used to return a reference to the element.They should be avoided in most cases,but they can be useful when you need to access direct DOM element or an instance of a component.
## 5. What is the difference between shadow DOM and Virtual DOM?
- The shadow DOM is a browser technology designed primarily for scoping variables and css in web components.The Virtual is a concept implemented by libraries in Javascript on top of browers APIs.