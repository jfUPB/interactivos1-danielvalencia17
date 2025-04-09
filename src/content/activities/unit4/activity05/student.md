#### solucion a la actividad

##### Codigo Original
https://editor.p5js.org/danielvalencia17/sketches/Kikt46l87

##### Codigo Modificado
```js
var blobs = [];
var colors;
let variation = 0;
let xScale, yScale, centerX, centerY;
let port;
let connectBtn;
let microBitConnected = false;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let prevmicroBitAState = false;

function setup() {
    createCanvas(windowWidth, windowHeight);
    textAlign(CENTER, CENTER);
    
    xScale = width / 20;
    yScale = height / 20 * (width / height);
    
    centerX = width / 2;
    centerY = height / 2;
    
    colors = [color("#581845"), color("#900C3F"), color("#C70039"), color("#FF5733"), color("#FFC30F")];
    
    port = createSerial();
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(0, 0);
    connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open("MicroPython", 115200);
    } else {
        port.close();
    }
}

function draw() {
    if (!port.opened()) {
        connectBtn.html("Connect to micro:bit");
        microBitConnected = false;
    } else {
        microBitConnected = true;
        connectBtn.html("Disconnect");
        if (port.availableBytes() > 0) {
            let data = port.readUntil("\n");
            if (data) {
                data = data.trim();
                let values = data.split(",");
                if (values.length == 4) {
                    microBitX = int(values[0]) + windowWidth / 2;
                    microBitY = int(values[1]) + windowHeight / 2;
                    microBitAState = values[2].toLowerCase() === "true";
                    updateButtonStates(microBitAState);
                }
            }
        }
    }
    
    if (blobs.length === 0) {
        background("#1a0633");
        noStroke();
        fill(255);
        textSize(40);
        text("Press A to emit particles", centerX, centerY);
        return;
    }
    
    noStroke();
    fill(26, 6, 51, 10);
    rect(0, 0, width, height);
    
    let stepsize = deltaTime * 0.002;
    for (let i = blobs.length - 1; i >= 0; i--) {
        let blob = blobs[i];

        let x = getSlopeX(blob.x, blob.y);
        let y = getSlopeY(blob.x, blob.y);
        blob.x += blob.direction * x * stepsize;
        blob.y += blob.direction * y * stepsize;

        x = getXPrint(blob.x);
        y = getYPrint(blob.y);
        stroke(blob.color);
        strokeWeight(blob.size);
        line(x, y, blob.lastX, blob.lastY);
        blob.lastX = x;
        blob.lastY = y;

        const border = 200;
        if (x < -border || y < -border || x > width + border || y > height + border) {
            blobs.splice(i, 1);
        }
    }
}

function updateButtonStates(newAState) {
    if (newAState === true && prevmicroBitAState === false) {
        for (let i = 0; i < 20; i++) {
            let x = microBitX + random(-100, 100);
            let y = microBitY + random(-100, 100);
            let blob = {
                x: getXPos(x),
                y: getYPos(y),
                size: random(1, 5),
                lastX: x,
                lastY: y,
                color: colors[floor(random(colors.length))],
                direction: random(0.1, 1) * (random() > 0.5 ? 1 : -1)
            };
            blobs.push(blob);
        }
    }
    prevmicroBitAState = newAState;
}

function getSlopeY(x, y) {
    return Math.sin(x) * Math.cos(y);
}

function getSlopeX(x, y) {
    return Math.cos(y);
}

function getXPos(x) {
    return (x - centerX) / xScale;
}
function getYPos(y) {
    return (y - centerY) / yScale;
}

function getXPrint(x) {
    return xScale * x + centerX;
}
function getYPrint(y) {
    return yScale * y + centerY;
}
```
https://editor.p5js.org/danielvalencia17/sketches/Kikt46l87

![image](https://github.com/user-attachments/assets/618b1d9d-68bb-406e-8879-70fc319a12a0)
