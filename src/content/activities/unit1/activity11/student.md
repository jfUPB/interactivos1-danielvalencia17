#### Solucion a la actividad

Para solucionar esta actividad utlize ambos codigos base que se habia proporcionado incialmente, el codigo en microbit editor lo deje igual con el mapeo de los botones y cambie el codigo en p5.js en lo siguiente:

```js
let port;
let connectBtn;
let circleX;
let circleY;
let circleSize = 100;

function setup() {
    createCanvas(400, 400);
    background(220);
    
    circleX = width / 2;
    circleY = height / 2;
    
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
}

function draw() {
    if (port.availableBytes() > 0) {
        let dataRx = port.read(1);
        
        if (dataRx == 'A') {
            circleX -= 10;
        } else if (dataRx == 'B') {
            circleX += 10;
        }

        circleX = constrain(circleX, circleSize / 2, width - circleSize / 2);
        
        background(220);
        fill(128, 0, 128);
        ellipse(circleX, circleY, circleSize, circleSize);
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

Quite el boton de send love, cambie el color del circulo y mapie los botones a y b para que al presionarlos en cirulos se mueva -+10 puntos en el X.
