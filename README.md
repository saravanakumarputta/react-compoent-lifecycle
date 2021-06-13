# Life Cycle Methods of React Component

The Life Cycle Methods of a React Component is catagorized into phases as below.

1. **Mounting** - When the component is being render in the DOM.
2. **Updating** - When the component is re-rendered on the chnages happened to its props/state of the component.
3. **UnMounting** - When the component is rempved from the DOM,

## Mounting

1. constructor
2. static getDerivedStateFromProps
3. render
4. componentDidMount

### constructor:

- Invoked when the component gets created.
- should always call `super(props)`.
- Initialize the state of the component.
- Bind the Event Handlers.
- No to do - Make any Http requests.

```
constructor(props){
  super(props)
}
```

### static getDerivedStateFromProps

- Invoked after the `constructor`.
- It receives two arguments - props, state.
- React documentation states that this is rarely used method.
- Used only when the state of the component changes based on the props.
- It always return the state/null.
- No to do - Make any Http requests.

```
static getDerivedStateFromProps(props, state){
  return null/state;
}
```

### render

- Invoked after the `getDerivedStateFromProps`.
- It is a pure function and returns the JSX(Which is actual UI).
- It can contain other components as `children`.
- Not to do - Should not make any state updates. On not doing so it will cause the infinite render method triggers in the updating phase.
- It also triggers the `children` component's life cycle method if any children is present.

```
render(){
  return <div>Hi, From the render</div>
}
```

### componentDidMount

- Invoked after the `render` and all its `children` components are rendered to the DOM.
- Typically used for making the HTTP requests.

```
componentDidMount(){
  fetch('https://randomuser.me')
}
```

## Updating

1. static getDerivedStateFromProps
2. shouldComponentUpdate
3. render
4. getSnapshotBeforeUpdate
5. componentDidUpdate

### static getDerivedStateFromProps

- In invoked every time the component gets re-rendered.
- It receives two arguments - props, state.
- React documentation states that this is rarely used method.
- Used only when the state of the component changes based on the props.
- It always return the state/null.
- No to do - Make any Http requests.

```
static getDerivedStateFromProps(props, state){
  return null/state;
}
```

### shouldComponentUpdate

- It receives the updated props, state as arguments.
- It can prevent the component from re-rendering.
- If the returned value is true -> Component will re-render, if it is false -> Component will nor re-render.
- This method is used for performance optimization.

```
shouldComponentUpdate(nextProps, nextState){
  //Comparison Logic
  return true/false;
}
```

### render

- Invoked after the `shouldComponentUpdate` result..
- It is a pure function and returns the JSX(Which is actual UI).

```
render(){
  return <div>Hi, From the render</div>
}
```

### getSnapShotBeforeUpdate

- Invoked right before the changes in the Virtual DOM are to be reflected to the DOM.
- It receives the previous props and state as arguments.
- This method either return `null` or `value`.
- The returned value is passed to the next life cycle metho. ie `componentDidUpdate`.
- Rarely used methods as per React's Documentation.
- Example: Maintaining the Scroll Postion on the updates.

```
getSnapShotBeforeUpdate(prevProps, prevState){
  return null/{data: {}}
}
```

### componentDidUpdate

- Invoked after the render is finished in the re-render cycles.
- It receives previous props, state and snapshot value as arguments.

```
componentDidUpdate(prevProps, prevState, snapshot){
  //Business Logic
}
```

## UnMounting

1. componentWillUnmount

### componentWillUnmount

- Invoked before remving the component from DOM.
- Used to clean up the event listeners/subscriptions of the component.

```
componentWillUnmount(){
  document.getElementById('scrollBox').removeEventListener('scroll', handleScroll)
}
```
