#### Solucion a la actividad

cuanto intente cerre el servidor salio este mensaje
```js
GET http://localhost:3000/socket.io/?EIO=4&transport=polling&t=... net::ERR_CONNECTION_REFUSED
WebSocket connection to 'ws://localhost:3000/socket.io/?EIO=4&transport=websocket&...' failed:
```
significa que no fue capaz de conectarse al servidor pero no obtuvo respuesta, cuando reinicio desaparecen los errores, cuando comento esa linea de codigo la pagina 1 aparece en blanco incialmente solo cuando muevo la dos actualiza el estado, esto es util dependiendo del tipo de interaccion que se quiera, por ejemplo que el espectador no pueda generar una interaccion hasta que el servidor no mande la señal especefica que deberia usar

```js
Page 2 received: { x: 217, y: 109 }
```
este es el mensaje que envie page 2, esto sucede porque el evento lo manda el servidor el cual no se envia al socket donde se origino entonces el que recibe la señal es page 1. haciendo el experimento del if este mensaje Page 2 detected change… aparece cuando muevo un poco la pagina cuando me quedo quieto desaperece esto funciona igual que en el envio de datos binarios y acsii para evitar un envio de paquete de datos inecesarios y sobrecargar el servidor sin necesidad.

##### actividad final
hice todos los cambios necesarios en el codigo y lo que logre es que, el fondo se volviera mas oscuro cuando la ventana se alejaba tambien el circulo crecia dependiendo del tamaño de page 2 o de la ventana remota por ultimo la linea cambiaba entre verde y rojo dependiendo de si estaba en izquiera o derecha aunque no era muy preciso.



