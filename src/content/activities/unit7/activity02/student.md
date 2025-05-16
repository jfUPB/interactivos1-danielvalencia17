#### Solucion a la actividad

##### Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?
devtunnels funciono como un intermediario entre servidores y es necesario para poder mandar la informacion desde otro dispositivo externo al servidor de node.js

##### ¿Por qué usamos JSON.stringify() en el emisor (móvil) y JSON.parse() en el receptor (escritorio)? ¿Qué problema resuelve JSON aquí?
porque necesitamos convertir la cadena de datos a un paquete que pueda leer el receptor de manera facil, json simplifica al ser un lenguaje establecido de emsion de datos.

##### Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.
la funcion touchmode sirve para leer el movimiento en la pantalla tactil del celular el treshold ignora pequeños movimientos para evitar sobrecargar el canal con pqueños datos inecesarios.

##### ¿Qué otros eventos táctiles existen en p5.js y para qué tipo de interacciones podrían ser útiles (ej. un botón virtual, detectar un tap)?
podriamos crear botones que cambien cosas en el servidor loca, como que cambie el color del fondo dependiendo que a boton le demos, o quizas alguna ointegracion con camara.

##### Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?
usando solo la ip local practicamente desaparece la latencia y se siente una respuesta muy rapida, la ventaja del devtunnels es que me deja ingresar desde otros dispositivos lo cual abre las posibilidades de interaccion
