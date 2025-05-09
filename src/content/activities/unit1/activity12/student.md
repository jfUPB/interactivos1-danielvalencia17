#### Solucion a la actividad

En este ejercicio debi cambiar ambos codigos para lograr el objetivo, use los codigos base en la parte final tenian la variable con el boton send love:

##### CODIGO MICROBIT

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
                display.show(Image.HOUSE)
                sleep(500)
                

            if data[0] == ord('O'):
                display.show(Image.GHOST)
                sleep(500)
                
            if data[0] == ord('L'):
                display.show(Image.SWORD)
                sleep(500)
            
            if data[0] == ord('A'):
                display.show(Image.HEART)
                sleep(500)
```
Use la parte final del codigo y la duplique por 4 cambiando la orden por cada una de las letras que coloque en el p5js y cambiando el display por alguna de las variables de imagen que coloque en la parte de arriba.

##### CODIGO P5JS

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

    hBtn = createButton('H');
    hBtn.position(80, 350);
    hBtn.mousePressed(() => sendButtonClick('H'));

    oBtn = createButton('O');
    oBtn.position(160, 350);
    oBtn.mousePressed(() => sendButtonClick('O'));

    lBtn = createButton('L');
    lBtn.position(240, 350);
    lBtn.mousePressed(() => sendButtonClick('L'));

    aBtn = createButton('A');
    aBtn.position(320, 350);
    aBtn.mousePressed(() => sendButtonClick('A'));
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
Aca utlize la misma variable para crear un boton como el de send love que al presionar genera la señal que envia al microbit y activa la imagen.
