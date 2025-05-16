#### Solucion a la actividad
EL progama comienza un estado incial y se comienza el bucle que es definido con la variable (while True), ahora el comienza a pasar entre los tres estados posibles en el intervalo que les fue asignado ahora comienza a funcionar con un sistema de if mientras esta en el intevalo, si se presiona el boton A el progama lo detecta y pasa al siguiente con un intervalo de 2000ms, si no pasa al siguiente estado en el tiempo asigando, asi en bucle, basicamente el progama tienes dos posibles salidas en el cambio de estados.

 ##### Practica de vectores
 Vectores de prueba tiene un estado incial de "enojado", y otros tres estados "feliz, triste y confundido" funciona de la siguiente manera:

###### Vector de prueba 1: De enojado a feliz y luego a triste
Estado inicial: El micro:bit comienza mostrando la cara enojada,
Se presiona el botón A para cambiar a la cara feliz,
Se presiona el botón B para cambiar a la cara triste,
Después de 2 segundos sin presionar ningún botón, vuelve a la cara enojada.

###### Vector de prueba 2: De enojado a confundido por sacudida
Estado inicial: El micro:bit comienza mostrando la cara enojada ,
Se detecta una sacudida y el micro:bit cambia a la cara confundida,
Después de 2 segundos sin presionar ningún botón, vuelve a la cara enojada .

###### Vector de prueba 3: Ciclo completo (enojado → feliz → triste → confundido → enojado)
Estado inicial: El micro:bit comienza mostrando la cara enojada,
Se presiona el botón A para cambiar a la cara feliz,
Se presiona el botón B para cambiar a la cara triste,
Se detecta una sacudida y el micro:bit cambia a la cara confundida,
Después de 2 segundos, el micro:bit vuelve a la cara enojada.

```js
from microbit import *
import utime

# Definir los estados
STATE_ANGRY = 1
STATE_HAPPY = 2
STATE_SAD = 3
STATE_CONFUSED = 4

# Definir los intervalos
DEFAULT_INTERVAL = 2000  # Intervalo de 2 segundos

current_state = STATE_ANGRY  # Comienza con la cara enojada
start_time = 0
interval = DEFAULT_INTERVAL  # Intervalo para cada estado (2 segundos)

while True:
    # Mostrar la cara en función del estado actual
    if current_state == STATE_ANGRY:
        display.show(Image.ANGRY)
    elif current_state == STATE_HAPPY:
        display.show(Image.HAPPY)
    elif current_state == STATE_SAD:
        display.show(Image.SAD)
    elif current_state == STATE_CONFUSED:
        display.show(Image.CONFUSED)

    # Si se presiona el botón A, cambiar a cara feliz
    if button_a.was_pressed():
        current_state = STATE_HAPPY
        start_time = utime.ticks_ms()  # Reinicia el tiempo

    # Si se presiona el botón B, cambiar a cara triste
    if button_b.was_pressed():
        current_state = STATE_SAD
        start_time = utime.ticks_ms()  # Reinicia el tiempo

    # Si se detecta una sacudida, cambiar a cara confundida
    if accelerometer.is_gesture("shake"):
        current_state = STATE_CONFUSED
        start_time = utime.ticks_ms()  # Reinicia el tiempo

    # Si ha pasado el intervalo de 2 segundos, volver a la cara enojada
    if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
        current_state = STATE_ANGRY
        start_time = utime.ticks_ms()  # Reinicia el tiempo
```
