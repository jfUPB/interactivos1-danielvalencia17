#### Solucion a la actividad

##### ¿Por qué es útil enviar los datos como un objeto JSON ({type: ‘touch’, x: …, y: …}) en lugar de simplemente enviar, por ejemplo, una cadena como “mouseX,mouseY”?
ya que los archivos se deben convertitr a un formato universal y mas optimizado para lograr el mejor rendimiento a la hora de enviar los paquetes, como en el caso del codigo binario.

##### ¿Qué pasaría si quitaras la comprobación del threshold? ¿Cómo afectaría al rendimiento o la fluidez de la interacción?
podria saturar el canal y generar poblemas a la hora de enviar nuevos paquetes ya que se enviara paquetes de datos inecesarios quitando mucha optmizacion a la interaccion.

##### ¿Cómo adaptarías este código si quisieras que también respondiera al clic del ratón en un computador (para pruebas)? (Pista: p5.js tiene mouseMoved() y mousePressed()).
tendria que cambiar la parte de:

```js
function touchMoved() { // Función especial de p5.js para eventos táctiles
    if (socket && socket.connected) {
        // Calcula si el movimiento supera el umbral
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold || lastTouchX === null) { // Enviar si supera umbral o es el primer toque
            let touchData = {
                type: 'touch', // Tipo de mensaje (podríamos tener otros)
                x: mouseX,     // Coordenada X del toque (relativa al canvas móvil)
                y: mouseY      // Coordenada Y del toque
            };
```
Sustituyendola por lo que ya hemos usado en anteriores unidades con mouse.pressed cambiando el moviemiendo tactil por el mouse.

#### Escritorio

##### ¿Por qué es importante usar JSON.parse() dentro de un bloque try…catch?
Para verificar que el dato recibido si es un.JSON de lo contrario seria un dato invalido.

##### Si los canvas del móvil y del escritorio tuvieran tamaños diferentes (ej: móvil 300x300, escritorio 600x600), ¿cómo modificarías el código del escritorio para que la posición del círculo rojo refleje proporcionalmente la posición del toque en el móvil? (Pista: usa la función map() de p5.js).
La funcion map se utilizaria para mapear el rango de accion de la interacion con el movil, ya sea mapeando que solo lo detecte en el canvas del movil, o readaptando los datos para que se escale proporcionalmente en el escritorio, como duplicando los valores de posicion.

##### ¿Qué tendrías que cambiar en el código del escritorio si el servidor, en lugar de retransmitir el evento como ‘message’, lo enviara como ‘updateDesktop’?
habira que cambiar en socket.on el evento para que updatedeskopt remplaze a message.

#### Reporte final

##### Describe el propósito principal de mobile/sketch.js y desktop/sketch.js.
cada uno es el codigo fuente de la aplicacion mobil y de escritorio, estos son los que se encargan de mandar y reintrepetar los datos que se envian a travez de server.js.

##### Explica la función touchMoved en el móvil, incluyendo el uso del threshold y JSON.stringify.
La funcion touchmoved lee la posicion en la que se toco en el canvas y envia esa posicion a la aplicacion de escritorio, el treshold elminina datos muy pqueños y optmiza el envio de los paquetes de datos, y el stringify es la que trasforma la cadena de datos en un paquete.json para poder ser optimo el envio.
##### Explica cómo el cliente de escritorio recibe (socket.on) y procesa (JSON.parse, chequeo de type) los datos para actualizar la posición del círculo.

