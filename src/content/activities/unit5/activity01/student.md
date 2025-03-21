#### Solucion a la actividad

##### Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?
el microbit esta enviando los datos atraves del este formato
```
    data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
```
y se conecta con el P5.js que conecta esta linea de codigo
```js
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
```

##### ¿Cómo es la estructura del protocolo ASCII usado?
```js
39 36 39 2C 36 35 32 2C 54 72 75 65 2C 46 61 6C 73 65 0A
```
cada numero se representa con un 3 antes es decir: 39 36 39 --- 969, y el 2C y 0A representas las comas y el punto final.

##### Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.
el lee cual es la zona 
```js

       y)) {
            y = clickPosY;if (microBitAState === true) {
        let x = microBitX;
        let y = microBitY;

        if (keyIsPressed && keyCode === SHIFT) {
          if (abs(clickPosX - x) > abs(clickPosY -
          } else {
            x = clickPosX;
          }
        }
```
##### ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?

##### Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.

