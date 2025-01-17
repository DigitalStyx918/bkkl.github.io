I created this fork because I have some ideas to make the Tetris game more friendly both with PC and mobile devices.  This is my first time to do anything on the devolopment side of github.

I am self-taught in Javascript, HTML, and CSS on an as needed basis.  I am personally interested in this project to make the Tetris app available for use on Oculus Quest as part of my own Amblyopia treatment.

My necessary goals for my intended use are to change the gamepad mapping to use an Xbox controller and to add the abilities to start the game, enter VR, and reset the game using the gamepad or at least clickable buttons so that this app will be mobile friendly.

# Amblyopia (Lazy Eye) WebVR Polyfill examples. 
This site contains a number of example WebVR Programs that show the potential of 
creating games and apps to help with Amblyopia therapy.  Specifically:

1) Amblyopia Letter Game (very modified from Tetris source from "http://www.smashinglabs.pl") 
2) Amblyopia WebVR Tetris (original Tetris source from "http://www.smashinglabs.pl") 
3) Simple rotating cubes showing use of WebVR layers for left/right/stereo object placement

The source for the three.js tetris game was merged with the WebVR Polyfill examples below. 
WebVR Polyfill was used choosen for iphone VR compatiblity.  
No attempt was made to perserve the itegrity of the various repositories of the sources used 
in these examples.  Various depricated API were manually patched.   

These programs prove that standard commerical VR platforms (Oculus, Iphone, Android..) and 
WebVR can easily be used to create therapeutic games and apps for Amblyopia. 

The hope is the mainline repositories for VR development will explicitly document features 
to enable Amblyopia friendly features in nearly all VR games and apps. It's estimated that 
about 2 to 3 percent of the U.S. population has some degree of amblyopia.

All information and links on this site should be considered experimental coding examples and
not intended for actual therapeutic use.  Any experimentation should be done under the 
supervision of medical professionals.  All  safety and use guidelines for the VR gaming system 
should be followed.  


https://www.vrlazyeye.com/


# WebVR Polyfill

A JavaScript implementation of the [WebVR spec][spec]. This project lets you use
WebVR today, without requiring a [special][moz] [browser][cr] build. It also
lets you view the same content without requiring a virtual reality viewer.

Take a look at [basic WebVR samples][samples] that use this polyfill.

[moz]: http://mozvr.com/
[cr]: https://drive.google.com/folderview?id=0BzudLt22BqGRbW9WTHMtOWMzNjQ
[samples]: https://toji.github.io/webvr-samples/
[spec]: https://mozvr.github.io/webvr-spec/

## Implementation

The polyfill decides which VRDisplays to provide, depending on the configuration
of your browser. Mobile devices provide the `CardboardVRDisplay`. Desktop devices
use the `MouseKeyboardVRDisplay`.

`CardboardVRDisplay` uses DeviceMotionEvents to implement a complementary
filter which does [sensor fusion and pose prediction][fusion] to provide
orientation tracking. It can also render in stereo mode, and includes mesh-based
lens distortion. This display also includes user interface elements in VR mode
to make the VR experience more intuitive, including:

- A gear icon to select your VR viewer.
- A back button to exit VR mode.
- An interstitial which only appears in portrait orientation, requesting you switch
  into landscape orientation (if [orientation lock][ol] is not available).

`MouseKeyboardVRDisplay` uses mouse events to allow you to do the equivalent of
mouselook. It also uses keyboard arrows keys to look around the scene
with the keyboard.

[fusion]: http://smus.com/sensor-fusion-prediction-webvr/
[ol]: https://www.w3.org/TR/screen-orientation/


## Configuration

The polyfill can be configured and debugged with various options. The following
are supported:

```javascript
WebVRConfig = {
  // Flag to disabled the UI in VR Mode.
  CARDBOARD_UI_DISABLED: false, // Default: false

  // Forces availability of VR mode, even for non-mobile devices.
  FORCE_ENABLE_VR: true, // Default: false.

  // Complementary filter coefficient. 0 for accelerometer, 1 for gyro.
  K_FILTER: 0.98, // Default: 0.98.

  // Flag to disable the instructions to rotate your device.
  ROTATE_INSTRUCTIONS_DISABLED: false, // Default: false.

  // How far into the future to predict during fast motion (in seconds).
  PREDICTION_TIME_S: 0.040, // Default: 0.040.

  // Flag to disable touch panner. In case you have your own touch controls.
  TOUCH_PANNER_DISABLED: false, // Default: true.

  // Enable yaw panning only, disabling roll and pitch. This can be useful
  // for panoramas with nothing interesting above or below.
  YAW_ONLY: true, // Default: false.

  // To disable keyboard and mouse controls, if you want to use your own
  // implementation.
  MOUSE_KEYBOARD_CONTROLS_DISABLED: true, // Default: false.

  // Prevent the polyfill from initializing immediately. Requires the app
  // to call InitializeWebVRPolyfill() before it can be used.
  DEFER_INITIALIZATION: true, // Default: false.

  // Enable the deprecated version of the API (navigator.getVRDevices).
  ENABLE_DEPRECATED_API: true, // Default: false.

  // Scales the recommended buffer size reported by WebVR, which can improve
  // performance.
  BUFFER_SCALE: 0.5, // Default: 0.5.

  // Allow VRDisplay.submitFrame to change gl bindings, which is more
  // efficient if the application code will re-bind its resources on the
  // next frame anyway. This has been seen to cause rendering glitches with
  // THREE.js.
  // Dirty bindings include: gl.FRAMEBUFFER_BINDING, gl.CURRENT_PROGRAM,
  // gl.ARRAY_BUFFER_BINDING, gl.ELEMENT_ARRAY_BUFFER_BINDING,
  // and gl.TEXTURE_BINDING_2D for texture unit 0.
  DIRTY_SUBMIT_FRAME_BINDINGS: true // Default: false.
}
```

## Performance

Performance is critical for VR. If you find your application is too sluggish,
consider tweaking some of the above parameters. In particular, keeping
`BUFFER_SCALE` at 0.5 (the default) will likely help a lot.

## Development

If you'd like to contribute to the `webvr-poyfill` library, check out
the repository and install
[Node](https://nodejs.org/en/download/package-manager/) and the dependencies:

```bash
git clone https://github.com/googlevr/webvr-polyfill
cd webvr-polyfill
npm install
```


## License

This program is free software for both commercial and non-commercial use,
distributed under the [Apache 2.0 License](COPYING).


## Thanks

- [Brandon Jones][bj] and [Vladimir Vukicevic][vv] for their work on the [WebVR
  spec][spec].
- [Ricardo Cabello][doob] for THREE.js.
- [Diego Marcos][dm] for VREffect and VRControls.
- [Dmitriy Kovalev][dk] for help with lens distortion correction.

[dk]: https://github.com/dmitriykovalev/
[bj]: https://twitter.com/tojiro
[vv]: https://twitter.com/vvuk
[spec]: https://mozvr.github.io/webvr-spec/
[dm]: https://twitter.com/dmarcos
[doob]: https://twitter.com/mrdoob
