

### React Async


- Speaker:
- Works at: HelloSign

Plans to give 60 free seats at reactuniversity.com.


#### High level summary

- React has won on the UI side.
    - Angular 2 similar to react
    - Ember moved to component approach

- Stuff missing in `redux` with `async`
    - There is middleware `redux-saga` for async

- New frontier in javascript is async

#### JavaScript Revolution

- JQuery, Backbone, Knockout, Angular, Angular2, etc.
    - Now we are seeing the patterns emerge and react has 'won'
    - But react is just one part of the architecture
        - Should only handle view layer
- State management: `redux` has simplified it
    - "redux is a great step forwards"
- Redux:
    - Manage state through pure functions and unidirectional data flow
    - Your UI becomes a state machine
    - hen your redux store state changes your react views respond with new data
    - `HelloSign` has 5 single page apps. Some started implementing redux
        - Result: moved business logic out of react components which is the goal

### Redux is a workflow - NOT a "complete architecture"
- We need an architecture on top of redux   
    - Approach to this: redux middleware
        - think of middleware as a third party extension - django analogy
    - uses currying to dispatch... (see slides)
- Lets look at some code examples
- Promises: only three states
    - pending
    - ??
    - rejected
- However, async we also need to be able to cancel async processes
- Redux documentation says `redux-thunk` but the author says - this is wrong
    - `redux-thunk` is a function that wraps an expression to delay its evaluation
- Wrap whatever function into another function and have the middleware (`redux-thunk`) run it later
    - speaker has an example of redux-thunk wrapping in the presentation
- `redux-thunk` evaluation: 
    - Great for small projects
    - super simple
    - fast to run
    - easy to test in node
    - dependency injection is hard to do...
        - recently redux allows passing an extra value in the thunk
        - but you always have to pass your dependencies in here which adds a lot of code
    - fsa - flux standard action
        - a set of standards describing what an action should look like
    - redux thunk is not fsa compliant
    - doesn't scale well
        - tons of action creators dispatching functions, hard to track down
    - "too easy to forget error handling and pending state"
        - forgetting to do the cache
        - forgetting to set a spinner when loading
    - no way to cancel a thunk - ouch
- `rxjs`: Reactive eXtensions for JavaScript
    - functional reactive programming 
        - need to have a masters or phd to understand functional js
    - If Functional Reactive Programming (FRP) is your thing this is for you
    - netflix uses it a ton
    - does a lot of stuff redux already does, it's probably not a good thing to use WITH redux.
    - `rxjs` is really robust already
- `redux-saga`: `saga pattern` in redux
    - author uses a ton at `HelloSign`
    - based on generators
        - author considers generators a better strategy than async await in many cases
    - "turns your async code into a pillar of your architecture"
    - instead of dispatching `thunk`s, you create `saga`s to gather all your Side Effects logic in a central place
    - `saga pattern`: ... (look it up, there's a technical paper about it)

#### Wrapup

- Redux is great for managing state but incomplete; missing:
    - `

He just skipped this slide...  get the slides


#### Questions

- Generators is a learning curve with redux saga "The 80/20 of Generators" - book
    - create your own babel and something or other
    - Title is probably: "The 80/20 of ES2015 Generators" by Valeri Karpov
- guy comments: angular 2 observables can be used in the same way as redux-saga
- guy question: are observables the future?
    - speaker: observables got pushed back and there has been actual pushback against it
        - netflix is pushing hard for something or other with observables, maybe 'falcor'
- react, redux etc support ie8 i guess, or maybe just hellosign? 
- Highlight of promise to saga is cancelable. If that is async how is it really cancelable?
    - My undestanding is that it stops calling .next on it, maybe...
    - or just drops the result as a cancel maybe?
    - `try... catch` has `finally` which may be responsible for canceling

