# Phaser3, Pixi, and Phonegap

This build toolchain is easy to set up once you know how to do it.




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


### Install

1. Drop the `.ipa` file into your phone with the Apple official app: `Apple Configurator 2`


## Using Phaser3 and Pixi

Both phaser.js and pixi.js are MIT licensed, so bundle away.

Phaser3 is under active development and it has some amazing effects.




## Building for Multiple platforms

Discuss how to build for android and ios, or multiple iphones.

### stub




## Emulating platforms

Discuss

### stub