#### solucion a la actividad

quiero crear una interaccion de tipo magnetica, que la page 1 sea una especie de agujero negro que atraiga a un sistema de particulas en page 2, para esto debo simular la fuerza de atraccion como una variable matematica en el p5, debo cambiar la parte visual en la parte del draw de ambas paginas para que genere esta sensancion y donde estan las variables matematicas que generar esta interaccion de la linea debo colocar variables que generen que un punto tenga esa fuerza de atraccion con la page 2, haciendolo lo primero que logre es que una esfera se atrajiera hacia el centro de page 1 pero se salia del canvas y no podia volver a intervenir con ella, coloque bordes para que que no se saliera y funciono, luego cambie los .hmtl y les di la forma de aguejero ademas cree el sistema de particulas pero no se estaba enviando los datos de manera correcta, lo que pasa es que estaba leyendo unos datos erroneos ya que el server.js tenia otro nombre para ese tipo de datos, funciono, pero tenia un poblema en las coordenadas ya que estaba leyendo el centro en el borde de la pagina se cambio calculando el canvas completo de la pantalla y ya funciono, ademas logramos cambiar el punto muerto de las particulas donde se desaparecen cambiando su punto muerto con las nuevas coordenadas que habiamos calculado.

Page 1
```js
let socket = io('http://localhost:3000');

// Datos de la ventana de page 1
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

socket.on('connect', () => {
    console.log(socket.id);
    // Enviar datos de la ventana de page 1
    socket.emit('win1update', currentPageData, socket.id);
});

let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
}

function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    // Verificar si hubo un cambio de posición o tamaño
    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {
        
        // Enviar la nueva posición y tamaño de la ventana a todos los clientes
        socket.emit('win1update', currentPageData, socket.id);
        previousPageData = currentPageData;
        //console.log("send pos");
    }
}

function draw() {
    background(0);

    // Dibujo del agujero negro
    stroke(255, 140, 0);  // Borde naranja brillante
    strokeWeight(5);
    fill(0);  // Color negro para el agujero
    ellipse(width / 2, height / 2, 200, 200);  // Agujero negro en el centro de la pantalla

    checkWindowPosition();
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```
page 2
```js
let socket = io('http://localhost:3000');

let remotePageData = { x: 100, y: 100, width: 100, height: 100 };  // Agujero negro en page 1
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

socket.on('connect', () => {
    socket.emit('win2update', currentPageData, socket.id);
});

socket.on('updatePage1', (dataWindow) => {
    remotePageData = dataWindow;  // Actualizar la posición del agujero negro
    //console.log(`x: ${remotePageData.x},y: ${remotePageData.y} `);
});

let particles = [];

function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
}

function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {
        socket.emit('updatePage2', currentPageData, socket.id);
        previousPageData = currentPageData;
    }
}

function draw() {
    background(10);

    // Generar nuevas partículas constantemente
    particles.push(new Particle(width / 2, height / 2));  // Partículas empiezan desde el centro de la pantalla

    for (let i = particles.length - 1; i >= 0; i--) {
        let p = particles[i];
        p.attractToHole();  // Atraer la partícula hacia el agujero negro
        p.update();
        p.display();

        if (p.isAttracted()) {
            particles.splice(i, 1);  // Eliminar la partícula cuando esté cerca del agujero negro
        }
    }

    checkWindowPosition();
}

// Partícula
class Particle {
    constructor(x, y) {
        this.pos = createVector(x, y);
        this.vel = p5.Vector.random2D().mult(random(0.5, 1.5));  // Velocidad aleatoria inicial
        this.acc = createVector(0, 0);
        this.stuck = false;
        this.color = color(random(50, 100), random(100, 200), 255);  // Color azul
        this.maxSpeed = 3;
        this.size = 6;  // Tamaño de la partícula
    }

    attractToHole() {
        // Atrae la partícula hacia el agujero negro
        let holeX = remotePageData.x + remotePageData.width / 2;
        let holeY = remotePageData.y + remotePageData.height / 2;

        let particleX = this.pos.x+currentPageData.x;
        let particleY = this.pos.y+currentPageData.y;
        

        let force = createVector(holeX - particleX, holeY - particleY);
        let distance = force.mag();
        //console.log(distance);

        // Si está demasiado cerca, desaparece
        if (distance < 20) {
            this.stuck = true;
        }

        // Normalizar y aplicar fuerza
        force.normalize();
        force.mult(0.5);  // Fuerza de atracción

        this.acc.add(force);
    }

    update() {
        if (this.stuck) return;

        this.vel.add(this.acc);
        this.vel.limit(this.maxSpeed);  // Limitar velocidad para suavizar movimiento
        this.pos.add(this.vel);
        this.acc.mult(0);  // Resetear aceleración
    }

    display() {
        noStroke();
        fill(this.color);
        ellipse(this.pos.x, this.pos.y, this.size, this.size);  // Dibujar partícula
    }

    isAttracted() {
        // Comprobar si la partícula está suficientemente cerca del agujero negro
        let holeX = remotePageData.x + remotePageData.width / 2;
        let holeY = remotePageData.y + remotePageData.height / 2;
        let particleX = this.pos.x+currentPageData.x;
        let particleY = this.pos.y+currentPageData.y;

        let distance = dist(particleX, particleY, holeX, holeY);

        return distance < 20;  // Ajustar el umbral según el tamaño del agujero negro
    }
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```
Server
```js
// server.js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');

const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;

app.use(express.static(path.join(__dirname, 'views')));

app.get('/page1', (req, res) => {
  res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});

app.get('/page2', (req, res) => {
  res.sendFile(path.join(__dirname, 'views', 'page2.html'));
});

let page1 = {}; // agujero negro
let page2 = {}; // afectado

io.on('connection', (socket) => {
  console.log('New client connected:', socket.id);

  socket.on('win1update', (data, id) => {
    page1 = data;
    socket.broadcast.emit('updatePage1', page1);
  });

  socket.on('win2update', (data, id) => {
    page2 = data;
    socket.broadcast.emit('updatePage2', page2);
  });

  socket.on('disconnect', () => {
    console.log('Client disconnected:', socket.id);
  });
});

server.listen(port, () => {
  console.log('Servidor corriendo en http://localhost:' + port);
});
```
