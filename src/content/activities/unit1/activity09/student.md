#### Solucion a la actividad

``` ej
let t = 0; 

function setup() {
  createCanvas(1000, 1000); 
  noLoop(); 
  noStroke(); 
}

function draw() {
  background(10);
  
  let spacing = 20; 
  
  for (let x = 0; x < width; x += spacing) {
    for (let y = 0; y < height; y += spacing) {
      let offsetX = sin((x + t) * 0.05) * 20; 
      let offsetY = cos((y + t) * 0.05) * 20; 


      let r = map(sin((x + t) * 0.01), -1, 1, 100, 200); // Limitar el rojo (suave)
      let g = map(cos((y + t) * 0.01), -1, 1, 0, 50);    // Mantener el verde bajo
      let b = map(sin((x + y) * 0.01), -1, 1, 150, 255); // Aumentar el azul

      
      fill(r, g, b, 100); 
      ellipse(x + offsetX, y + offsetY, spacing * 0.8); 
    }
  }

  t += 1; 
}


function mousePressed() {
  t = random(1000); 
  redraw(); 
}
```
