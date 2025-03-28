#### Solucion a la actividad

##### Codigo de microbit
```js
from microbit import *

uart.init(baudrate=115200)

while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(100)
    if button_b.is_pressed():
        uart.write('B')
        sleep(100)
    if accelerometer.is_gesture("shake"):
        uart.write('S')
        sleep(100)
    if pin_logo.is_touched():
        uart.write('L')
        sleep(100)
```
##### Codigo para p5.js
```js
let port;
let connectBtn;
let estado = 0;
let contador = 20;
let displayText = "Config";
let ultimoTiempo = 0;
let secuencia = [];
let secuenciaCorrecta = ['A', 'B', 'A', 'S'];

function setup() {
  createCanvas(400, 400);
  port = createSerial();

  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(width / 2 - 75, height / 2 + 160);
  connectBtn.mousePressed(connectMicrobit);

  textAlign(CENTER, CENTER);
  textSize(32);
  text(displayText, width / 2, height / 2);
}

function draw() {
  background(220);
  text(displayText, width / 2, height / 2);

  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);
    if (dataRx === 'A') {
      if (estado === 0 && contador < 60) {
        contador++;
        displayText = contador.toString();
      }
      if (estado === 1) {
        secuencia.push('A');
        verificarSecuencia();
      }
    } else if (dataRx === 'B') {
      if (estado === 0 && contador > 10) {
        contador--;
        displayText = contador.toString();
      }
      if (estado === 1) {
        secuencia.push('B');
        verificarSecuencia();
      }
    } else if (dataRx === 'S') {
      if (estado === 0) {
        estado = 1;
        displayText = "ARMED";
      }
      if (estado === 1) {
        secuencia.push('S');
        verificarSecuencia();
      }
    } else if (dataRx === 'L') {
      if (estado === 2) {
        resetear();
      }
    }
  }

  if (estado === 1) {
    let tiempoActual = millis();
    if (tiempoActual - ultimoTiempo >= 1000) {
      ultimoTiempo = tiempoActual;
      if (contador > 0) {
        contador--;
        displayText = contador.toString();
      } else {
        estado = 2;
        displayText = "EXPLOSION!";
      }
    }
  } else if (estado === 2) {
    explotar();
  }
}

function connectMicrobit() {
  if (!port.opened()) {
    port.open('MicroPython', 115200);
    connectBtn.html('Disconnect');
  } else {
    port.close();
    connectBtn.html('Connect to micro:bit');
  }
}

function explotar() {
  background(255, 0, 0);
  text("BOOM!", width / 2, height / 2);
}

function resetear() {
  estado = 0;
  contador = 20;
  displayText = "Config";
  secuencia = [];
}

function verificarSecuencia() {
  if (secuencia.length > secuenciaCorrecta.length) {
    secuencia = [];
  }

  for (let i = 0; i < secuencia.length; i++) {
    if (secuencia[i] !== secuenciaCorrecta[i]) {
      secuencia = [];
      break;
    }
  }

  if (secuencia.length === secuenciaCorrecta.length && secuencia.toString() === secuenciaCorrecta.toString()) {
    estado = 0;
    contador = 20;
    displayText = "Config";
    secuencia = [];
  }
}

```
