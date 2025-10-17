
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



## Actividad 05


Diseña una aplicación interactiva que use el touch del móvil para controlar una visuales de tema musical de tu elección. Las visuales correrán en una aplicación 




<img width="1407" height="785" alt="Captura de pantalla 2025-10-16 112757" src="https://github.com/user-attachments/assets/c145a73a-d5e3-4f4c-ad78-bcd326c4dc3f" />







<img width="661" height="775" alt="Captura de pantalla 2025-10-16 112823" src="https://github.com/user-attachments/assets/a79296d6-6ea2-42f8-a400-0ee308e27f03" />



de escritorio (desktop). Recuerda que ambas aplicaciones las construirás usando p5.js y utilizando el servidor Node.js como puente.
Implementa tu diseño. Puedes usar IA generativa para ayudarte a escribir el código, pero primero debes hacer el diseño de lo que quieres.
Incluye todos los códigos (servidor y clientes) en tu bitácora.




Codigo servidor 

```

import express from "express";
import { createServer } from "http";
import { Server } from "socket.io";
import path from "path";
import { fileURLToPath } from "url";


const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

const app = express();
const server = createServer(app);


const io = new Server(server, {
  cors: {
    origin: "*",
    methods: ["GET", "POST"]
  }
});


app.use(express.static(path.join(__dirname, "public")));


app.get("/desktop", (req, res) => {
  res.sendFile(path.join(__dirname, "public/desktop/index.html"));
});

app.get("/mobile", (req, res) => {
  res.sendFile(path.join(__dirname, "public/mobile/index.html"));
});


io.on("connection", (socket) => {
  console.log("✅ Cliente conectado:", socket.id);

  socket.on("newElement", (data) => {
    console.log("📲 Elemento recibido del móvil:", data);
    io.emit("newElement", data);
  });
});

// Puerto del servidor
const PORT = 3000;
server.listen(PORT, () => {
  console.log(`Servidor en: http://localhost:${PORT}`);
});

```


Codigo Desktop HTML


```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Librerías p5 -->
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/addons/p5.sound.min.js"></script>

  <!-- Socket.IO desde CDN (importante, evita problemas de túnel) -->
  <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>

  <!-- Tu script principal -->
  <script src="sketch.js" defer></script>

  <title>Desktop p5.js Application</title>
</head>
<body style="margin: 0; overflow: hidden; background: #000;"></body>
</html>
```

Codigo Desktop js

```
let fft;
let socket;
let waveHeight = 50;
let elements = [];
let started = false; // <- controla el inicio manual de la música

function preload() {
  song = loadSound('zell.mp3');
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  fft = new p5.FFT();

  // 🔹 Conéctate al mismo túnel que usas en el celular:
  // (copia exactamente el enlace público del puerto 3000)
 socket = io.connect("https://3c2w808t-3000.use2.devtunnels.ms");


  // 🔹 Escucha cuando el móvil envíe un nuevo elemento
  socket.on("newElement", (data) => {
    console.log("Elemento recibido del móvil:", data);
    elements.push({
      type: data,
      x: random(width),
      y: random(height / 2, height - 100)
    });
  });

  textAlign(CENTER);
  textSize(24);
  fill(255);
  text("Toca para iniciar la música", width / 2, height / 2);
}

function mousePressed() {
  if (!started) {
    song.loop();
    started = true;
  }
}

function draw() {
  background(0, 50, 100);

  if (!started) return; // no dibujar hasta que empiece la música

  let spectrum = fft.analyze();
  let energy = fft.getEnergy("bass");
  let waveAmplitude = map(energy, 0, 255, 20, 150);

  noFill();
  stroke(255);
  strokeWeight(3);

  beginShape();
  for (let x = 0; x <= width; x += 20) {
    let y = height / 2 + sin(x * 0.02 + frameCount * 0.05) * waveAmplitude;
    vertex(x, y);
  }
  endShape();

  for (let e of elements) {
    drawElement(e);
  }
}

function drawElement(e) {
  textAlign(CENTER);
  textSize(30);
  noStroke();

  switch (e.type) {
    case "burbuja": fill(173, 216, 230); ellipse(e.x, e.y, 30); break;
    case "cara": fill(255, 255, 0); text("😊", e.x, e.y); break;
    case "estrella": fill(255, 255, 0); text("⭐", e.x, e.y); break;
    case "wup": fill(255); text("WUP", e.x, e.y); break;
    case "wp": fill(255); text("WP", e.x, e.y); break;
    case "gota": fill(0, 150, 255); text("💧", e.x, e.y); break;
  }
}

```


Codigo mobile HTML

```

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />

  <!-- Librerías p5 -->
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>

  <!-- Socket.IO desde CDN -->
  <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>

  <!-- Tu script principal -->
  <script src="sketch.js" defer></script>

  <title>Mobile Controller</title>
</head>
<body style="margin: 0; overflow: hidden; background: #111;"></body>
</html>
```

Codigo mobile js

```

let socket;

function setup() {
  createCanvas(windowWidth, windowHeight);
  socket = io.connect("https://3c2w808t-3000.use2.devtunnels.ms");

}

function draw() {
  background(30);
  fill(255);
  textAlign(CENTER);
  textSize(24);
  text("Presiona un botón para enviar", width / 2, 50);

  // Botones
  drawButton("burbuja", width / 2 - 100, height / 3);
  drawButton("cara", width / 2 + 100, height / 3);
  drawButton("estrella", width / 2 - 100, height / 2);
  drawButton("wup", width / 2 + 100, height / 2);
  drawButton("wp", width / 2 - 100, height * 0.7);
  drawButton("gota", width / 2 + 100, height * 0.7);
}

function drawButton(label, x, y) {
  fill(100, 150, 255);
  ellipse(x, y, 100);
  fill(255);
  textSize(20);
  text(label, x, y + 5);
}

function mousePressed() {
  let labels = ["burbuja", "cara", "estrella", "wup", "wp", "gota"];
  for (let i = 0; i < labels.length; i++) {
    let x = width / 2 + ((i % 2 === 0) ? -100 : 100);
    let y = [height / 3, height / 3, height / 2, height / 2, height * 0.7, height * 0.7][i];
    if (dist(mouseX, mouseY, x, y) < 50) {
      socket.emit("newElement", labels[i]);
    }
  }
}

```

Cancion usada: https://youtu.be/fo773EQdFC4?si=dQ4HA92pYCBC-YHE
