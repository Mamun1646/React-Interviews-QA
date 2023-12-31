# React Interview Questions

## 1. Why should we not update the state directly?

- If we try to update the state directly then it won't re-render the component.
```jsx harmony

//wrong 
this.state.message="hello world"

```


- Instead use setState() method it schedules an update to a components state object.When state changes , the component responds by re-redering

```jsx harmony

//right
setState({message:"hello world"})
```

## 2. What is the purpose of callback function as an argument of setState()?
- The callback function is invoked when the setState finished and the components get re-rended.Since `setState()` is __asynchronous__ the callback function is used for any post action.

```jsx harmony
setState({message:"hello world"},()=>{console.log("The state and component re-rendered")})
```
__Note__ It is recommended to use LifeCycle method

## 3. How to pass a parameter to an event handler of callback?
- You can use an arrow function to wrap around an event handler and pass parameters.
```jsx harmony
<button onClick={()=>{handleClick(id)}}>Button Name</button>
```
## 4. What is the use of refs?

- The ref is used to return a reference to the element.They should be avoided in most cases,but they can be useful when you need to access direct DOM element or an instance of a component.
## 5. What is the difference between shadow DOM and Virtual DOM?
- The shadow DOM is a browser technology designed primarily for scoping variables and css in web components.The Virtual is a concept implemented by libraries in Javascript on top of browers APIs.
## 6. What is switching component?
A switching component is a component that renders one of many components. We need to use object to map prop values to components.

For example, a switching component to display different __pages__ based on page prop:
```jsx harmony
import HomePage from "./HomePage";
import AboutPage from "./AboutPage";
import ServicesPage from "./ServicesPage";
import ContactPage from "./ContactPage";

const PAGES = {
  home: HomePage,
  about: AboutPage,
  services: ServicesPage,
  contact: ContactPage,
};

const Page = (props) => {
  const Handler = PAGES[props.page] || ContactPage;

  return <Handler {...props} />;
};

// The keys of the PAGES object can be used in the prop types to catch dev-time errors.
Page.propTypes = {
  page: PropTypes.oneOf(Object.keys(PAGES)).isRequired,
};

```



###  7. Why should component names start with capital letter?

If you are rendering your component using JSX, the name of that component has to begin with a capital letter otherwise React will throw an error as an unrecognized tag. This convention is because only HTML elements and SVG tags can begin with a lowercase letter.

```jsx harmony
   class SomeComponent extends Component {
      // Code goes here
    }

```

    
 


You can define component class which name starts with lowercase letter, but when it's imported it should have capital letter. Here lowercase is fine:

```jsx harmony

    class myComponent extends Component {
      render() {
        return <div />;
      }
    }

    export default myComponent;

```

While when imported in another file it should start with capital letter:
```jsx harmony
 import MyComponent from "./myComponent";


```
   
#### What are the exceptions on React component naming?
The component names should start with an uppercase letter but there are few exceptions to this convention. The lowercase tag names with a dot (property accessors) are still considered as valid component names.
    For example, the below tag can be compiled to a valid component.
```jsx harmony
 render() {
              return (
                <obj.component/> // `React.createElement(obj.component)`
              )
        }

```
### 8.How to loop inside JSX?
You can simply use `Array.prototype.map` with ES6 _arrow function_ syntax.
For example, the `items` array of objects is mapped into an array of components:

```jsx harmony
    <tbody>
      {items.map((item) => (
        <SomeComponent key={item.id} name={item.name} />
      ))}
    </tbody>
```

But you can't iterate using `for` loop:

```jsx harmony
    <tbody>
      for (let i = 0; i < items.length; i++) {
        <SomeComponent key={items[i].id} name={items[i].name} />
      }
    </tbody>
```

This is because JSX tags are transpiled into _function calls_, and you can't use statements inside expressions. This may change thanks to `do` expressions which are _stage 1 proposal_.

### 9.How to pretty print JSON with React?
\We can use `<pre>` tag so that the formatting of the `JSON.stringify()` is retained:
```jsx harmony
     const data = { name: "John", age: 42 };

     class User extends React.Component {
       render() {
         return <pre>{JSON.stringify(data, null, 2)}</pre>;
       }
     }

     React.render(<User />, document.getElementById("container"));
```

 ### 10.Why you can't update props in React?
The React philosophy is that props should be _immutable_ and _top-down_. This means that a parent can send any prop values to a child, but the child can't modify received props.

### 11. How can we find the version of React at runtime in the browser?
You can use `React.version` to get the version.
```jsx harmony
     const REACT_VERSION = React.version;

     ReactDOM.render(
       <div>{`React version: ${REACT_VERSION}`}</div>,
       document.getElementById("app")
     );
```

### What are the possible ways of updating objects in state?

1. **Calling `setState()` with an object to merge with state:**

- Using `Object.assign()` to create a copy of the object:

    ```javascript
          const user = Object.assign({}, this.state.user, { age: 42 });
          this.setState({ user });
          ```
 - Using _spread operator_:

    ```javascript
          const user = { ...this.state.user, age: 42 };
          this.setState({ user });
          ```

2. **Calling `setState()` with a function:**

```javascript
        this.setState((prevState) => ({
          user: {
            ...prevState.user,
            age: 42,
          },
        }));
```