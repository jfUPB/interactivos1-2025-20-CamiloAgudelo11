
# Evidencias de la unidad 6


## Autoevaluacion 

Actividad 01: 5.0


Debido a que realice y comprendi la actividad propuesta ademas respondi de manera un tanto breve pero contundente a las preguntas formuladas.


Actividad 02: 4.2

Aunque respondi todas las preguntas en algunas me quede en lo superficial y no fui a mas investigacion, sin embargo conteste cada una de las preguntas.

Actividad 03: 4.0

Debido a que me enfoque mas en los experimentos no logre plasmar en mi bitacora cada una de las acciones o cosas que vi mientras los realizaba, pero de igual manera logre hacer cada experimento contestando cada pregunta.


Actividad 04: 4.2

Sucede lo mismo que en la actividad 03 me enfoque mas en la hora de hacer experimentos, pero en este caso si logre plasmar un poco mas, ademas de poner alguna parte de codigo para verificar lo que estoy realizando.

Actividad 05: 5.0

Realice toda la actividad propuesta, donde hice un nuevo programa utilizando el caso de estudio que es innovador y diferente al que ya tenia.

## Nota:4.4


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



## Acividad 04


Abre page2.html en tu navegador (con el servidor corriendo).

Abre la consola de desarrollador (F12).

Detén el servidor Node.js (Ctrl+C).

Refresca la página page2.html. Observa la consola del navegador. ¿Ves algún error relacionado con la conexión? ¿Qué indica?


En la consola aparecio un error de conexion WebSocket conection failed 



Vuelve a iniciar el servidor y refresca la página. ¿Desaparecen los errores?


Cuando volvi a iniciar el servidor y los errores desaparecieron lo que quiere dercir es que los clientes dependen de que el servidor este iniciado.


Comenta la línea socket.emit(‘win2update’, currentPageData, socket.id); dentro del listener connect.

Reinicia el servidor y refresca page1.html y page2.html.

Mueve la ventana de page2 un poco para que envíe una actualización.

¿Qué pasó? ¿Por qué?

Lo que pso es que page1 no recibio actualizaciones ya que no se emite una actualizacion el servidor no envia nada a los otros clientes.



Abre ambas páginas (es posible que ya las tengas abiertas).

Mueve la ventana de page1. Observa la consola del navegador de page2. ¿Qué datos muestra?


En la consola de page2 aparecieron los datos enviados.



Mueve la ventana de page2. Observa la consola de page1. ¿Qué pasa? ¿Por qué?


Pasa lo mismo que cuando movi la page1 que aparecen los datos en la otra ventana, ya que cada cliente recibe los datos de la posicion del otro ya que los datos se reenvian por el servidor 


Observa checkWindowPosition() en page2.js y modifica el código del if para comprobar si el código dentreo de este se ejecuta.
Mueve cada ventana y observa las consolas.
¿Qué puedes concluir y por qué?


En la consola se mostro que si entraba al if. Lo que se puede concluir es que checkWindowPosition() controla cuando envia actualizaciones, lo que evita enviar datos innecesarios.



Cambia el background(220) para que dependa de la distancia entre las ventanas. Puedes calcular la magnitud del resultingVector usando let distancia = resultingVector.mag(); y luego usa map() para convertir esa distancia a un valor de gris o color. background(map(distancia, 0, 1000, 255, 0)); (ajusta el rango 0-1000 según sea necesario).

Inventa otra modificación creativa.

''
js
let distancia = resultingVector.mag();

background(map(distancia, 0, 1000, 255, 0));

let tamano = map(distancia, 0, 1000, 20, 200); 
ellipse(width / 2, height / 2, tamano, tamano);
''


Hice que el tamaño de un  circulo en pantala dependa de la distancia.



## Actividad 05

Explica tu idea y realiza algunos bocetos.


La idea es crear tipo chat sencillo de emojis donde en una pagina se utilicen botones para enviarle emojis a la otra pagina. Mientras que la otra pagina los envie con las teclas a la otra pagina.


Implementa tu idea.
Incluye todos los códigos (servidor y clientes) en tu bitácora.


server.js
```js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');
const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

let page1 = { x: 0, y: 0, width: 100, height: 100 };
let page2 = { x: 0, y: 0, width: 100, height: 100 };
let connectedClients = new Map();
let syncedClients = new Set();

app.use(express.static(path.join(__dirname, 'views')));

app.get('/page1', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});

app.get('/page2', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page2.html'));
});

io.on('connection', (socket) => {
    console.log('A user connected - ID:', socket.id);
    connectedClients.set(socket.id, { page: null, synced: false });
    
    socket.on('disconnect', () => {
        console.log('User disconnected - ID:', socket.id);
        connectedClients.delete(socket.id);
        syncedClients.delete(socket.id);
        socket.broadcast.emit('peerDisconnected');
    });

    socket.on('win1update', (window1, sendid) => {
        console.log('Received win1update from ID:', socket.id, 'Data:', window1);
        if (isValidWindowData(window1)) {
            page1 = window1;
            connectedClients.set(socket.id, { page: 'page1', synced: false });
            socket.broadcast.emit('getdata', { data: page1, from: 'page1' });
            checkAndNotifySyncStatus();
        }
    });

    socket.on('win2update', (window2, sendid) => {
        console.log('Received win2update from ID:', socket.id, 'Data:', window2);
        if (isValidWindowData(window2)) {
            page2 = window2;
            connectedClients.set(socket.id, { page: 'page2', synced: false });
            socket.broadcast.emit('getdata', { data: page2, from: 'page2' });
            checkAndNotifySyncStatus();
        }
    });

    socket.on('requestSync', () => {
        const clientInfo = connectedClients.get(socket.id);
        if (clientInfo?.page === 'page1') {
            socket.emit('getdata', { data: page2, from: 'page2' });
        } else if (clientInfo?.page === 'page2') {
            socket.emit('getdata', { data: page1, from: 'page1' });
        }
    });

    socket.on('confirmSync', () => {
        syncedClients.add(socket.id);
        const clientInfo = connectedClients.get(socket.id);
        if (clientInfo) {
            connectedClients.set(socket.id, { ...clientInfo, synced: true });
        }
        checkAndNotifySyncStatus();
    });    

    
    socket.on("message", (emoji) => {
        console.log("Emoji recibido:", emoji);
        // Reenviar a todos los demás clientes
        socket.broadcast.emit("message", emoji);
    });
});

function isValidWindowData(data) {
    return data && 
           typeof data.x === 'number' && 
           typeof data.y === 'number' && 
           typeof data.width === 'number' && data.width > 0 &&
           typeof data.height === 'number' && data.height > 0;
}

function checkAndNotifySyncStatus() {
    const page1Clients = Array.from(connectedClients.entries()).filter(([id, info]) => info.page === 'page1');
    const page2Clients = Array.from(connectedClients.entries()).filter(([id, info]) => info.page === 'page2');
    
    const bothPagesConnected = page1Clients.length > 0 && page2Clients.length > 0;
    const allClientsSynced = Array.from(connectedClients.keys()).every(id => syncedClients.has(id));
    const hasMinimumClients = connectedClients.size >= 2;

    console.log(`Debug - Connected clients: ${connectedClients.size}, Page1: ${page1Clients.length}, Page2: ${page2Clients.length}, Synced: ${syncedClients.size}`);

    if (bothPagesConnected && allClientsSynced && hasMinimumClients) {
        io.emit('fullySynced', true);
        console.log('All clients are fully synced');
    } else {
        io.emit('fullySynced', false);
        console.log(`Sync status: pages=${bothPagesConnected}, synced=${allClientsSynced}, clients=${connectedClients.size}`);
    }
}

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});

```


page1.html 

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Emoji Chat 1</title>
  <style>
    body { font-family: Arial; text-align: center; }
    #messages { font-size: 2rem; margin-top: 20px; }
    button { font-size: 2rem; margin: 10px; cursor: pointer; }
  </style>
</head>
<body>
  <h2>Emoji Chat (User 1)</h2>
  <button onclick="sendEmoji('😀')">😀</button>
  <button onclick="sendEmoji('❤️')">❤️</button>
  <button onclick="sendEmoji('🔥')">🔥</button>
  <button onclick="sendEmoji('👀')">👀</button>
  <button onclick="sendEmoji('🎶')">🎶</button>

  <div id="messages"></div>

 
  <script src="/socket.io/socket.io.js"></script>
 
  <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>


  <script src="page1.js"></script>
</body>
</html>
```


page1.js

```js
(function () {
  let socket = null;

  function addEmoji(emoji) {
    const messagesDiv = document.getElementById("messages");
    if (!messagesDiv) {
      console.error("No se encontró #messages en el DOM");
      return;
    }
    const span = document.createElement("span");
    span.textContent = emoji;
    span.style.margin = "0 8px";
    messagesDiv.appendChild(span);
  }

  function initSocket() {
    try {
      if (typeof io !== "function") {
        console.error("io() no está disponible (socket.io cliente no cargado)");
        return;
      }
      socket = io();

      socket.on("connect", () => {
        console.log("page1: socket conectado, id =", socket.id);
      });
      socket.on("disconnect", () => {
        console.log("page1: socket desconectado");
      });

      socket.on("message", (emoji) => {
        console.log("page1: mensaje recibido desde server:", emoji);
        addEmoji(emoji);
      });
    } catch (err) {
      console.error("page1: error inicializando socket:", err);
      socket = null;
    }
  }


  window.sendEmoji = function (emoji) {
 
    addEmoji(emoji);

    if (socket && socket.connected) {
      console.log("page1: enviando emoji al servidor:", emoji);
      socket.emit("message", emoji);
    } else {
      console.warn("page1: socket no conectado — no se pudo enviar al servidor");
    }
  };

 
  window.addEventListener("load", () => {
    console.log("page1: DOM cargado — intentando inicializar socket...");
    initSocket();
  });
})();
```

page2.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page 2 - Chat Emojis</title>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
  <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
 
  <script src="page2.js"></script>
</body>
</html>
```


page2.js

``` js
let socket;
let emojis = ["😀", "😂", "😍", "😎", "😡", "👍", "👎", "🔥", "🎉", "💀"];
let messages = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  textSize(64);
  textAlign(CENTER, CENTER);

  socket = io();

  socket.on("message", (msg) => {
    messages.push(msg);
    if (messages.length > 10) messages.shift();
  });
}

function draw() {
  background(220);

  for (let i = 0; i < messages.length; i++) {
    text(messages[i], width / 2, 100 + i * 70);
  }

  fill(0);
  textSize(24);
  text("Presiona teclas 1-0 para enviar emojis", width / 2, height - 50);
}

function keyPressed() {
  let index;
  if (key >= '0' && key <= '9') {
    index = int(key) - 1;
    if (index === -1) index = 9; // si presiona 0 → último emoji
    if (index >= 0 && index < emojis.length) {
      let chosen = emojis[index];
      socket.emit("message", chosen);

      
      messages.push(chosen);
      if (messages.length > 10) messages.shift();
    }
  }
}


```
