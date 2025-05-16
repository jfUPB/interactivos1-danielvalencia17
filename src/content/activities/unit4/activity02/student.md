#### Solucion a la actividad

```js

var c;
var lineModuleSize = 0;
var angle = 0;
var angleSpeed = 1;
var lineModule = [];
var lineModuleIndex = 0;

```
Esta es la parte inicial del codigo donde se inicializan las variables, basicamente es el punto donde comienza las variables que genera la linea, el line module esta vacio esperando a que cambiemos los pinceles y modos de pintura.

```js
function setup() {
  createCanvas(windowWidth, windowHeight);
  background(255);
  //cursor(CROSS);
  noCursor();
  strokeWeight(0.75);

  c = color(181, 157, 0);
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```
Esto basicamente es la parte incial de canvas, crea la configuracion inicial del lienzo.

```js
function draw() {
  if (mouseIsPressed && mouseButton == LEFT) {
    var x = mouseX;
    var y = mouseY;

    if (keyIsPressed && keyCode == SHIFT) {
      if (abs(clickPosX - x) > abs(clickPosY - y)) {
        y = clickPosY;
      } else {
        x = clickPosX;
      }
    }

    push();
    translate(x, y);
    rotate(radians(angle));

    if (lineModuleIndex != 0) {
      tint(c);
      image(lineModule[lineModuleIndex], 0, 0, lineModuleSize, lineModuleSize);
    } else {
      stroke(c);
      line(0, 0, lineModuleSize, lineModuleSize);
    }

    angle += angleSpeed;
    pop();
  }
}
```
Esta es la zona que se encarga del dibujo, no toma tnato en cuenta las variables de pincieles, es mas como la base del dibujo que luego se modifica con los if.

```js
function mousePressed() {
  lineModuleSize = random(50, 160);
  clickPosX = mouseX;
  clickPosY = mouseY;
}
```
Esto es lo que le los movimientos del mouse.

```js
  if (key == ' ') c = color(random(255), random(255), random(255), random(80, 100));
  // default colors from 1 to 4
  if (key == '1') c = color(181, 157, 0);
  if (key == '2') c = color(0, 130, 164);
  if (key == '3') c = color(87, 35, 129);
  if (key == '4') c = color(197, 0, 123);

  // load svg for line module
  if (key == '5') lineModuleIndex = 0;
  if (key == '6') lineModuleIndex = 1;
  if (key == '7') lineModuleIndex = 2;
  if (key == '8') lineModuleIndex = 3;
  if (key == '9') lineModuleIndex = 4;
}
```
Cada uno de estos if se guarda en una variable mas arriba que es lo que cambia la forma, tamaño, color del pincel.

![250312_91414_711](https://github.com/user-attachments/assets/478c0e38-2d25-4c66-acae-0404277ad338)

Este es el dibujo que cree mientras entendia el funcionamiento.
