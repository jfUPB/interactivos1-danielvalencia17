#### Solucion a la actividad

``` js
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


      let r = map(sin((x + t) * 0.01), -1, 1, 100, 200); 
      let g = map(cos((y + t) * 0.01), -1, 1, 0, 50);    
      let b = map(sin((x + y) * 0.01), -1, 1, 150, 255); 

      
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
![image](https://github.com/user-attachments/assets/a064a412-167e-4542-b476-be6b530e8592)

##### Explicacion
Este codigo genera una serie de cirulos en posiciones aletorias tanto en X como en Y cada que presionamos click, funciona como el sistema de color RGB (0 a 255) asi que el fondo esta configurado en un fondo oscuro y las figuras tienen valores mas altos en los canales Rojo y azul para generar esos difuminados en colores frios, las fguras se generar a partir de un elipse y tienen la variable fill baja para que se noten algo trasparentes.

