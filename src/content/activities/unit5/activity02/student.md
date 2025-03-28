#### Solucion a la actividad

##### Envio de datos binarios por el puerto serial
![image](https://github.com/user-attachments/assets/cd8a2578-1351-4fdf-a5ca-b3effc9fb299)
![image](https://github.com/user-attachments/assets/07c72679-6209-4cf3-95c0-383ab9491e2c)

Enviar los datos en ascii hace mucho mas facil la lectura de los datos, si se sabe cuales son los datos que se van a enviar es mejor en binario por la compresion pero si es alguna prueba considero que es mejor el ascii, se estan enviando 6 datos cuando se hace el gesto shake
![image](https://github.com/user-attachments/assets/af329a28-607f-4b92-9486-004f527f7caa)

Cada uno tiene un numero entero que no veo que haga nada al lado de cada datos, los dos primero son la posicion en X y Y que tiene el microbit cuando se hace el gesto en shake y los otros dos son el true y false de la A y B, cuando esta en true aparece como 1, cuando intento sacar resultados negativos simplemente aparecen 00 no entiendo como se podria ver.
![image](https://github.com/user-attachments/assets/0496f792-b775-4055-8953-2eedbc186ee5)

Es mucho mas facil de leer los datos en texto pero en hex es mucho mas complejo y lanza muchisimos mas datos de los necesarios, considero que tienen usos distintos dependiendo de la utilizacion que se le vaya a dar, digamos que tanta interaccion tiene con el usario nuestro proyecto, para evitar sobrecargas del puerto serial seria mejor usar formato binario.


