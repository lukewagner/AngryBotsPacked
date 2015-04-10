# AngryBotsPacked
This is a <a href="http://lukewagner.github.io/AngryBotsPacked">demo</a> of [asm.js-pack](https://github.com/lukewagner/asm.js-pack) applied to the WebGL export of the Unity 5 [AngryBots demo](http://beta.unity3d.com/jonas/AngryBots/). Runs in Firefox, Chrome and Safari.

STR:
 1. Start with WebGL export of standard AngryBots demo in Unity5
 2. Split `Release/AngryBots.js` into two files:
  - `AngryBots-asm.js`: containing a single top-level asm.js function `asmModule`
  - `AngryBots-glue.js`: containing all the glue code to link `asmModule` to the browser
 3. `cp -r asm.js-pack/out/* Release` after checking out and building [asm.js-pack](https://github.com/lukewagner/asm.js-pack).
 4. `asmjspack AngryBots-asm.js AngryBots-asm.packed`
 5. Change the loading of `AngryBots.js` in `index.html` to instead call `unpackAsmJS('AngryBots-asm.packed')` and, when the returned promise is resolved, store the unpacked asm.js module to the global variable `asmModule` then load `AngryBots-glue.js` to start the app.

**I realize this should just be an Emscripten flag; one step at a time :)**
