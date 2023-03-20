# Learning HTML5 Native Game Dev

It looks like there are a lot of different ways to do this, and games are typically packaged for ios using phonegap or cordova.

## Goals

1. Make some simple games in `html5`
2. Somehow translate the games to `mobile native (Android & iOS)`
	- Otherwise I may have to relearn a lot of platform specific knowledge...
3. Leverage existing javascript libraries for multiplayer, maybe even run a server/api for play between phone and browser users


## Trajectory

1. Package someone else's game for iOS with Phonegap (or Cordova) just to see it happen.
1. I plan to use the default `phonegap hello world` app to test this out.
1. Make modifications to the game and package again to iOS.


## More Engines!

- This site [https://html5gameengine.com/](https://html5gameengine.com/) has way more engines!
- This llst [https://github.com/collections/javascript-game-engines](https://github.com/collections/javascript-game-engines) has a lot more js frameworks...

## Notes

- `SVG Keyframe animations` may be sort of restricted to data visualization, not games
- Game Engines tend to use `webgl` and fallback to `canvas`
- Converting to iOS
	- still done with `phonegap` or `cordova`
	- can be done (partially, not full POC) [without a conversion framework](https://www.gamasutra.com/blogs/HaroldBowmanTrayford/20180124/313387/Phaser_to_iOS_without_PhoneGap_or_Cordova__Touch__Sound.php)


## Option: phaser.js

They offer a community edition and a paid product.  They claim it is intended to be packaged for native apps. I wonder if many examples of this exist. I should get it up and running for ios and android. It is the 2nd most starred on github after pixi.js.

Phase is a 2d game engine.

### Resources

- 



## Option: react-game-kit

Pitch from the dev:

- Use the same game code for web, iOS, android
- Use react
- Hot reload game logic
- Don't have to learn unity


### References

[source](https://github.com/FormidableLabs/react-game-kit)

[interactive guide](http://reactnext.surge.sh/)


### Recommendations

Jeffrey built [this](https://jeffreyatw.github.io/react-redux-platformer)  ([source](https://github.com/JeffreyATW/react-redux-platformer)).

> i made this once. this uses `matter.js` as well as `react-game-kit`, the status of which i’m unaware. seems straightforward enough, although it uses the DOM instead of canvas, which i’m iffy about - Jeffrey

> Formidable Labs does great stuff - Nick


## Option: PlayCanvas

I signed up for this with a google account.  It seems to provide an environment for pretty rich 3d art. I doubt you would develop the assets in playcanvas, but I don't know that much about it.  It doesn't seem like quite what I am looking for.

PlayCanvas is a suite of products:

- PlayCanvas Engine
	- Open Source / MIT Licensed on Github: [PlayCanvas Engine](https://github.com/playcanvas/engine)
	- "The open-source PlayCanvas Engine is the world's most advanced WebGL game engine. Use JavaScript to program anything from simple 2D games to advanced 3D graphics simulations. All written in standards-compliant, cross-platform HTML5 for every major browser and device."
	- Tiny footprint, mobile optimized: "The PlayCanvas Engine has a tiny footprint that loads and executes incredibly quickly. The PlayCanvas Engine gives incredible performance, even on devices such as the iPhone 4S."
- a webgl authoring tool, with a UI similar to adobe products.


## Option: pixi.js

2D Sprite Managment.  PixiJS is a rendering library, so you still need the game framework. It's sounding like there is a standard way to pack javascript into a native app, so that might not be important.


### References

- [learning pixi](https://github.com/kittykatattack/learningPixi)
- [source](https://github.com/pixijs/pixi.js)



## Option: Unreal Engine 4

Does html5, maybe overkill.




