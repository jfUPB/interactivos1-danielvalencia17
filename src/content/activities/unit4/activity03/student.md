#### Solucion a la actividad

xValue: la inclinación en el eje X del acelerómetro.
yValue: la inclinación en el eje Y del acelerómetro.
aState: si el botón A está presionado (True o False).
bState: si el botón B está presionado (True o False).

```js
"{},{},{},{}\n".format(xValue, yValue, aState,bState)
```
En esta zona es donde se almacenan los datos de la señal analogica del microbit, los formatos se mandan en formato CSV, que es una manera de guardar datos de manera plana con una especie de archivo txt, literalmente siginifica (Coma Separated Values), se usa las comas y el separado para diferencia cada valor si no se usara los datos enviados por la terminal serial se ven asi
(969652TrueFalse969652TrueFalse),Este mensaje se envía cada 100 ms
```js
(sleep(100))
```
lo que significa que la frecuencia de transmisión es 10 Hz, si no se usara se podria sobrecargar el puerto serial haciendo quye el progama falle, los valores en las posiciones del eje x y el eje y del acelerometro cambian dependiendo de como movamos el microbit, lo maximo que logre sacar hacia cada eje fueron 1024, si se presiona alguno de los dos botones cambian su estado a true de lo contrario estan en false, cuando se cambia a (is pressed), despues de presionar el boton queda en estado true, los caracteres que se envian por el pueto serial estan en caracteres ASCII, lo cual es como una especie de lenguaje de codificacion de datos, lo que obtuve en la prueba fue lo siguiente:

```js
39 36 39 2C 36 35 32 2C 54 72 75 65 2C 46 61 6C 73 65 0A
```
Esto es porque cada numero se represente con un 3 antes es decir: 39 36 39 --- 969, y el 2C y 0A representas las comas y el punto final.

