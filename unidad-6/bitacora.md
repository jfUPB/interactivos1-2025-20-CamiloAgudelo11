
# Evidencias de la unidad 6


## Acividad 01

¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?

Se instalo todo el proyecto para que la aplicacion funcione.


¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?

Aparecio "Server listening on port 3000", y esto indica qque el servidor esta funcionando y esta esperando para recibir ordenes.


Describe lo que ves inicialmente en page1 y page2 en tu navegador.

Se muestran 2 paginas web en cada una hay una bola roja que esta con una cuerda que las une.

¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?

A user connected - ID: atjgqKeyr4oJjlkMAAAB
Received win1update from ID: atjgqKeyr4oJjlkMAAAB Data: { x: -7, y: 0, width: 767, height: 695 }
Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 0
Sync status: pages=false, synced=false, clients=1
Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 1
Sync status: pages=false, synced=true, clients=1
A user connected - ID: QDP32K0uaG-jyN57AAAD
Received win2update from ID: QDP32K0uaG-jyN57AAAD Data: { x: 752, y: 106, width: 770, height: 696 }


Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?


Al mover una pagina la otra la sigue uniendo con la cuerda, pero sin moverse la bola.

All clients are fully synced
Received win2update from ID: QDP32K0uaG-jyN57AAAD Data: { x: 776, y: 36, width: 768, height: 695 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2

## Acividad 02

Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.

En mi casa y en la Universidad me conecto por Wi-Fi esa seria mi rampa de acceso y si se corta no tendria conexion o en algun caso prenderia los datos moviles para seguir utilizando ya sea paginas web, enviar mensajes,etc.

¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?

Restaurante: yo soy el cliente, el mesero es el servidor. Yo pido comida y él me trae el plato.

Biblioteca: yo soy el cliente, la biblioteca es el servidor. Yo pido un libro y me lo entregan.

Cajero automático: yo soy el cliente, el cajero es el servidor. Yo pido dinero y la máquina me lo entrega.


Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?

Ejemplo: https://www.youtube.com/

Protocolo: https://

Dominio: www.youtube.com

Ruta: en este caso no hay
Si solo escribo www.youtube.com, el servidor me envía la página principal por defecto .


Compara HTTP con los protocolos seriales que usaste.

¿Qué similitudes encuentras?


Los dos deifinen reglas claras para que dos partes se puedan entender.



¿Qué diferencias clave ves?


En serial era solo enviar bytes, en cambio en HTTP hay peticiones, respuestas y demas.


¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?


Es mas complejo ya que maneja mas tipos de datos ya sean imagenes, texto o video y una comunicacion entre miles de dispositivos.


Piensa en una página web simple, como un formulario de login.

¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?

Los campos de usuario o la contraseña.


¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?

El color de los botones, el estilo o la fuente del texto


¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?

Validar si estan completos los campos y mostrar por ejemplo contraseña incorrecta.


Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.

¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?

Ventaja es que reacciona cuando pasa algo lo hace mas eficiente.


¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?


No seria nada eficiente ya que nada cambia en este tiempo.

¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?

Es util ya que se utiliza un lenguaje para todo lo que facilita en todo aspecto ya sea aprender, compartir y trabajar en equipo en un codigo.


Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?

El HTTP es cuando la persona pide y el servidor responde, mientras que usando WebSockets es una conexion directa y que es continua donde ambos se pueden enviar mensajes en tiempo real. La he visto ya sea en juegos en linea o videollamadas


## Acividad 03


Cambia la primera ruta de /page1 a /pagina_uno.

Inicia el servidor.

Intenta acceder a http://localhost:3000/page1. ¿Funciona?


No funciono


Ahora intenta acceder a http://localhost:3000/pagina_uno. ¿Funciona?


Si funciona

¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? Restaura el código.


El servidor solo responde a la ruta especifica que se tenga definida 


Asegúrate de que el servidor esté corriendo (npm start).

Abre http://localhost:3000/page1 en una pestaña. Observa la terminal del servidor. ¿Qué mensaje ves? Anota el ID.


Se mostro un ID unico en la terminal

Abre http://localhost:3000/page2 en OTRA pestaña. Observa la terminal. ¿Qué mensaje ves? ¿El ID es diferente?


Aparece otro ID unico diferente en al page1

Cierra la pestaña de page1. Observa la terminal. ¿Qué mensaje ves? ¿Coincide el ID con el que anotaste?


Se muestra un mensaje de User Disconected con el mismo ID que tenia en la pagina.

Cierra la pestaña de page2. Observa la terminal.

Aparece tambien lo mismo de la page1 con la diferencia que es el ID de page2


Inicia el servidor y abre page1 y page2.

Mueve la ventana de page1. Observa la terminal del servidor. ¿Qué evento se registra (win1update o win2update)? ¿Qué datos (Data:) ves?


En la terminal mostro Received win1update 


Mueve la ventana de page2. Observa la terminal. ¿Qué evento se registra ahora? ¿Qué datos ves?



En la terminal mostro Received win2update 



Experimento clave: cambia socket.broadcast.emit(‘getdata’, page1); por socket.emit(‘getdata’, page1); (quitando broadcast). Reinicia el servidor, abre ambas páginas. Mueve page1. ¿Se actualiza la visualización en page2? ¿Por qué sí o por qué no? (Pista: ¿A quién le envía el mensaje socket.emit?). Restaura el código a broadcast.emit.


Los cambios solo se reciben en la misma pestaña y la otra pestaña no se actualiza.


Detén el servidor.

Cambia const port = 3000; a const port = 3001;.

Inicia el servidor. ¿Qué mensaje ves en la consola? ¿En qué puerto dice que está escuchando?


El servidor mostro  http://localhost:3001

Intenta abrir http://localhost:3000/page1. ¿Funciona?


No funciono.



Intenta abrir http://localhost:3001/page1. ¿Funciona?


Si funciona



¿Qué aprendiste sobre la variable port y la función listen? Restaura el puerto a 3000.


Si el puerto cambia tambien cambia la direccion que debo usar en el navegador.

