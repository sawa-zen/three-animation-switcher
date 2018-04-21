# Utsuroi

![](./readme.gif)

[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

This is a plug-in for easy switching animation of blender models in Three.js.

### Demo

- [http://utsuroi.sawa-zen.com/demo/](http://utsuroi.sawa-zen.com/demo/)

### Setup

#### NPM Install

```bash
$ npm install utsuroi
```

#### Script Install

```html
<script src="utsuroi.js"></script>
```

### Basic Usage Example

#### How to create

```javascript
var utsuroi;

// Load asset
var loader = new THREE.JSONLoader();
loader.load('assets/model.json', (geometry, materials) {

  // Allow "skining" for all materials.
  materials.forEach(function(m) {
    m.skinning = true;
  });

  // Mesh
  var actor = new THREE.SkinnedMesh(geometry, materials);
  scene.add(actor);

  // AnimationMixer
  var mixer = new THREE.AnimationMixer(actor);

  // Create Utsuroi
  utsuroi = new Utsuroi(mixer, [
    {name: "Rest Pose", loop: true},
    {name: "Walk", loop: true},
    {name: "Jump", duration: 100},
    {name: "Fall"},
    {name: "Attack", duration: 70}
  ], "Rest Pose");

  // start motion
  utsuroi.play();
});
```

#### How to update animation

```javascript
var clock = new THREE.Clock();

function tick() {
  requestAnimationFrame(tick);
  if(utsuroi) {
    var delta = clock.getDelta();
    utsuroi.update(delta);
  }
}

tick();
```

#### How to change action

```javascript
utsuroi.to('Walk');
```
