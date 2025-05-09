#### Solucion a la actividad

##### Explica los cambios clave que realizaste en mobile/sketch.js: ¿Qué datos envías ahora y cómo/cuándo los envías? Pega fragmentos de código relevantes.
```js
function touchMoved() {
    if (socket && socket.connected) { 
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold || lastTouchX === null) {
            let touchData = {
                type: 'touch',
                x: mouseX,
                y: mouseY
            };
            socket.emit('message', JSON.stringify(touchData));

            lastTouchX = mouseX;
            lastTouchY = mouseY;
        }
    }
    return false;
}
```
Esta parte del codigo es la que envia al escritorio la posicion de generacion de las particulas, deje el canvas del el tamaño original y conviertiendo el envio de los paquetes en .json.

##### Explica los cambios clave que realizaste en desktop/sketch.js: ¿Cómo recibes e interpretas los datos? ¿Qué modificaste en setup() o draw() para lograr el nuevo efecto? Pega fragmentos de código relevantes.
```js
 socket = io();

  socket.on('connect', () => {
    console.log('Connected to server');
  });

  socket.on('message', (data) => {
    console.log(`Received message: ${data}`);
    try {
      let parsedData = JSON.parse(data);
      if (parsedData && parsedData.type === 'touch') {
        circleX = parsedData.x;
        circleY = parsedData.y;

        // Si querés crear una partícula desde datos remotos también:
        particles.push(new Particle(parsedData.x, parsedData.y));
      }
    } catch (e) {
      console.error("Error parsing received JSON:", e);
    }
  });

  socket.on('disconnect', () => {
    console.log('Disconnected from server');
  });

  socket.on('connect_error', (error) => {
    console.error('Socket.IO error:', error);
  });
}
```
esta parte es la que recibe los datos en el deskopt, interpreta el paquete .json y lo pasa a los datos de posicion, para que draw genere las particulas.

```js
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.lifespan = 255;
    this.size = random(5, 13);
    this.noiseOffset = random(1000);
  }

  update() {
    let angle = noise(this.pos.x * 0.005, this.pos.y * 0.005, this.noiseOffset) * TWO_PI * 2;
    let force = p5.Vector.fromAngle(angle);
    force.mult(0.5);
    this.vel.add(force);
    this.vel.limit(4);
    this.pos.add(this.vel);
    this.lifespan -= 3;
  }

  display() {
    fill(29, 235, 232, this.lifespan);
    ellipse(this.pos.x, this.pos.y, this.size);
```
en la zona inicial de draw deje esa manera de recibir la posicion igual en general, ene sta parte cambie el tamaño de la particula, el color, velocidad y tamaño, ademas cambie el tamaño de canvas para que sea del mismo tamaño que el generador del mobile.

#### Server
```js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

app.use(express.static('public'));

io.on('connection', (socket) => {
    console.log('New client connected');
    socket.on('message', (message) => {
        console.log(`Received message => ${message}`);
        socket.broadcast.emit('message', message);
    });

    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```
#### Server Deskopt
```js
let particles = [];
let socket;
let circleX = 200;
let circleY = 200;

function setup() {
  createCanvas(300, 400);
  background(0, 20);

  // Inicializar socket
  socket = io();

  socket.on('connect', () => {
    console.log('Connected to server');
  });

  socket.on('message', (data) => {
    console.log(`Received message: ${data}`);
    try {
      let parsedData = JSON.parse(data);
      if (parsedData && parsedData.type === 'touch') {
        circleX = parsedData.x;
        circleY = parsedData.y;

        // Si querés crear una partícula desde datos remotos también:
        particles.push(new Particle(parsedData.x, parsedData.y));
      }
    } catch (e) {
      console.error("Error parsing received JSON:", e);
    }
  });

  socket.on('disconnect', () => {
    console.log('Disconnected from server');
  });

  socket.on('connect_error', (error) => {
    console.error('Socket.IO error:', error);
  });
}

function draw() {
  background(0, 20);

  // Dibuja partículas si hay clic local
  if (mouseIsPressed) {
    particles.push(new Particle(mouseX, mouseY));

    // Enviar datos al servidor
    let data = JSON.stringify({ type: 'touch', x: mouseX, y: mouseY });
    socket.emit('message', data);
  }

  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].display();
    if (particles[i].isDead()) {
      particles.splice(i, 1);
    }
  }


}

class Particle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.lifespan = 255;
    this.size = random(5, 13);
    this.noiseOffset = random(1000);
  }

  update() {
    let angle = noise(this.pos.x * 0.005, this.pos.y * 0.005, this.noiseOffset) * TWO_PI * 2;
    let force = p5.Vector.fromAngle(angle);
    force.mult(0.5);
    this.vel.add(force);
    this.vel.limit(4);
    this.pos.add(this.vel);
    this.lifespan -= 3;
  }

  display() {
    fill(29, 235, 232, this.lifespan);
    ellipse(this.pos.x, this.pos.y, this.size);
  }

  isDead() {
    return this.lifespan < 0;
  }
}

function keyPressed() {
  console.log(`particle size: ${particles.length}`);
}
```
#### Server Mobile
```js
let socket;
let lastTouchX = null; 
let lastTouchY = null; 
const threshold = 5;

function setup() {
    createCanvas(300, 400);
    background(220);

    // Conectar al servidor de Socket.IO
    //let socketUrl = 'http://localhost:3000';
    socket = io();

    socket.on('connect', () => {
        console.log('Connected to server');
    });

    socket.on('message', (data) => {
        console.log(`Received message: ${data}`);
    });

    socket.on('disconnect', () => {
        console.log('Disconnected from server');
    });

    socket.on('connect_error', (error) => {
        console.error('Socket.IO error:', error);
    });
}

function draw() {
    background(220);
    fill(0, 0, 0);
    textAlign(CENTER, CENTER);
    textSize(20);
    text('Toca para generar las particulas', width / 2, height / 2);
}

function touchMoved() {
    if (socket && socket.connected) { 
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold || lastTouchX === null) {
            let touchData = {
                type: 'touch',
                x: mouseX,
                y: mouseY
            };
            socket.emit('message', JSON.stringify(touchData));

            lastTouchX = mouseX;
            lastTouchY = mouseY;
        }
    }
    return false;
}
```
#### Video
https://imagekit.io/tools/asset-public-link?detail=%7B%22name%22%3A%22WhatsApp%20Video%202025-05-09%20at%204.55.14%20PM.mp4%22%2C%22type%22%3A%22video%2Fmp4%22%2C%22signedurl_expire%22%3A%222028-05-08T21%3A57%3A37.561Z%22%2C%22signedUrl%22%3A%22https%3A%2F%2Fmedia-hosting.imagekit.io%2Fba6257f908ee4900%2FWhatsApp%2520Video%25202025-05-09%2520at%25204.55.14%2520PM.mp4%3FExpires%3D1841435858%26Key-Pair-Id%3DK2ZIVPTIP2VGHC%26Signature%3DdUgAKOcDMXjmbxas~jQhhh87SZxe1KFfz9Y3LWzlTu6JQ1g~FzSZoP8OSl80qJklhvMGJP1AWXzLfB92g4FXAYrYHIfuaPiKRMkETRuGbJM-TeunJtwk3W~XEZSlG3~axhhVz-eXhJ7aIZVl9WqkabAiirv8UPHOLrqeoIBRwzz87Oq9EkB-4AaeB6~GX~7MpBCcECq2Hks5ZHeA-JY9r9Lt-9PcO1MoPmtnF~sMnwUh2NQmJ6xzZzaD9WuJInyLo8rRyoM2SqvAl0EAlqlk-B77PgnWhPpiWgWjYC9Bv63MqXlRSIjspFLTUxFS6tdg4wT9cBpptPY-OHofKluFPw__%22%7D
