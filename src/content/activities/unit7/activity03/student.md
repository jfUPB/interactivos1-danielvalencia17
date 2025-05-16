#### Solucion a la actividad

##### ¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?
lo que hace es mandar archivos estaticos, el ejemplo mas claro es el index de las pagina web el public es para que lo busque especificamente en la carpeta public del repositorio, la diferencia con app.get es que en esta ultima podemos dar control total a como queremos que se manejen estos archivos estaticos y su orden, es una respuesta mas rapida porque va exactamente a la direccion que le especificamos.

##### Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?
touch.moved recibe la señal de tacto en el celular, esto se pasa a enviar los datos con socket.emit que recibe el servidor de node.js con touchmovement,esto lee los datos que envio el servidor remoto y esto llega al servidor de escritorio con socket.broadcastemit que envia los datos a los clientes exepeto a quien los envio.

##### Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?
mientras se haga con socket.broadcast enviara los datos a ambos computadores de escritorio, ya que retrasmite a ambas a exepeto a ella misma.

##### ¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?
con esto puedo hacer que en la consola me muestre cualquier dato que considere necesario en la fase de pruebas para poder depurar errores.
