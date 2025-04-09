#### Solucion de la actividad

##### ¿Por qué esta técnica es poderosa para la escalabilidad de tu aplicación en términos de concurrencia y de manejo de eventos?
Este tipo de codigo funciona muy bien a la hora de crear una simulacion de algo, o caminos multiples a la hora de resolver una actividad o interactuar con ella, suponiendo que es una experiencia interactiva puede llevar a que los usuarios hagan lo que hagan interactuen de manera correcta con la experiencia, este sistema maneja una especie de modularidad en la cual es muy facil agregar eventos nuevos y posibles caminos nuevos sin afectar mucho al resto del codigo.

##### ¿Qué ventajas y desventajas tiene el tipo de pruebas que realizaste en esta unidad?
Con estas pruebas podemos abarcar una gran cantidad de posibles funciones y caminos inesperados que podria hacer un usuario que no entendio bien la funcionalidad o que simplemente quiere intentar dañar la funcionalidad del sistema, con estos verificamos que todo siempre lleve a donde deseamos que llegue, como un contra es que todo esto depende principalmente de la comunicacion serial de los dispositivos, asi que poniendolo en una situacion limite de mandar informacion desmesuradamente podria complicar este tipo de pruebas.

##### ¿Por qué son importantes las pruebas de regresión? ¿Qué pasa si modificas tu aplicación y no haces las pruebas de regresión?
Lo mas importante de estas pruebas es comprobar lo que pasa muchas veces en el codigo y es que cuando arreglas un error aparecen 3, lo que hace esto es reverificar la funcionalidad total del codigo para asegurarte de que el error alla quedado solucionado sin que afectara el resto de cosas que estaban bien.
