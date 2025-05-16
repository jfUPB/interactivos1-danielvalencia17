#### Solucion a la actividad

Para esta actividad utilize tres botones para mostrar diferentes textos para variar, ya que he hecho varias veces las imagenes, para esto, utilize el mismo codigo base que en las imagenes solo que este caso se usa la variable "display.scroll('Hola mundo')" simplemente remplaze esto con los tres textos de ejemplo (dormir, comer, moto) y funciono bien.

##### Codigo Micro.bit
```js
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)
display.show(Image.HOUSE)
display.show(Image.GHOST)
display.show(Image.SWORD)

while True:

        data = uart.read(1)
        if data:
            if data[0] == ord('H'):
                display.scroll('Dormir')
                sleep(500)


            if data[0] == ord('O'):
                display.scroll('Comer')
                sleep(500)

            if data[0] == ord('L'):
                display.scroll('Moto')
                sleep(500)
```
##### Codigo de P5.js
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

    hBtn = createButton('1');
    hBtn.position(80, 350);
    hBtn.mousePressed(() => sendButtonClick('H'));

    oBtn = createButton('2');
    oBtn.position(160, 350);
    oBtn.mousePressed(() => sendButtonClick('O'));

    lBtn = createButton('3');
    lBtn.position(240, 350);
    lBtn.mousePressed(() => sendButtonClick('L'));


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
