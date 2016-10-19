

### React Animation

- Speaker:

- About Speaker: Comes from game development industry


#### Game Animation

- 30 FPS doesn't really work out, you need to get to 60 fps
- Debugging is very challenging


#### Webapps

- Sad about the animation quality (gives a number of really terrible animation examples.
- CSS3 animations
    - better performance
    - fairly easy to use
    - no programmatic control - trigger and forget
    - cross browser support (it's better now)

- DOM 
    - Incredibly slow
    - Inconsistent API with bad cross-browser support
    - never meant to support complex single page apps
- Single page apps
    - Code and state management is near impossible in a jQuery App
    - State management is bad in backbone

- But - `react` + `redux`
    - fast rendering
    - fast state management


#### So with `react+redux` can we do the cool stuff from the game dev industry?
- We don't have the years of experience and code patterns...
- (get the example from the presentation)
    - sets css3 `opacity` from reducer based on scroll
    - `getOpacityFromScroll(action.yScroll)`
    - use `connect` to make sure react component can listen to and get state of the redux store
    - connect is a library that works between react and redux. quite popular?
    - one way data flow, set and forget
    - very performant, fluid
        - did not use time control but redux has it
        - in redux you can go frame by frame with time control to debug weird animation frames
- can we make the demo better?
    - maybe make middleware
    - perhaps write a general animation library based on the concept
        - wraps the whole thing (jquery but in react/redux)


#### Questions

- Have you tried particle systems based on this demo?
    - not yet but i want to 
- "Sara Drasner" or something that sounds similar is an authority on doing this sort of particle based animation
- question person: shoutout to "greenstuff" or something similar, GSAP animation library?
- Are you using react native at instacart?
    - no we are in native and we are moving code to swift, we are trying to get all our code to swift
