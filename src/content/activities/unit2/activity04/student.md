#### Solucion a la actividad

Inicalmente pense en que debia cambiar el codigo base en el microbit para asginar la accion (uart.write:) a el sensor del microbit y simplemente crear un codigo sencillo de cambio de color en p5js, cuando lo intente, el codigo en microbit fue muy facil ya que la web trae ejemplos de cada sensor, simplemte cambie la accion de enviar a los leds por la de uart:A, y en p5js cree el codigo base usando el ejemplo de la unidad y la conexion funciono como esperaba.

```js
let port;
let connectBtn;

let colorIndex = 0;
let colors = ['blue', 'purple', 'pink'];

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    
    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
}

function draw() {

    if (port.availableBytes() > 0) {
        let dataRx = port.read(1);
        
        if (dataRx == 'A') {
            colorIndex = (colorIndex + 1) % colors.length;
            background(220);
            fill(colors[colorIndex]);
            ellipse(width / 2, height / 2, 100, 100);
        }
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
en las conclusiones creo que comprendo bien el como se conecta las señales del microbit con la generacion de p5js.
