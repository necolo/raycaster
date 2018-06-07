# raycaster

Presents two function: `rayIntersectsTriangle` and `unproject`, can help finding the point in 3D world when click on the canvas. 

## Example

```js
const { vec3, mat4 } = require('gl-matrix');
const raycaster = require('raycaster');

canvas.addEventListner('mousedown', (ev) => {
    const { clientX, clientY } = ev;
    
    const ray = raycaster.unproject(
        [clientX, clientY],
        [0, 0, window.innerWidth, window.innerHeight], //assume the canvas is full-size
        projection, //your invert projection matrix
        view, //your invert view matrix
    );

    const intersectionPoint = vec3.create();
    const triangle = [ //example triangle
        vec3.fromValues(-1, -1, 0),
        vec3.fromValues(1, 1, 0),
        vec3.fromValues(-1, 1, 0),
    ];

    if (raycaster.rayIntersectsTriangle(
        eye, // your camera position
        ray,
        triangle,
        intersectionPoint,
    )) {
        console.log('hits', intersectionPoint);
    }
})
```