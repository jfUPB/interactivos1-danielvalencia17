#### Solucion de la actividad

En el estado armado de la use variables de if y elif, cuando se cumple el requisito de la secuencia hace otro if que entra al estado de configuracion.

##### Codigo de microbit

```js
from microbit import *
import utime
import music

CONFIGURACION = 0
ARMADO = 1
EXPLOSION = 2

estado = CONFIGURACION
contador = 20
ultimo_tiempo = utime.ticks_ms()

secuencia = [button_a, button_b, button_a, "shake"]
indice_secuencia = 0
tiempo_ultima_secuencia = utime.ticks_ms()

def actualizar_display(tiempo):
    display.show(str(tiempo))

def explotar():
    display.show(Image.SKULL)
    music.play(music.POWER_DOWN)
    sleep(1000)
    display.clear()

display.scroll("Config")

while True:
    if estado == CONFIGURACION:
        actualizar_display(contador)

        if button_a.was_pressed():
            if contador < 60:
                contador += 1
                actualizar_display(contador)

        if button_b.was_pressed():
            if contador > 10:
                contador -= 1
                actualizar_display(contador)

        if accelerometer.was_gesture("shake"):
            estado = ARMADO
            display.scroll("Armed")
            ultimo_tiempo = utime.ticks_ms()

    elif estado == ARMADO:
        tiempo_actual = utime.ticks_ms()

        
        if indice_secuencia < len(secuencia):
            if secuencia[indice_secuencia] == button_a and button_a.was_pressed():
                indice_secuencia += 1
            elif secuencia[indice_secuencia] == button_b and button_b.was_pressed():
                indice_secuencia += 1
            elif secuencia[indice_secuencia] == "shake" and accelerometer.was_gesture("shake"):
                indice_secuencia += 1

        
        if indice_secuencia == len(secuencia):
            estado = CONFIGURACION
            contador = 20
            display.scroll("Reset")
            indice_secuencia = 0

        
        if tiempo_actual - ultimo_tiempo >= 1000:
            ultimo_tiempo = tiempo_actual
            if contador > 0:
                contador -= 1
                actualizar_display(contador)
            else:
                estado = EXPLOSION

    elif estado == EXPLOSION:
        explotar()

        while not pin_logo.is_touched():
            sleep(50)

        estado = CONFIGURACION
        contador = 20
        display.scroll("Reset")
```
