#### Solucion a la actividad

En esta actividad use ambos codigos base proporcionados, utilize el mismo codigo en mcirobit y cambien el codigo en p5.js:

```js
let port;
let connectBtn;
let squareX;
let squareY;
let squareSize = 100;

function setup() {
    createCanvas(400, 400);
    background(220);
    squareX = width / 2 - squareSize / 2;
    squareY = height / 2 - squareSize / 2;
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
}

function draw() {
    if (port.availableBytes() > 0) {
        let dataRx = port.read(1);
        
        if (dataRx == 'A') {
            fill(random(255), random(255), random(255));
        }

        background(220);
        rect(squareX, squareY, squareSize, squareSize);
    }

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
```

Cambie la forma de (elipse) a (square), quite el boton de send love, quite las letras dentro del boton y agregue que con el boton A el cuadrado se rellenara de un color aleatorio.
