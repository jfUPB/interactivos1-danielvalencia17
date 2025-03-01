#### Solucion de la actividad

Implemente el mismo codigo que utlize en la actividad referida cambiando las variables y el mismo codigo de la bomba de la actividad anterior

##### codigo de P5.js (index)
```js
    <script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>
```

##### codigo de P5.js
```js
let port;
let connectBtn;
let aBtn, bBtn, sBtn, tBtn;

function setup() {
    createCanvas(400, 400);
    background(220);

    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    aBtn = createButton('A');
    aBtn.position(80, 350);
    aBtn.mousePressed(() => sendButtonClick('A'));

    bBtn = createButton('B');
    bBtn.position(160, 350);
    bBtn.mousePressed(() => sendButtonClick('B'));

    sBtn = createButton('S');
    sBtn.position(240, 350);
    sBtn.mousePressed(() => sendButtonClick('S'));

    tBtn = createButton('T');
    tBtn.position(320, 350);
    tBtn.mousePressed(() => sendButtonClick('T'));
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
    if (port.opened()) {
        port.write(letter + '\n');
        console.log("Mensaje enviado:", letter);
    } else {
        console.log("Error: el puerto serial no está abierto.");
    }
}
```
