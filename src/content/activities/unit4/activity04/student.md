#### Solucion a la actividad

Inicialmente la diferencia que noto es que el codigo base tiene mucho mas sources, en cuanto al sketch no noto nada muy distinto, la zona con la funcion preload se utiliza para cargar los archivos base, vectores, sonidos etc, que necesita el progama para funcionar, luego entra la zona donde se utiliza los puertos seriales en toda la conversacion con el profe entendi mejor esta parte, los datos seriales se envian a traves de esta linea
```js
data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
```
Lo que hace es que en cada espacio esta destinado para uno de los datos que estan entre parentesis, el envia los datos en formato ASCII y espera que se envien los 4 datos para enviar el enter (/n), si no se envian correctamente el progama hacer automaticamente la funcion de enviar los datos que le han llegado hasta el momento pero dañando el funcionamiento del progama, la suma  windowWidth/2 y windowHeight/2 se debe utilizar para centrar los valores desde el 0,0 de la pantalla de lo contrario estaria en la zona superior izquierda, el updatebuttonstate es funcion que compara los cambios de estados de los botones, es decir, el lee si hay algun cambio en el estado de un boton, ejemplo, que pase de notpressed a pressed, es importante guardar el estado de los botones para detectar un "clic" único en lugar de un evento continuo mientras el botón está presionado, si no se hiciera el boton se mantiene presionado continuamente y no se siente la diferencia entre un clic largo y uno corto.

##### ___

en el nuevo codigo ya la tecla espacio no elimina el fondo si no la tecla de borrar, basicamente coloca el background nuevamente en blanco, este tiene varias funcionas que varian en compracion a la primera que son basicamentes las que tienen que ver directamente con la integracion con el microbit, con "no se estan recibiendo cuatro datos del microbit" no me aparece, intente de todas las maneras que saliera pero no me ocurre este mensaje.
