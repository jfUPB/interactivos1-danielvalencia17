#### Solucion a la actividad

La bomba tiene tres estados.  Configuracion, Armado, explosion estos transisionan entre ellos de la siguiente manera:

##### configuracion
La bomba está desarmada y se ajusta el tiempo de cuenta regresiva con los botones A y B, el tiempo se reduce un segundo cada que se presionan.
###### Eventos y transiciones:
botón A presionado - aumenta el tiempo (máximo 60s), 
botón B presionado - disminuye el tiempo (mínimo 10s), 
gesto Shake - Transición a armado

##### Armado
Inicia la cuenta regresiva en el display led.
###### Eventos y transiciones:
cada segundo, disminuye el contador usando utime.ticks_ms(), 
 cuando el contador llega a 0 - Transición explosion.

##### Explosion
Activa el speaker con un sonido y muestra una calavera en el display led.
###### Eventos y transiciones:
Si se toca el botón Touch → Transición a configuracion con reinicio del contador a 20 s.
