#### Solucion a la actividad

##### 1 Presionar A varias veces en Configuración
Incrementa contador hasta 60,
Funciona correctamente

##### 2 Presionar B varias veces en Configuración
Decrementa contador hasta 10,
Funciona correctamente

##### 3 Agitar el micro:bit
Cambia a estado ARMADO,
Funciona correctamente

##### 4 Esperar a que la cuenta regresiva llegue a 0
Cambia a estado EXPLOSION,
Funciona correctamente

##### 5 Tocar el logo en EXPLOSION
Reinicia a CONFIGURACION,
No siempre detecta el toque

#### Errores Encontrados y Correcciones

1. El logo no siempre detecta el toque
El sensor táctil del logo no respondía de manera confiable.
Corrección: Se aumentó el tiempo de espera para mejorar la detección y se agregó un bucle para asegurarse de que el toque sea registrado.

2. Interfaz de usuario poco clara al iniciar
No había un mensaje inicial que indicara el estado del dispositivo.
Corrección: Se agregó un mensaje de "Config" al encender.

3. Tiempo de actualización del display impreciso
La cuenta regresiva no era exacta por la forma en que utime.ticks_ms() se manejaba.
Corrección: Se utilizó una estructura de control más precisa para el temporizador.

#### Codigo corregido
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

