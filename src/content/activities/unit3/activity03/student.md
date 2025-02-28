#### Solucion de la actividad



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


evento_ocurrido = False  
evento = ""  

secuencia = ['A', 'B', 'A', 'S']
indice_secuencia = 0
tiempo_ultima_secuencia = utime.ticks_ms()

def actualizar_display(tiempo):
    display.show(str(tiempo))

def explotar():
    display.show(Image.SKULL)
    music.play(music.POWER_DOWN)
    sleep(1000)
    display.clear()

def tareaEventos():
    global evento_ocurrido, evento
    if button_a.was_pressed():
        evento = 'A'
        evento_ocurrido = True
    
    if button_b.was_pressed():
        evento = 'B'
        evento_ocurrido = True

    if accelerometer.was_gesture("shake"):
        evento = 'S'
        evento_ocurrido = True

    if uart.any():
        mensaje = uart.read().decode('utf-8').strip()
        if mensaje:
            evento = mensaje
            evento_ocurrido = True

def tareaBomba():
    global estado, contador, ultimo_tiempo, evento_ocurrido, evento, indice_secuencia, tiempo_ultima_secuencia

    if estado == CONFIGURACION:
        actualizar_display(contador)

        if evento_ocurrido:
            if evento == 'A' and contador < 60:
                contador += 1
                actualizar_display(contador)
            elif evento == 'B' and contador > 10:
                contador -= 1
                actualizar_display(contador)
            elif evento == 'S':
                estado = ARMADO
                display.scroll("Armed")
                ultimo_tiempo = utime.ticks_ms()

            evento_ocurrido = False  # Consumir el evento

    elif estado == ARMADO:
        tiempo_actual = utime.ticks_ms()

        if indice_secuencia < len(secuencia) and evento_ocurrido:
            if evento == secuencia[indice_secuencia]:
                indice_secuencia += 1
                evento_ocurrido = False  # Consumir el evento

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

        while True:
            if uart.any():
                mensaje = uart.read().decode('utf-8').strip()
                if mensaje == 'T':
                    estado = CONFIGURACION
                    contador = 20
                    display.scroll("Reset")
                    break
            sleep(50)


sleep(500)
display.scroll("Config")

while True:
    tareaEventos()  
    tareaBomba()
```
