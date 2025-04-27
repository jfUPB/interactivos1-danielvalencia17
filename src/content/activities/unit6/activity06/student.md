#### Solucion a la actividad

##### Describe con tus propias palabras cuál es la función del servidor Node.js en la arquitectura que exploramos. ¿Por qué los clientes p5.js no se comunican directamente entre sí?
Node crea un servidor local que se encarga de enviar y recibir los datos que envian las paginas, los clientes no se comunican porque necesitan un servidor ya que las pagina web no permiten conexiones directas.

##### Explica la diferencia fundamental entre socket.emit() y socket.broadcast.emit() en el contexto de Socket.IO en el servidor. ¿Cuándo usarías cada uno?
socket emit envia solo al ciente que envio la conexion es decir envia y recibe del mismo, socket.broadcast.emit() envia un mensaje a todos los clientes menos el que origino el evento, este ultimo se usaria para lkos datos que se envian constatenmente y el socket.emit para datos mas especificos como configuracion o verificaciones.

##### Compara la comunicación mediante Node.js/Socket.IO con la comunicación serial (ASCII y binaria con framing) que viste en unidades anteriores. Menciona al menos una ventaja y una desventaja de cada enfoque según el contexto de aplicación (ej. conectar micro:bit vs. conectar dos navegadores).

![image](https://github.com/user-attachments/assets/7751d434-072a-4b6d-bf09-20d82c3593a2)


##### ¿Qué rol juega el protocolo http y qué rol juega socket.io (que usa WebSockets por debajo) en la aplicación del caso de estudio?
http su rol es mandar los archivos que  solicita el servidor para cargar la pagina inicial el socket se encarga de mantener una conexion en tiempo real entre el servidor y el navegador.

##### ¿Qué fue lo más sorprendente o interesante que aprendiste sobre la comunicación en red en esta unidad?
Lo mas interesante son lo que se puede lograr haciendo estas conexiones mandando datos a partir del servidor, se puede generar interacciones muy interesantes entre las paginas.
