from microbit import *
import utime

class TrafficLight:
    def __init__(self, interval):
        self.state = "Red"           # Estado inicial del semáforo (rojo)
        self.startTime = 0           # Marca el tiempo en que el estado cambió
        self.interval = interval     # Intervalo de tiempo para cambiar de estado

    def update(self):
        # Controla la lógica de cambio de estado del semáforo
        if self.state == "Red":
            self.display_red()
        elif self.state == "Yellow":
            self.display_yellow()
        elif self.state == "Green":
            self.display_green()

    def display_red(self):
        if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
            # Enciende el píxel rojo (en la posición (0,0))
            display.set_pixel(0, 0, 9)  # Rojo
            display.set_pixel(0, 1, 0)  # Apaga el amarillo
            display.set_pixel(0, 2, 0)  # Apaga el verde
            self.state = "Yellow"
            self.startTime = utime.ticks_ms()  # Reinicia el temporizador

    def display_yellow(self):
        if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
            # Enciende el píxel amarillo (en la posición (0,1))
            display.set_pixel(0, 0, 0)  # Apaga el rojo
            display.set_pixel(0, 1, 9)  # Amarillo
            display.set_pixel(0, 2, 0)  # Apaga el verde
            self.state = "Green"
            self.startTime = utime.ticks_ms()

    def display_green(self):
        if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval:
            # Enciende el píxel verde (en la posición (0,2))
            display.set_pixel(0, 0, 0)  # Apaga el rojo
            display.set_pixel(0, 1, 0)  # Apaga el amarillo
            display.set_pixel(0, 2, 9)  # Verde
            self.state = "Red"
            self.startTime = utime.ticks_ms()

# Crea un semáforo con intervalo de 2000 ms (2 segundos) por estado
traffic_light = TrafficLight(2000)

while True:
    traffic_light.update()  # Actualiza el estado del semáforo
    sleep(10)  # Pausa para optimizar el rendimiento
