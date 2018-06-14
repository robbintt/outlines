# Phaser3, Pixi, and Phonegap

This build toolchain is easy to set up, with practice.


## Questions

1. What version of pixi.js does phaser3 use?  Check phaser3 source.
1. What pixi.js plugins does phaser3 use? - Check phaser3 source.
1. How do canvas sizes interact with platform builds? Is there a dynamic canvas size or some canvassize  detection method? Or is it done another way?
	- what is this: `game.scale.setGameSize(x, y)`
	- `renderer.resize` may be relevant
	- Look into 'scalemanager' which may still be in dev, see [issue #3148](https://github.com/photonstorm/phaser/issues/3148)
	- Here is an [article on scaling in phaser](https://www.joshmorony.com/how-to-scale-a-game-for-all-device-sizes-in-phaser/)
1. Question for later: Do I need to be using phonegap? Why not [just use cordova?](https://cordova.apache.org/#getstarted)
	- Well... how would I build the IPA? Figure this out later...

## Phonegap

Phonegap build is a webapp that will build from your hosted repos, but you do need to provide an app key from Apple, which takes awhile to set up. 


### Set Up

1. You can build and test directly in phonegap. This development environment is intended to be faithful to all platforms
	- What issues exist and can be checked for, and how?
1. Apple Developer account + $99+tax fee
1. Register devices for testing
1. Generate a key and get it signed for your account and device
1. Build, Download, and Install the app on your device (phone, tablet, even laptop via steam??)


### Build

1. Use the phaser + phonegap [framework]() managed by Adobe (see trello to fill this in).
1. `npm install -g phonegap@latest`
1. `phonegap create ./MyPhaserApp --template phonegap-template-phaser`
1. You can then use phonegap (I used the macos app ui) to test the project.
1. You can also use phonegap (I used the phonegap-build webapp) to build the project for target devices.


### Build from a custom/local phonegap app template

I replaced the `phonegap-template-phaser`, which I guess defaults to the NPM package, and I used a filepath instead.   It copied everything over, but didn't create everything that the node app created. It seemed to skip three folders: `.  `phonegap --template` just wraps [cordova --template](https://cordova.apache.org/docs/en/latest/guide/cli/template.html).

The above worked fine but when building my phaser `.ipa` demo, I actually copied a phaser2 project (the project created from the `phonegap --template` command), then added the phaser 3.10.1 files to that.

My Phaser3 retrofit app runs with the [Phaser3 "hello world" demo](http://phaser.io/tutorials/getting-started-phaser3/part5)!

#### Issues

I think you can also use a git remote with cordova because of the [phonegap source code](https://github.com/phonegap/phonegap-cli/blob/master/lib/phonegap/create.js#L118). However, I tried to specify one and it told me it can't find the package.json, so something seems to be going wrong?



### Install

1. Drop the `.ipa` file into your phone with the Apple official app: `Apple Configurator 2`


## Using Phaser3 and Pixi

Both phaser.js and pixi.js are MIT licensed, so bundle away.

Phaser3 is under active development, and phaser3 has already been released.

Pixi.js is also actively developed.

### Phaser 2 Examples

[here](http://phaser.io/examples)


### Phaser 3 Examples


### Phaser 2 Sandbox

There's a [Phaser 2 sandbox](http://phaser.io/sandbox) for quick and dirty testing.

### Phaser 3 Sandbox

If this is broken you can get a phaser 3 sandbox in the phaser examples app.

This [also exists](http://labs.phaser.io/edit.html).

### Use pixi.js in phaser2

[This is from 2016](https://gamedev.stackexchange.com/questions/121218/how-do-i-add-a-pixi-container-into-a-phaser-game)

> All Phaser display objects (group, sprites...) are based on PIXI ones. PIXI objects can be rendered in phaser render tree. the only problem is the update and postUpdate function.

> I solved it adding this simple patch:

```
PIXI.DisplayObject.prototype.update = function () { };
PIXI.DisplayObject.prototype.postUpdate = function () { };
```

> this patch adds a empty function for "update" and "postUpdate" methods in PIXI displayObjects prototype. In that case Phaser update tree founds a function to execute.


### Input in Phaser

We want mobile-first multiplatform, which means we really only have multitouch events to go off of, and the relationship of those events to regions of the screen...

[some info](http://www.html5gamedevs.com/topic/1764-how-to-capture-a-touch-event-on-mobile-device/)


## Building for Multiple platforms

Discuss how to build for android and ios, or multiple iphones.

### stub




## Emulating platforms

Discuss

### stub