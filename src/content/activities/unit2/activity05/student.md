#### Solucion a la actividad

En este proceso experimente con el el codigo ya utlizado en la actividad 12 de la unidad uno, usando lo mismo que expuse en aquella actividad.

##### Codigo Micro.bit
```js
from microbit import *

uart.init(baudrate=115200)
display.show(Image.HOUSE)


while True:

        data = uart.read(1)
        if data:
            if data[0] == ord('H'):
                display.show(Image.HOUSE)
                sleep(500)
```
##### Codigo P5.js
```js
let port;
let connectBtn;
let hBtn, oBtn, lBtn, aBtn;

function setup() {
    createCanvas(400, 400);
    background(220);

    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    hBtn = createButton('Enviar');
    hBtn.position(80, 350);
    hBtn.mousePressed(() => sendButtonClick('H'));

}

function draw() {
    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendButtonClick(letter) {
    port.write(letter);
}
```
