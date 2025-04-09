#### Solucion a la actividad

Segun lo que investigue, las clases son la manera mas facil de crear varios objetos en python, es decir esto define una clase de objetos para que sea mas facil replicarlo usando las maquinas de estado.

```js
from microbit import *

class Semaforo:
    def __init__(self, columna, tiempo_rojo, tiempo_amarillo, tiempo_verde):
        self.columna = columna  # Columna de LEDs (0, 1 o 2)
        self.tiempo_rojo = tiempo_rojo  # Tiempo en milisegundos
        self.tiempo_amarillo = tiempo_amarillo
        self.tiempo_verde = tiempo_verde
        self.estado = 'rojo'  # Estado inicial
        self.tiempo_inicio = running_time()  # Tiempo de inicio
    
    def update(self):
        tiempo_actual = running_time() - self.tiempo_inicio
        
        # Cambiar estados según el tiempo transcurrido
        if self.estado == 'rojo':
            self._mostrar_rojo()
            if tiempo_actual >= self.tiempo_rojo:
                self.estado = 'amarillo'
                self.tiempo_inicio = running_time()
        
        elif self.estado == 'amarillo':
            self._mostrar_amarillo()
            if tiempo_actual >= self.tiempo_amarillo:
                self.estado = 'verde'
                self.tiempo_inicio = running_time()
        
        elif self.estado == 'verde':
            self._mostrar_verde()
            if tiempo_actual >= self.tiempo_verde:
                self.estado = 'rojo'
                self.tiempo_inicio = running_time()
    
    def _mostrar_rojo(self):
        display.set_pixel(self.columna, 0, 9)  # Rojo en la fila 0 (arriba)
        display.set_pixel(self.columna, 2, 0)  # Apagar amarillo
        display.set_pixel(self.columna, 4, 0)  # Apagar verde
    
    def _mostrar_amarillo(self):
        display.set_pixel(self.columna, 0, 0)  # Apagar rojo
        display.set_pixel(self.columna, 2, 9)  # Amarillo en la fila 2 (centro)
        display.set_pixel(self.columna, 4, 0)  # Apagar verde
    
    def _mostrar_verde(self):
        display.set_pixel(self.columna, 0, 0)  # Apagar rojo
        display.set_pixel(self.columna, 2, 0)  # Apagar amarillo
        display.set_pixel(self.columna, 4, 9)  # Verde en la fila 4 (abajo)


semaforo1 = Semaforo(0, 5000, 2000, 3000)  
semaforo2 = Semaforo(1, 3000, 1000, 2000)  
semaforo3 = Semaforo(2, 4000, 3000, 2000) 


while True:
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()
```
