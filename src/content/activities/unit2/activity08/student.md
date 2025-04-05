#### Solucion a la actividad

El ejemplo planteado funciona con una clase que es "pixel", esto controla el estado de un pixel en el microbit, esto funciona en el rango de (apagado 0 ------------ 9 encendido) el codigo enciende dos pixeles (pixel 1 y 2) y tienen cuatro atributos, posicion en X, y, estado inicial e intervalo, las lineas de update generan un nuevo estado cuando pasa el tiempo de intervalo y el "while true" funciona como un bucle.

los estados que identifico son en dos partes, cuando inicia y en las zonas del waittimeout. los eventos se dan cuando los "if" preguntan si el led esta encendido o no y la accion es el display.set.pixel que enciende el led.
