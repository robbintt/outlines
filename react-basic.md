
### React Basics

This is a draft version of a react outline from basics.  Send PRs to correct any misconceptions.


### Resources

1. [react-boilerplate](https://github.com/mxstbr/react-boilerplate)
2. [React official docs](https://facebook.github.io/react/)
3. [plot.ly React Tutorial](http://academy.plot.ly/react/1-introduction/)


### Getting Started

1. Basics Capabilities - React Official Docs

    1. React can be used in:
        - Frontend Stack
        - React Native (mobile)
        - Server Side (node)
    2. React Components:
        - Keep state out of DOM
        - Encapsulated
        - Compose them to make complex UIs
        - Build them
    3. Declarative Views
        - Design Simple Views for each state in your application
        - React efficiently updates and renders just the right components when the data changes

### Plot.ly Introduction - Weather App
    
1. Who uses react? Netflix, Airbnb, etc.

2. Why React? For **"building large applications with data that changes over time"**
    - Components: composable, reusable, encapsulated

3. Lets Build: A Weather App
    1. [react.jsbin.com](https://react.jsbin.com/sewaru/11/edit?js,output) - a fully featured react environment
    2. React is 2 Libraries:
        1. `React` - allows you to create `ReactElements`
        2. `ReactDOM` - renders the `ReactElements`
        3. Why the split? You could theoretically render those `ReactElements anywhere
    3. 
        ```javascript
        ReactDOM.render(
            React.createElement('h1', {className: 'heading'}, 'Hello World!'),
            document.getElementById('container')
        );
    4. `ReactDOM.render()` will render a `ReactElement` created by `React.createElement()`

