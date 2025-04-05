#### Solucion a la actividad

##### Si estoy en el ESTADO_X y recibo el evento Y, entonces deben ocurrir estas acciones y debo ir al ESTADO_Z.

"CONFIGURACIÓN", "Botón A presionado", "Incrementar contador (+1 seg, máx. 60)", "CONFIGURACIÓN", "[X]"

"CONFIGURACIÓN", "Botón B presionado", "Decrementar contador (-1 seg, mín. 10)", "CONFIGURACIÓN", "[X]"

"CONFIGURACIÓN", "Gesto 'Shake'", "Cambia estado a ARMADO", "ARMADO", "[X]"

"CONFIGURACIÓN", "Mensaje serial 'S'", "Cambia estado a ARMADO", "ARMADO", "[X]"

"CONFIGURACIÓN", "Contador en 60, Botón A presionado", "No debe incrementar más allá de 60", "CONFIGURACIÓN", "[X]"

"CONFIGURACIÓN", "Contador en 10, Botón B presionado", "No debe decrementar más allá de 10", "CONFIGURACIÓN", "[X]"

"ARMADO", "Secuencia correcta 'A, B, A, S'", "Restablece a CONFIGURACIÓN", "CONFIGURACIÓN", "[X]"]

"ARMADO", "Secuencia incorrecta 'A, A, B, S'", "No cambia estado, espera secuencia correcta", "ARMADO", "[X]"

"ARMADO", "Tiempo llega a 0", "Cambia estado a EXPLOSIÓN", "EXPLOSIÓN", "[X]"

"ARMADO", "Se recibe evento inesperado (ej. 'X')", "No cambia estado ni afecta secuencia", "ARMADO", "[X]"

"EXPLOSIÓN", "Mensaje serial 'T'", "Restablece a CONFIGURACIÓN", "CONFIGURACIÓN", "[X]"

"EXPLOSIÓN", "Botón A/B/S presionado", "No debe cambiar estado, sigue en explosión", "EXPLOSIÓN", "[X]"
