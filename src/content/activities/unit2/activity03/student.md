#### Solucion a la actividad

##### Entradas del Micro:bit
Botón A y B: dos botones físicos en la placa que pueden detectar si están presionados,
Pines táctiles: funcionan como entradas táctiles, detectando contacto con los dedos o materiales conductores,
Acelerómetro: detecta movimientos y cambios de inclinación en los ejes X, Y y Z,
Sensor de luz: mide la cantidad de luz ambiental utilizando la matriz de LEDs.

##### Salidas del Micro:bit
Matriz de LEDs: Pantalla de 5x5 que puede mostrar imágenes y texto,
Zumbador/bocina: Genera sonidos y tonos musicales,
Pines de salida: Permiten controlar LEDs, motores y otros componentes electrónicos,
Bluetooth: Permite comunicación inalámbrica entre múltiples Micro:bits.

#### ejemplos
##### Entradas

Detecta si el boton A esta presionado
```js
from microbit import *

while True:
    if button_a.is_pressed():
        display.show("A")
```
Lector de valores analogicos
```js
from microbit import *

while True:
    valor = pin1.read_analog()
    display.scroll(str(valor))
```
Lectura de la aceleracion en el eje X
```js
from microbit import *

while True:
    x = accelerometer.get_x()
    display.scroll(str(x))
```
##### Salidas
Muestra imagenes en la pantalla
```js
from microbit import *

display.show(Image.HEART)
```
activa una salida digital en el pin 1
```js
from microbit import *

pin0.write_digital(1)  # Activa un LED conectado al pin 0
```
Reproduce un sonido usando la bocina
```js
import music

music.play(music.NYAN)
```

