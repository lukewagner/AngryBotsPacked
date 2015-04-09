# AngryBotsPacked
This is a <a href="http://lukewagner.github.io/AngryBotsPacked">demo</a> of [asm.js-pack](https://github.com/lukewagner/asm.js-pack) applied to the WebGL export of the Unity 5 [AngryBots demo](http://beta.unity3d.com/jonas/AngryBots/).

STR:
 1. Start with WebGL export of standard AngryBots demo in Unity5
 2. Split `Release/webgl.js` into two files:
  - `webgl.asm.js`: containing a single top-level asm.js function
  - `webgl-glue.js`: containing all the glue code to link and glue the asm.js module to the browser, assuming the asm.js module is a global variable named `asmModule`
 3. `cp -r asm.js-pack/out/* Release` after checking out and building [asm.js-pack](https://github.com/lukewagner/asm.js-pack).
 4. `asmjspack webgl.asm.js webgl.asm` to pack the asm.js file.
 5. Change the loading of `webgl.js` in `index.html` to instead call `unpackAsmJS('webgl.asm')` and, when the returned promise is resolved, store the unpacked asm.js module to the global variable `asmModule` then finally load `webgl-glue.js` to start the app.

Runs in Chrome and Firefox.  (Seems to have black textures on the floors in both browsers on Linux, but that is a pre-existing issue.)

**I realize this should just be an Emscripten flag; one step at a time :)**
