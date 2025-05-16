#### Solucion a la actividad

##### funcionamiento
https://www.flexclip.com/es/share/8333841dde3024f2fcea3ebfdc7667d1e863422.html

##### Codigo para micro.bit
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

def actualizar_display(tiempo):
    display.show(str(tiempo)) 

def explotar():
    display.show(Image.SKULL)
    music.play(music.POWER_DOWN)
    sleep(1000)
    display.clear()

while True:
    if estado == CONFIGURACION:
        display.scroll("Config")
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
            sleep(100)
        
        estado = CONFIGURACION
        contador = 20  
        display.scroll("Reset")
```
