#### Solucion a la actividad

##### ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?
Es basicamente unas reglas que se estipulan entre dos dispositivios para establecer con una conexion, la cual se hace principalmente con datos seriales.

##### ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?
Si no se separa los datos con comas se envian uno junto al otro lo cual los hace muy dificil de diferenciar cuando miramos la consola para revisar los datos seriales
(969652TrueFalse969652TrueFalse)

##### ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
El (\n) o enter es la manera en que el progama detecta el final del envio de ese paquete de datos, es necesario para que los datos se envien por el puerto serial de manera correcta si no se coloca podria generar un sobrecupo del puerto serial o no enviar los datos de manera correcta a la interaccion o progama.

##### ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?

##### ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?

##### ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?

##### ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
Ya que eesta se almacena con un entorno del propio P5js asi que los datos puede que siempre esten ahi pero hay que preguntar si realmente estan (el ejemplo de portero del edificio)
```js
if (port.availableBytes() > 0)
```
##### ¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?

##### Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías?

##### Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?

##### Si el micro:bit tiene los siguientes datos xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial?
si es mirandolo desde el puerto serial seria 
```js
123Value, 796Value, FalseState,TrueState
```
si se mira desde el punto de vista de que hace cada dato serian, posicion en eje X y Y, el boton A no esta presionado y el Boton B esta presionado.

##### ¿Qué aprendiste nuevo del micro:bit que no sabías antes?
Obviamente sabia acerca de la interaccion con los sensores y botones con P5.js, pero nunca pense que podria generar este tipo de interaccion usando el giroscopio del microbit, creo que abre muchas posibilidades a la hora de crear experiencias.
```js
 if (microBitAState === true) {
        let x = microBitX;
        let y = microBitY;

        if (keyIsPressed && keyCode === SHIFT) {
          if (abs(clickPosX - x) > abs(clickPosY - y)) {
            y = clickPosY;
          } else {
            x = clickPosX;
          }
        }
```
##### ¿Qué aprendiste nuevo de p5.js que no sabías antes?
La integracion de diferentes funcionalidades en un progama creando distintos bloques de codigo, ejemplo en el codigo incial que puedes cambiar colores y formas con presionar las teclas 1,2,3,4,5 esto hace el progama mucho mas dinamico y nos complicado de integrar

```js
  // default colors from 1 to 4
  if (key === "1") c = color(181, 157, 0);
  if (key === "2") c = color(0, 130, 164);
  if (key === "3") c = color(87, 35, 129);
  if (key === "4") c = color(197, 0, 123);

  // load svg for line module
  if (key === "5") lineModuleIndex = 0;
  if (key === "6") lineModuleIndex = 1;
  if (key === "7") lineModuleIndex = 2;
  if (key === "8") lineModuleIndex = 3;
  if (key === "9") lineModuleIndex = 4;
}
```
