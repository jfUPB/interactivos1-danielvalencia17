#### Solucion a la actividad

https://editor.p5js.org/danielvalencia17/sketches/Kikt46l87

Codigo de P5 en binario
```js
/******************
Code by Vamoss
Original code link:
https://www.openprocessing.org/sketch/751983

Author links:
http://vamoss.com.br
http://twitter.com/vamoss
http://github.com/vamoss
******************/

//Inspired by Felix Auer
//http://www.felixauer.com/javascript/difeqrk.html

// Modificación para cambiar la interfaz humano máquina con micro:bit

//***************************************
// CODE APP DANI
let blobs = [];
let colors;
let variation = 0;
let xScale, yScale, centerX, centerY;
//auto change
let changeDuration = 3000;
let lastChange = 0;
//***************************************

let port;
let connectBtn;
let microBitConnected = false;
let serialBuffer = []; // Buffer para almacenar bytes recibidos

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAITMICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};

let appState = STATES.WAIT_MICROBIT_CONNECTION;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

function setup() {
  createCanvas(windowWidth, windowHeight);

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);

  //***********************************
  // CODE APP DANI

  textAlign(CENTER, CENTER);

  xScale = width / 20;
  yScale = (height / 20) * (width / height);

  centerX = width / 2;
  centerY = height / 2;

  colors = [
    color("#FF00B3"),
    color("#BB0048"),
    color("#910029"),
    color("#500E00"),
    color("#FFCC32"),
  ];

  //*****************
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}

function updateButtonStates(newAState, newBState) {
  // Generar eventos de keypressed
  if (newAState === true && prevmicroBitAState === false) {
    print("A pressed");
  }
  // Generar eventos de key released
  if (newBState === false && prevmicroBitBState === true) {
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}


function readSerialData() {
  // Acumula los bytes recibidos en el buffer
  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }

  // Procesa el buffer mientras tenga al menos 8 bytes (tamaño de un paquete)
  while (serialBuffer.length >= 8) {
    // Busca el header (0xAA)
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift(); // Descarta bytes hasta encontrar el header
      continue;
    }

    // Si hay menos de 8 bytes, espera a que llegue el paquete completo
    if (serialBuffer.length < 8) break;

    // Extrae los 8 bytes del paquete
    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8); // Elimina el paquete procesado del buffer

    // Separa datos y checksum
    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];
    // Calcula el checksum sumando los datos y aplicando módulo 256
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error in packet");
      continue; // Descarta el paquete si el checksum no es válido
    }

    // Si el paquete es válido, extrae los valores
    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0) + windowWidth / 2;
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);

  }
}


function draw() {
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");
  }

  switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
      // No puede comenzar a dibujar hasta que no se conecte el microbit
      // evento 1:
      if (microBitConnected === true) {
        // Preparo todo para el estado en el próximo frame
        print("Microbit ready to draw");
        strokeWeight(0.75);
        c = color(181, 157, 0);
        noCursor();
        port.clear();
        prevmicroBitAState = false;
        prevmicroBitBState = false;        
        appState = STATES.RUNNING;
      }

      break;

    case STATES.RUNNING:
      // EVENTO: estado de conexión del microbit
      if (microBitConnected === false) {
        print("Waiting microbit connection");
        cursor();
        appState = STATES.WAIT_MICROBIT_CONNECTION;
        break;
      }

      readSerialData();
      //***************************
      // CODE APP DANI
      appCode();
      //***************************

      break;
  }
}

//******************************************************************
// CODE APP DANI

function appCode() {
  //EVENTO: recepción de datos seriales del micro:bit

  if (microBitAState === true) {
    //let x = microBitX;
    //let y = microBitY;

    for (let i = 0; i < 20; i++) {
      let x = microBitX + random(-100, 100);
      let y = microBitY + random(-100, 100);
      var blob = {
        x: getXPos(x),
        y: getYPos(y),
        size: random(1, 8),
        lastX: x,
        lastY: y,
        color: colors[floor(random(colors.length))],
        direction: random(0.7, 1) * (random() > 0.5 ? 1 : -1),
      };
      blobs.push(blob);
    }
  }

  var length = blobs.length;
  if (length == 0) {
    background("#000000");
    noStroke();
    fill(255);
    textSize(40);
    text("Presiona para emitir particulas", centerX, centerY);
    return;
  }

  noStroke();
  fill(26, 6, 70, 10);
  rect(0, 0, width, height);

  //auto change
  let time = millis();
  if (time - lastChange > changeDuration) {
    lastChange = time;
    variation++;
    if (variation > 11) variation = 0;
  }

  var stepsize = deltaTime * 0.002;
  for (var i = length - 1; i >= 0; i--) {
    let blob = blobs[i];

    var x = getSlopeX(blob.x, blob.y);
    var y = getSlopeY(blob.x, blob.y);
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
    if (
      x < -border ||
      y < -border ||
      x > width + border ||
      y > height + border
    ) {
      blobs.splice(i, 1);
    }
  }
}

function getSlopeY(x, y) {
  switch (variation) {
    case 0:
      return Math.sin(x);
    case 1:
      return Math.sin(x * 5) * y * 0.3;
    case 2:
      return Math.cos(x * y);
    case 3:
      return Math.sin(x) * Math.cos(y);
    case 4:
      return Math.cos(x) * y * y;
    case 5:
      return Math.log(Math.abs(x)) * Math.log(Math.abs(y));
    case 6:
      return Math.tan(x) * Math.cos(y);
    case 7:
      return -Math.sin(x * 0.1) * 3; //orbit
    case 8:
      return (x - x * x * x) * 0.01; //two orbits
    case 9:
      return -Math.sin(x);
    case 10:
      return -y - Math.sin(1.5 * x) + 0.7;
    case 11:
      return Math.sin(x) * Math.cos(y);
  }
}

function getSlopeX(x, y) {
  switch (variation) {
    case 0:
      return Math.cos(y);
    case 1:
      return Math.cos(y * 5) * x * 0.3;
    case 2:
    case 3:
    case 4:
    case 5:
    case 6:
      return 1;
    case 7:
      return Math.sin(y * 0.1) * 3; //orbit
    case 8:
      return y / 3; //two orbits
    case 9:
      return -y;
    case 10:
      return -1.5 * y;
    case 11:
      return Math.sin(y) * Math.cos(x);
  }
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

//******************************************************************
```
https://editor.p5js.org/danielvalencia17/sketches/BNO5W2yXp

![image](https://github.com/user-attachments/assets/c233e484-3774-4d4c-89ae-a8a0e9f5d2fb)

![image](https://github.com/user-attachments/assets/6d0accd8-8cb9-460d-9a07-75db868b390d)

