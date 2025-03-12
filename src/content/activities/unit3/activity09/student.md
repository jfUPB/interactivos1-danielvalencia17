#### Solucion a la actividad

![pruebas de regresion](https://github.com/user-attachments/assets/86b3bc4d-45b0-4867-a62d-af128efbe74f)

##### Primera prueba
Error encontrado: Al llegar a EXPLOSIÓN, se reiniciaba automáticamente sin necesidad de presionar reset, Corrección: Se modificó la lógica para que solo el botón reset (logo del Micro:bit) permita salir de EXPLOSIÓN.

##### Segunda prueba
Error encontrado: La secuencia de desactivación no funcionaba correctamente cuando se enviaban eventos desde p5.js, Corrección: Se revisó la secuencia de entrada para asegurar que los eventos de A, B, A, Shake se registraran en orden antes de resetear la bomba.

##### Tercera prueba
Error encontrado: El contador de la bomba en estado ARMADO bajaba de forma irregular en p5.js,Corrección: Se ajustó el temporizador para que al bajar el contador sea más fluido
