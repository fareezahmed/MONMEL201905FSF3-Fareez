# React component lifecycle methods
React components lifecycle methods can be described as events that take place from any component’s inception to the death of that same component. The lifecycle of a React component takes place within these events that are in four categories:

## Mounting: 
### The methods and events that take place here happen as the component is mounted in the DOM.

## Updating: 
### Here the methods and events take place after the React component has entered the DOM.

## Un-mounting: 
### Here the methods and events take place as they React component leaves the DOM or is unmounted from the DOM.

## Error Boundaries: 
### Here is a special category that deals with handling or gracefully catching errors in order not to totally break your React application render.

In this post, the React lifecycle methods will be explained in the order they are called by React in the DOM.


## render()
This is the most important method of any React class, the whole work that is going to appear in the DOM is done here as it outputs the JSX of your component. It is the most used React lifecycle method and it is the only required method in any React class.

```js
    render(){
     console.log("render method is called here");
     return <div>Hello world!</div>
    }
```
You are not however allowed to set state inside the render method as it should be pure. Pure functions are functions without side effects, they must always return the same outputs when the same corresponding inputs are passed into them.

## componentDidMount()
This method is called immediately after the render method call as soon as the component is mounted. Inside this method is where you are allowed to do all the behind the scenes work you need without the DOM. These things can range from setting state, initializing and loading data and even adding event listeners. The syntax looks like this:
```js
    componentDidMount() {
     console.log("componentDidMount was called here");
    }
```
If setState is called inside this method, the DOM is re-rendered to reflect the modification. This method is perfect for making AJAX calls.


## shouldComponentUpdate()
This is the method that is called right after the componentDidMount method, this method does not allow you set state in it. It is useful for when you do not want your props or state changes re-rendered, it is like a bridge where you have to get permission if a component should be updated based on the props or state changes made. It returns a boolean, usually true by default. The syntax looks like this:
```js
    shouldComponentUpdate(nextProps, nextState) {
      console.log("should component update is called here!");
      return nextState.cars.length < this.state.cars.length;
    }
```
It takes in two arguments, nextProps and nextState and with those you can you can make your return conditions for the re-render. It is advised that this method be used with care and for optimization purposes keep in mind that it can trigger re-renders.


## componentWillUnmount()
This method is called just before a component is unmounted from the DOM, it is the method called right after componentDidUpdate. Here is where your clean up logic should go, clearing counters and caches, cancel API requests or removing things like event listeners. It can look like this:
```js
    componentWillUnmount(){
      console.log("componentWillUnmount was called here!");
      window.removeEventListener("restart");
    }
```
As you might have guessed, you cannot set state in this method because that would automatically have to cause a re-render most times. After this, your component is gone, for good.