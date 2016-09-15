
### React Basics

This is a draft version of a react outline from basics.  Send PRs to correct any misconceptions.


### Resources

1. [react-boilerplate](https://github.com/mxstbr/react-boilerplate)
2. [React official docs](https://facebook.github.io/react/)
3. [plot.ly React Tutorial](http://academy.plot.ly/react/1-introduction/)
    - Part 1: This section is confusingly written but the example is quite nice. See below.


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

3. Lets Build: A Counter that updates state.
    1. [react.jsbin.com](https://react.jsbin.com/sewaru/11/edit?js,output) - a fully featured react environment
    2. React is 2 Libraries:
        1. `React` - allows you to create `ReactElements`
        2. `ReactDOM` - renders the `ReactElements`
        3. Why the split? You could theoretically render those `ReactElements` anywhere
        4. Boilerplate HTML for this section

            ```html
                <!DOCTYPE html>
                <html>
                <head>
                  <meta charset="utf-8">
                  <title>React</title>
                  <link rel="stylesheet" href="http://cdnjs.cloudflare.com/ajax/libs/normalize/3.0.1/normalize.css">
                  <script src="//fb.me/react-with-addons-0.14.3.js"></script>
                  <script src="//fb.me/react-dom-0.14.3.js"></script>
                </head>
                <body>
                  <div id="container"></div>
                </body>
                </html>
            ```

    3. Example

        ```javascript
        ReactDOM.render(
            React.createElement('h1', {className: 'heading'}, 'Hello World!'),
            document.getElementById('container')
        );
        ```

    4. `ReactDOM.render()` will render a `ReactElement` created by `React.createElement()`
        - The DOM node we want to render (2nd argument) is called the `entry point`
        - `ReactElements` take three arguments:
            1. The node we want to create (HTML Element)
            2. A JavaScript Object of information (like 'type')
            3. Optionally a child such as `innerText` or another `ReactElement` 
                - A child element like this does get `null` for the second argument

    5. Components: Creating a `ReactComponent`
        1. Component is a function that receives `props` - short for properties

            ```javascript
            // What is the purpose of props here? Does it allow us to pass the child ReactElement?
            var Wrapper = function(props) {
                return(
                    React.createElement('div', { className: 'wrapper'}, props.children);
                );
            }
            React.createElement(Wrapper, {}, 'Hello World!');
           
            ReactDOM.render(
                React.createElement(Wrapper, null,
                    React.createElement('h1', { className: 'heading' }, 'Hello World!')
                ),
                document.getElementById('container')
            ); 
            ```

    6. Converting our `ReactComponent` to `JSX`
        1. `JSX` is 'nothing but a wrapper on `React.createElement`
            - To use Javascript in JSX, wrap it in curly braces.
            - `JSX` always must be transpiled with a build tool.

        2. How to `transpile` JSX in your build environment?
            - Babel / Gulp - [`npm install --save-dev babel-cli babel-preset-react`](https://babeljs.io/docs/plugins/preset-react/)
            - 

            ```javascript
            var Wrapper = function(props) {
                return (
                    <div className="wrapper">{ props.children }</div>
                );
            };
            ReactDOM.render(
              <Wrapper>
                <h1 className="heading">Hello World!</h1>
              </Wrapper>,
              document.getElementById('container')
            );
            ```
    7. Classes - 
        1. Event handlers like `onClick`, `onMouseOver`, etc. **CANNOT** go in a ReactComponent.
            - These handlers must be attached to an actual DOM node.
            - This 'Counter' object actually demonstrates passing Event Handlers.
        
                ```javascript
                class Counter extends React.Component {
                    render() {
                        return (
                            <div>
                                <p>This is a Counter component!</p>
                                <Button text="Click me!" onClick={function() { console.log('click!') }} />
                            </div>
                        );
                    }
                }
                // Button pulls `props` from ReactComponent JSX (React.CreateElement)
                var Button = function(props) {
                    return (
                        <button onClick={ props.onClick }>{ props.text }</button>
                    );
                }
                ReactDOM.render(
                    <Counter />
                    document.getElementById('container')
                );
                ```

        2. Handling State - State is a plain object in react, with any number of properties.
            - `constructor` is used to assign initial state 
            - Lets make counter do what it is supposed to do with state.
            - The `{ }` JSX notation works with any variable, example `{ myPotato }`

                ```javascript
                class Counter extends React.Component {
                    constructor() {
                        super();
                        this.state = {
                            clicks: 0
                        };
                        // "`this` is undefined in `increment` because of the way `ES6 Classes` work
                        // This explanation is terrible. Why again must we bind `this`?
                        // Trent: According to MDN, bind will make a new `bound function` and bind whatever you pass as `this` for that function. The bound function wraps the original function object.
                        // Trent: But why is increment set in the constructor? Is increment constructed before the constructor? Maybe... not sure. Alternative idea: Can you bind a function and then define it?
                        this.increment = this.increment.bind(this);
                    }

                    increment() {
                        this.setState({
                            clicks: this.state.clicks + 1
                        });
                    };

                    render() {
                        return (
                            <div>
                                <p>This is a Counter component! The button was clicked { this.state.clicks } times.</p>
                                <Button text="Click me!" onClick={function() { console.log('click!') }} />
                            </div>
                        );
                    }
                }
                // Button pulls `props` from ReactComponent JSX (React.CreateElement)
                var Button = function(props) {
                    return (
                        <button onClick={ props.onClick }>{ props.text }</button>
                    );
                }
                ReactDOM.render(
                    <Counter />
                    document.getElementById('container')
                );
                ```

            - Whenever the state changes, the `<p>` element is updated.
