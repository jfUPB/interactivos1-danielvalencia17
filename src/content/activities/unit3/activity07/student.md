#### Solucion a la actividad

##### Codigo de P5.js
```js
const CONFIGURACION = 0;
const ARMADO = 1;
const EXPLOSION = 2;

let estado = CONFIGURACION;
let contador = 20;
let ultimoTiempo = 0;
let secuenciaEsperada = ['A', 'B', 'A', 'Shake']; 
let secuenciaActual = []; 


let botonA, botonB, botonShake, botonReset;
let displayText = "";

function setup() {
  createCanvas(200, 210);
  

  botonA = createButton("Botón A");
  botonA.position(20, 150);
  botonA.mousePressed(botonAAccionado);

  botonB = createButton("Botón B");
  botonB.position(100, 150);
  botonB.mousePressed(botonBAccionado);


  botonShake = createButton("Shake");
  botonShake.position(20, 180);
  botonShake.mousePressed(gestoShake);


  botonReset = createButton("Reset");
  botonReset.position(100, 180);
  botonReset.mousePressed(resetear);


  textAlign(CENTER, CENTER);
  textSize(32);
  text("Config", width / 2, height / 2);
}

function draw() {
  background(220);

  if (estado === CONFIGURACION) {
    actualizarDisplay(contador);
  } else if (estado === ARMADO) {
    let tiempoActual = millis();
    if (tiempoActual - ultimoTiempo >= 1000) {
      ultimoTiempo = tiempoActual;
      if (contador > 0) {
        contador--;
        actualizarDisplay(contador);
      } else {
        estado = EXPLOSION;
        displayText = "BOOM!";
      }
    }

    if (secuenciaActual.length === secuenciaEsperada.length) {
      if (JSON.stringify(secuenciaActual) === JSON.stringify(secuenciaEsperada)) {
        estado = CONFIGURACION;
        contador = 20;
        secuenciaActual = []; // Resetear secuencia
        displayText = "Config";
      } else {

        secuenciaActual = [];
      }
    }
  } else if (estado === EXPLOSION) {
    // Mostrar "BOOM!" hasta que se presione el botón de reset
    background(255, 0, 0);
    text("BOOM!", width / 2, height / 2);
  }
}


function actualizarDisplay(tiempo) {
  displayText = tiempo;
  text(displayText, width / 2, height / 2);
}

function botonAAccionado() {
  if (estado === CONFIGURACION) {
    if (contador < 60) {
      contador++;
      actualizarDisplay(contador);
    }
  }


  if (estado === ARMADO) {
    secuenciaActual.push('A');
  }
}


function botonBAccionado() {
  if (estado === CONFIGURACION) {
    if (contador > 10) {
      contador--;
      actualizarDisplay(contador);
    }
  }


  if (estado === ARMADO) {
    secuenciaActual.push('B');
  }
}


function gestoShake() {
  if (estado === CONFIGURACION) {
    estado = ARMADO;
    displayText = "Armed";
    ultimoTiempo = millis();
  }
  if (estado === ARMADO) {
    secuenciaActual.push('Shake');
  }
}

// Función de reset
function resetear() {
  if (estado === EXPLOSION) {
    estado = CONFIGURACION;
    contador = 20;
    secuenciaActual = []; 
    displayText = "Config";
  }
}
```
