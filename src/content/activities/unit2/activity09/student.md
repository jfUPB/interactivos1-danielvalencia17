#### Solucion a la actividad

El semaforo funciona con maquinas de estados que activa cada color en el intervalo, funciona principlamente por esta funcion "if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:", ,con un intervalo de tiempo de 2 segundos entre estados, cada color cambia la posicion en la que enciende el led.

##### Codigo en Micro.bit
```js
from microbit import *
import utime

class TrafficLight:
    def __init__(self, interval):
        self.state = "Red"           
        self.startTime = 0          
        self.interval = interval    
    def update(self):
        if self.state == "Red":
            self.display_red()
        elif self.state == "Yellow":
            self.display_yellow()
        elif self.state == "Green":
            self.display_green()

    def display_red(self):
        if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
            display.set_pixel(0, 0, 9) 
            display.set_pixel(0, 1, 0)  
            display.set_pixel(0, 2, 0) 
            self.state = "Yellow"
            self.startTime = utime.ticks_ms() 
    def display_yellow(self):
        if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
            display.set_pixel(0, 0, 0)  
            display.set_pixel(0, 1, 9)  
            display.set_pixel(0, 2, 0)  
            self.state = "Green"
            self.startTime = utime.ticks_ms()

    def display_green(self):
        if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
            display.set_pixel(0, 0, 0) 
            display.set_pixel(0, 1, 0) 
            display.set_pixel(0, 2, 9)  
            self.state = "Red"
            self.startTime = utime.ticks_ms()

traffic_light = TrafficLight(2000)

while True:
    traffic_light.update() 
    sleep(10)  
```
