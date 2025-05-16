#### Solucion de la actividad

![image](https://github.com/user-attachments/assets/6b630ccf-376e-4046-b136-97d24591bb54)


##### En la unidad anterior abordaste la construcción de un protocolo ASCII. En esta unidad realizaste lo propio con un protocolo binario. Realiza una tabla donde compares, según la aplicación que modificaste en la fase de aplicación de ambas unidades, los siguientes aspectos: eficiencia, velocidad, facilidad, usos de recursos. Justifica con ejemplos concretos tomados de las aplicaciones modificadas.

##### ¿Por qué fue necesario introducir framing en el protocolo binario?
que que en el protocolo binario se emvian muchos mas datos que en el acscii lo cual colapsa el canal

##### ¿Cómo funciona el framing?
el framing suma los datos en numeros y los coloca en paquetes que es lo que envia al progama
##### ¿Qué es un carácter de sincronización?

##### ¿Qué es el checksum y para qué sirve?
Esto convierte los datos en enteros y los coloca en un numero del 0 al 255 esto sirve despues para verificar que los paquetes lleguen de manera correcta

##### ¿Qué hace la función concat? ¿Por qué?
 ```js
function readSerialData() {
    let available = port.availableBytes();
    if (available > 0) {
        let newData = port.readBytes(available);
        serialBuffer = serialBuffer.concat(newData);
    }
```
une dos arreglos, esta va cortando los bytes hasta que tiene los 8 que necesita

##### En la función readSerialData() tenemos un bucle que recorre el buffer solo si este tiene 8 o más bytes ¿Por qué?
 ```js
  while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift();
      continue;
    }
```
Para asegurarse de que los paquetes de datos lleguen completos, es el /n pero de binario.

##### En el código anterior qué significa 0xaa?
Es un numero hexadecimal, lo que hace ahi es la conversion del numero binario a enteros.

##### En el código anterior qué hace la función shift y la instrucción continue? ¿Por qué?
Se usa para desechar bytes, es decir los paquetes de datos que esten incompletos los deja de utilizar hasta que llegue el paquete correcto 0xaa y continue funciona para pasar a la siguiente iteraccion si el paquete esta correcto

##### Si hay menos de 8 bytes qué hace la instrucción break? ¿Por qué?

   ```js
 if (serialBuffer.length < 8) break;
```
Esto hace que se salga del while esperando por mas datos.

##### ¿Cuál es la diferencia entre slice y splice? ¿Por qué se usa splice justo después de slice?
```js
let packet = serialBuffer.slice(0, 8);
serialBuffer.splice(0, 8);
```
Slice corta los bytes y splice los reune desechando la parte que no funciono, por eso uno va despues del otro

##### A la siguiente parte del código se le conoce como programación funcional ¿Cómo opera la función reduce?
 ```js
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;
```
Convierte el arreglo en un solo numero, en este caso uno entre 0 y 255 

##### ¿Por qué se compara el checksum enviado con el calculado? ¿Para qué sirve esto?

 ```js
if (computedChecksum !== receivedChecksum) {
    console.log("Checksum error in packet");
    continue;
}
```
Para asegurarse de que el paquete este completo, y no tenga errores, es como una especie de verificacion.

##### En el código anterior qué hace la instrucción continue? ¿Por qué?
por si algun paquete vino corrupto continuar con el siguiente y no quedarse pensando.

##### ¿Qué es un DataView? ¿Para qué se usa?
 ```js
let buffer = new Uint8Array(dataBytes).buffer;
let view = new DataView(buffer);
```
se utiliza para poder generar la visualizacion de los datos que nos este llegando de un dispositvio o señal.

##### ¿Por qué es necesario hacer estas conversiones y no simplemente se toman tal cual los datos del buffer?
 ```js
    microBitX = view.getInt16(0) + windowWidth / 2;
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
```
Porque los datos que llegan, por decirlo asi, estan en otro idioma, por si solos realmente no significan nada toca generar la conversion para que tengan sentido en un contexto del progama que estamos utilizando.
