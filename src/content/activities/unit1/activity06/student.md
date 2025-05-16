#### Solucion a la actividad
Mis conocimiento previos a esta actividad de basan principalmente en trabajar con arduino asi que lo voy a intentar explicar con esa base.

##### Punto 15
El microbit funciona como un dispositivo de entrada y salidas de señales que se mapean atraves del primer progama que uso, se sube el codigo al microbit y con el otro codigo se le dan las bases para generar ese pequeño visual, se entienden los botones como dispositivos on/off (1 y 0) esto hace que cuando lo presionemos cierre el circuito y mande la señal para generar el visual A o B dependiendo de lo que oprimamos.
##### Punto 16
En este punto funciona igual que los dos anteriores con la diferencia de que la señal se activa atraves del acelerometro del microbit cuando dependiendo de su posicion o velocidad genera la señal de activacion.
##### Punto 17
Este es el que menos entiendo pero supongo que el boton funciona por la parte final del codigo donde dice: 
```
function sendBtnClick() {
    port.write('h');
}
```
Esto manda la señal al dispositivo de escribir la variable "h" y trasforma en el sistema de leds.
