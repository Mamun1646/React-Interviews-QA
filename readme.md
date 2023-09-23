#React Interview Questions

## Why should we not update the state directly?

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