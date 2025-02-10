#### Solucion a la actividad

En este ejericio solo use el progama del microbit, simplemente genere la variable de presionar el boton A y shake, y utilize el codigo que viene de ejemplo para generar sonidos.

```js
from microbit import *
import music

uart.init(baudrate=115200)


while True:
    if button_a.is_pressed():
        music.play(music.BIRTHDAY)
        sleep(500)
    if accelerometer.was_gesture('shake'):
        music.play(music.PUNCHLINE) 
        sleep(500)
```
