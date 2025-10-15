
# Evidencias de la unidad 7

## Actividad 01 

¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?


La que obtuve fue https://3c2w808t-3000.use2.devtunnels.ms/ y es necesaria ya que el celular no puede acceder directamente a localhost ni la IP de mi PC cuando estan en redes diferentes. Dev Tunnels crea un enlace que es publico que lo redirige al servidor local.


Describe brevemente qué hace npm install y npm start.


npm install es que descarga las dependencias del proyecto 


npm start ejecuta el servidor Node.js que conecta el celular y el PC


¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?


Server is listening on http://localhost:3000


New client connected


Received message => { type: 'touch', x: 145.09091186523438, y: 266.9090881347656 }


Received message => { type: 'touch', x: 153.8181915283203, y: 258.9090881347656 }


Client disconnected

Los mensajes fueron iguales en ambos clientes solo cambian los datos que enviaba el celular.


Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?




Si funciono correctamente, cuando movia el circulo rojo en el celular se movia en la pantalla del PC y si hubo un cierto retraso pero fue leve.



## Actividad 02



Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?


Es  necesario por que permite que un dispositivo externo en este caso el celular acceda a un servidor que esta funcionando en mi PC. Y funciona creando un tunel seguro entre una URL publica y el puerto local del servidor, enviando la informacion en ambos.


Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.


La funcion es que se ejecuta cuando la persona toca y mueve el dedo sobre la pantalla del celular. La variable threshold es la que ayuda a que evite enviar demasiados mensajes si el movimiento es muy minimo ayudando al rendimiento.



Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?


Usar la IP local solo funcionaria si los dos dispositivos estan en la misma red y puede fallar por bloqueos de router o firewall. Dev Tunnels permite la conexion desde cualquier lugar con internet.



Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal)


<img width="1913" height="1008" alt="Captura de pantalla 2025-10-15 172101" src="https://github.com/user-attachments/assets/b5c26e8e-bea0-4b57-ab46-c40e134b53cd" />





## Actividad 03



¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?


express.static(‘public’) sirve para compartir todos los archivos dentro de la carperta public sin necesidad de dar rutas manualmente. en cambio con app.get(‘/ruta’, …) se debe especificar cada ruta una por una.



Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?

El celular detecta el toque en touchMoved().


Envia las coordenadas al servidor mediante socket.emit('message', data).


El servidor recibe ese mensaje en socket.on('message').


Luego usa socket.broadcast.emit('message', message) para reenviarlo a los demás clientes conectados (como el escritorio).


El cliente de escritorio recibe el mensaje y actualiza la posición del circulo.
Se usa broadcast.emit para que el servidor envie el mensaje a todos excepto al que lo genero.


Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?


Los dos computadores recibirian el mensaje ya que el servidor lo reenvia a todos los clientes excepto alq ue lo envia que en este caso es el celular.


¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?


Permite ver cuando se conectan o desconectan clientes, ademas de verificar los datos que se envian .


## Actividad 04


Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.


<img width="1156" height="645" alt="Captura de pantalla 2025-10-15 175410" src="https://github.com/user-attachments/assets/c2868936-862e-4f49-b6f9-1a3da793ce42" />
