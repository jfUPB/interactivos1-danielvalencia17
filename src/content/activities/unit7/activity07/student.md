#### Solucion a la actividad

##### Evalúa tu confianza: para cada objetivo de aprendizaje, evalúate honestamente usando una escala simple (ej: 2=Necesito repasar mucho, 3=Lo entiendo pero con dudas, 4=Lo entiendo bien, 5=Podría explicarlo a un compañero).

Configurar y usar VS Code Dev Tunnels: 5
Implementar arquitectura cliente-servidor (móvil->servidor): 4
Usar Socket.IO para retransmitir datos (servidor->escritorio): 4
Capturar y procesar eventos en el móvil (p5.js): 3
Modificar sistema interactivo para crear la experiencia: 4
Analizar y explicar flujo de datos completo (móvil->servidor->escritorio): 3

##### ¿Qué concepto o actividad de esta unidad te resultó más fácil de entender o realizar? ¿Por qué crees que fue así?
las actividades de entender el concepto del servidor movil y compararlo con la unidad anterior fueron faciles de entender una vez sabia usar el Vs code tunnels.

##### ¿Qué concepto o actividad te presentó mayor dificultad? ¿Qué pasos seguiste para intentar superarla? ¿Qué recursos o estrategias te fueron más útiles?
la actividad incial ya que se me complico entender por mi cuenta como funcionaba el dev tunels y toda esta integracion con VS code, hablar con el profesor siempre aclara dudas en este tipo de actividades mas complejas, normalmente las primeras que dan la base de la unidad.

##### Describe con tus propias palabras, como si se lo explicaras a alguien que no tomó el curso, cuál es el flujo principal de información en la aplicación que construimos (desde la interacción del usuario en el móvil hasta la imagen en el escritorio). ¿Qué rol juega cada tecnología (Node.js, Socket.IO, Dev Tunnels, p5.js)?
Digamos que tenemos dos personas cada una con un dispositivo distinto, y quieren enviarse informacion de alguna manera, entonces el usario 1 toca la pantalla aleatoriamente lo manda la informacion de la posicion del toque al usario 2, el cual ve como se generan particulas con la misma posicion del usario 1. este es basicamente el funcionamiento de la aplicacion, ahora para que esto suceda tenemos 4 elementos, progamas, conexiones como lo quieras llamar, Node.js, socket.io, dev tunnels y y P5js.

###### Node.js
Es basicamente el servidor intermediario entre usario 1 y 2, el se encarga de trasmitir la informacion.
###### Socket.io
Este es el canal por el que se envian los datos al servidor en tiempo real, para lograr el efecto de la creacion de las particulas de manera inmediata.
###### Dev tunnels
es una extension de la herramienta de progamacion que se usa normalmente para progamar VS Code, esta permite la conexion de usario 1 desde un dispositivo remoto al que esta corriendo el progama.
###### P5.js
Es la tecnologia encargada de dibujar e interpretar de manera visual todos los datos que recibe, es la parte Visual de progama y donde se pueden cambiar las particulas.

##### ¿Cómo crees que podrías aplicar lo aprendido en esta unidad (usar un móvil como controlador, comunicación en tiempo real, túneles) en otros proyectos o contextos?
Esta tecnologia de los tuneles para conectar dispositivos remotos puede ser muy util para montajes interactivos, colocando varias pantallas para interactuar con una proyeccion, o de una manera didactica, para hacer que se resuelvan puzzles moviendo piezas a partir de la pantalla.
