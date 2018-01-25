

THREE.VRController
==============================================================================

![THREE.VRController](https://github.com/davidlyons/THREE.VRController/raw/master/VRController.png "THREE.VRController")

__Generic VR controller handler for building [WebVR](https://webvr.rocks/) 
experiences with [THREE.js](https://threejs.org/).__ 
Wraps the [Web Gamepad API](https://www.w3.org/TR/gamepad/) to handle gamepad
discovery, emits a controller (`THREE.Object3D`) instance upon discovery, 
handles controller updates for position and orientation (including 
3[DOF](https://en.wikipedia.org/wiki/Degrees_of_freedom_(mechanics)) rigs
via the `OrientationArmModel`). Watches for updates on axes and button states
and emits corresponding events on the controller instance. Good for 
[HTC Vive](https://www.vive.com), [Oculus Rift](https://www.oculus.com/rift/), 
[Google Daydream](https://vr.google.com/daydream/), and beyond. Submitted to
[Three.js](https://github.com/mrdoob/three.js/) as 
[pull request #10991](https://github.com/mrdoob/three.js/pull/10991)
on Saturday, 11 March 2017.


Requirements
------------------------------------------------------------------------------
1. Virtual Reality rig with controllers such as the 
[HTC Vive](https://www.vive.com/),
[Oculus Rift](https://www.oculus.com/rift/),
[Google Daydream](https://vr.google.com/daydream/), or similar devices.
2. WebVR-capable browser. For the latest list of browsers
that support WebVR — as well as download and setup instructions — see 
[WebVR Rocks](https://webvr.rocks/).
3. Working knowledge of [THREE.js](https://threejs.org/).


Try it now!
------------------------------------------------------------------------------
Already on a VR rig with a WebVR-capable browser? Just point your browser to
[https://stewdio.github.io/THREE.VRController/](https://stewdio.github.io/THREE.VRController/)
to experience this code in action.


Do it yourself
------------------------------------------------------------------------------
1. Add our 
[VRController.js](https://github.com/stewdio/THREE.VRController/raw/master/VRController.js) file to your existing Three.js project and use our 
[index.html](https://github.com/stewdio/THREE.VRController/raw/master/index.html) 
example file as your guide for the following steps.
2. Add a `THREE.VRController.update()` function call to your animation loop.
3. Add a listener for the `"vr controller connected"` global event. This is 
how you will receive the controller object instance—which is a 
`THREE.Object3D`. This means you can add it to your scene, attach meshes 
to it, and so on.
4. When you receive the controller object instance you must give it some 
additional information depending on the type of controller. For 6DOF (room 
scale) rigs you must provide a standing matrix, easily obtained from your 
`VRControls` instance. (Note that `VRControls` and `VRController` may have 
similar names but are entirely different things.) This will look similar to:
`controller.standingMatrix = controls.getStandingMatrix()`
For 3DOF (seated) rigs you must provide a reference to the camera so the 
controller can use the headset’s live position and orientation to guess where 
it ought to be: `controller.head = camera` There’s no penalty for providing 
the controller instance with both `standingMatrix` and `head` properties as 
we do in the 
[example](https://github.com/stewdio/THREE.VRController/raw/master/index.html).
5. Explore the available touch, press, and trackpad events by assigning
`THREE.VRController.verbosity = 1`.
You’ll now see a flood of verbose comments in the JavaScript console as you
interact with your controller. To access controllers directly from the console
explore the `THREE.VRController.controllers` object.


Run locally
------------------------------------------------------------------------------
The easiest way to fire this up on your own desktop machine is to start a 
simple Python server. Open up a 
[command line prompt](https://en.wikipedia.org/wiki/Command-line_interface), 
navigate to wherever you’ve stored this code package, then type the 
following command depending on the version of 
[Python](https://en.wikipedia.org/wiki/Python_(programming_language)) you have
installed.  

Python 2: `python -m SimpleHTTPServer 8000`  
Python 3: `py -m http.server 8000`  

In your browser you can now navigate to 
[http://localhost:8000/](http://localhost:8000/) to see the demo running 
locally. You can shutdown the local server by returning to the command line 
and hitting Control + C.



