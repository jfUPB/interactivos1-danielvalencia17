#### Solucion de la actividad

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
##### En la función readSerialData() tenemos un bucle que recorre el buffer solo si este tiene 8 o más bytes ¿Por qué?
 ```js
  while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift();
      continue;
    }
```
##### En el código anterior qué significa 0xaa?

##### En el código anterior qué hace la función shift y la instrucción continue? ¿Por qué?

##### Si hay menos de 8 bytes qué hace la instrucción break? ¿Por qué?

   ```js
 if (serialBuffer.length < 8) break;
```

##### ¿Cuál es la diferencia entre slice y splice? ¿Por qué se usa splice justo después de slice?
```js
let packet = serialBuffer.slice(0, 8);
serialBuffer.splice(0, 8);
```

##### A la siguiente parte del código se le conoce como programación funcional ¿Cómo opera la función reduce?
 ```js
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;
```

##### ¿Por qué se compara el checksum enviado con el calculado? ¿Para qué sirve esto?

 ```js
if (computedChecksum !== receivedChecksum) {
    console.log("Checksum error in packet");
    continue;
}
```
##### En el código anterior qué hace la instrucción continue? ¿Por qué?

##### ¿Qué es un DataView? ¿Para qué se usa?
 ```js
let buffer = new Uint8Array(dataBytes).buffer;
let view = new DataView(buffer);
```
##### ¿Por qué es necesario hacer estas conversiones y no simplemente se toman tal cual los datos del buffer?
 ```js
    microBitX = view.getInt16(0) + windowWidth / 2;
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
```
