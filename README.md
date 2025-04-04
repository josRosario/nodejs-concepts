# nodejs-concepts


## ¿Qué es Node.js?

Node.js es un entorno de ejecución para JavaScript en el lado del servidor basado en el motor V8 de Google Chrome.

## ¿Qué es el Event Loop en Node.js?

El **Event Loop** en Node.js es el mecanismo que permite manejar múltiples operaciones simultáneamente en un solo hilo, utilizando un modelo de programación asincrónico y no bloqueante. Es el núcleo de cómo Node.js gestiona las operaciones de entrada/salida (I/O) de manera eficiente.

### ¿Cómo funciona?
1. **Operaciones bloqueantes** como leer archivos, acceder a bases de datos o realizar solicitudes HTTP se delegan a hilos del sistema o APIs externas.
2. Mientras tanto, el **Event Loop** sigue ejecutando otras tareas en el hilo principal.
3. Cuando una operación asincrónica se completa, el Event Loop coloca su callback en la cola de tareas para ser ejecutado.

### Fases del Event Loop:
1. **Timers**: Ejecuta callbacks de funciones como `setTimeout` y `setInterval` cuyo tiempo ha expirado.
2. **I/O Callbacks**: Procesa callbacks de operaciones I/O (como lectura de archivos).
3. **Idle, Prepare**: Interno, usado por Node.js.
4. **Poll**: Recupera nuevas I/O y ejecuta callbacks relacionados.
5. **Check**: Ejecuta callbacks de `setImmediate`.
6. **Close Callbacks**: Maneja eventos de cierre, como `socket.on('close')`.

### Ejemplo:
```js
console.log('Inicio');

setTimeout(() => {
  console.log('Timeout');
}, 0);

setImmediate(() => {
  console.log('Immediate');
});

console.log('Fin');
```

**Salida:**
```
Inicio
Fin
Immediate
Timeout
```

Esto ocurre porque `setImmediate` se ejecuta antes que `setTimeout` si ambos se programan en el mismo ciclo del Event Loop.

## ¿Qué es un Callback en Node.js?

Un callback es una función que se pasa como argumento a otra función y se ejecuta cuando esa función termina de ejecutarse.

```js

function saludo(nombre, callback) {
  console.log(`Hola ${nombre}`);
  callback();
}

saludo('Juan', () => console.log('¡Saludos completados!'));

```

# import y require 



### 1. **`require`**:
   - Forma parte del sistema de módulos **CommonJS**.
   - Es la forma tradicional de importar módulos en Node.js.
   - Se utiliza con la función `require()`.

   **Ejemplo**:
   ```js
   const fs = require('fs'); // Importa el módulo 'fs'
   const miModulo = require('./miModulo'); // Importa un archivo local
   ```

   **Características**:
   - Es síncrono: carga el módulo en el momento en que se llama.
   - Compatible con todas las versiones de Node.js.
   - No requiere configuración adicional.

---

### 2. **`import`**:
   - Forma parte del sistema de módulos **ESM (ECMAScript Modules)**.
   - Es la forma moderna de importar módulos en JavaScript.
   - Se utiliza con la palabra clave `import`.

   **Ejemplo**:
   ```js
   import fs from 'fs'; // Importa el módulo 'fs'
   import miModulo from './miModulo.js'; // Importa un archivo local
   ```

   **Características**:
   - Es asíncrono: los módulos se cargan de manera diferida.
   - Requiere que el archivo tenga la extensión `.mjs` o que el campo `"type": "module"` esté definido en el archivo `package.json`.
   - Compatible con ES6 y versiones modernas de Node.js (a partir de la versión 12 con soporte completo en la versión 14).

---

### Diferencias clave:

| Característica       | `require` (CommonJS)         | `import` (ESM)              |
|----------------------|------------------------------|-----------------------------|
| **Sistema de módulos** | CommonJS                   | ECMAScript Modules (ESM)    |
| **Sincronía**         | Síncrono                   | Asíncrono                   |
| **Soporte**           | Todas las versiones de Node.js | Node.js 12+ (estable en 14) |
| **Extensión**         | `.js`                      | `.mjs` o `"type": "module"` |
| **Uso dinámico**      | Permitido                  | Limitado (usa `import()` dinámico) |

---

### ¿Cuándo usar cada uno?
- Usa **`require`** si trabajas en un proyecto existente o necesitas compatibilidad con versiones antiguas de Node.js.
- Usa **`import`** si estás trabajando en un proyecto moderno y quieres aprovechar las características de ES6+.

---

### Ejemplo combinado:
Si necesitas usar `import` en un proyecto basado en CommonJS, puedes habilitarlo con `import()` dinámico:

```js
(async () => {
  const miModulo = await import('./miModulo.js');
  console.log(miModulo);
})();
```


## módulo 

En Node.js, un módulo es un archivo que contiene código JavaScript que se puede reutilizar en otros archivos. Los módulos permiten dividir una aplicación en partes pequeñas y organizadas, facilitando el mantenimiento y la reutilización del código.

## Tipos de módulos en Node.js
- Módulos nativos: Son los que vienen incorporados con Node.js (como fs, http, path, etc.).

- Módulos de terceros: Son paquetes instalados desde npm (como express, lodash, etc.).

- Módulos propios: Son archivos creados por ti mismo dentro de tu proyecto.


## stream
Un Stream (flujo) es una abstracción que permite trabajar con datos que se transmiten en partes pequeñas (chunks), en lugar de cargarlos todos en memoria de una sola vez. Esto es especialmente útil para trabajar con archivos grandes, redes, o cualquier tipo de entrada/salida.

## 🚀 ¿Por qué usar Streams?
- Mejor rendimiento (procesa datos a medida que llegan).
- Menor uso de memoria.
- Ideal para lectura/escritura de archivos grandes, transmisión de video/audio, etc.

## 🔄 Tipos de Streams en Node.js
- Readable Streams (Lectura)
Te permiten leer datos pieza por pieza.
Ejemplo: leyendo un archivo o recibiendo datos de una petición HTTP.

- Writable Streams (Escritura)
Te permiten escribir datos en una fuente destino.
Ejemplo: escribir en un archivo o enviar una respuesta HTTP.

- Duplex Streams (Lectura y Escritura)
Permiten leer y escribir datos al mismo tiempo.
Ejemplo: un socket TCP.

- Transform Streams (Transformación)
Son duplex streams que modifican los datos en el camino.
Ejemplo: comprimir un archivo, convertir texto a mayúsculas, etc.

```js
const fs = require('fs');

// Leer desde un archivo
const readableStream = fs.createReadStream('entrada.txt');

// Escribir en otro archivo
const writableStream = fs.createWriteStream('salida.txt');

// Pasa los datos de lectura directamente a escritura
readableStream.pipe(writableStream);

```

## 🔧 Eventos comunes en Streams
- 'data': cuando se recibe un chunk de datos.

- 'end': cuando ya no hay más datos que leer.

- 'error': si ocurre algún error.

- 'finish': cuando se termina de escribir.

## cluster
Un cluster es un módulo que permite crear múltiples procesos hijos (workers) que se ejecutan simultáneamente y comparten el mismo servidor (puerto). Esto es útil porque Node.js corre en un solo hilo (single-threaded), y con clusters puedes aprovechar múltiples núcleos de CPU para mejorar el rendimiento.

## 💡 ¿Para qué sirve cluster?
Node.js por defecto no puede usar más de un núcleo de CPU. Con cluster, puedes crear varios procesos que corren el mismo código y balancean la carga entre ellos. Esto mejora la escalabilidad de una app, especialmente si es un servidor HTTP.


## 🧠 Cómo funciona
- El proceso principal (master) crea varios procesos worker.

- Todos los workers comparten el mismo puerto.

- Cuando llega una petición, Node.js distribuye la carga entre los workers.

```js
const cluster = require('cluster');
const http = require('http');
const os = require('os');

const numCPUs = os.cpus().length;

if (cluster.isMaster) {
  console.log(`Master PID: ${process.pid}`);

  // Crear un worker por cada núcleo
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  // Cuando un worker muere, se crea uno nuevo
  cluster.on('exit', (worker, code, signal) => {
    console.log(`Worker ${worker.process.pid} murió. Creando uno nuevo...`);
    cluster.fork();
  });

} else {
  // Código que ejecutará cada worker
  http.createServer((req, res) => {
    res.writeHead(200);
    res.end(`Hola desde el worker ${process.pid}\n`);
  }).listen(3000);

  console.log(`Worker ${process.pid} iniciado`);
}

```


## ✅ Beneficios
- Aprovecha todos los núcleos de CPU.

- Mejora la concurrencia en apps de alto tráfico.

- Aísla errores: si un worker falla, no tumba toda la app.


## Buffer 
un Buffer es una estructura de datos que permite manejar directamente datos binarios en memoria sin necesidad de convertirlos a strings.

Se usa principalmente cuando se trabaja con:

- Archivos

- Streams

- Redes (sockets)

- Criptografía


## 🧠 ¿Por qué existe Buffer?
Porque JavaScript no tiene soporte nativo para manipular datos binarios. Node.js lo necesita para operaciones de bajo nivel como leer archivos, datos de red, etc.

## 📦 ¿Qué es exactamente un Buffer?
Es como un array de bytes (valores entre 0 y 255), pero más eficiente para tareas de entrada/salida.


## 🛠️ Crear un Buffer
```js
// Desde un string
const buf = Buffer.from('Hola');
console.log(buf); // <Buffer 48 6f 6c 61>

// Desde un array de bytes
const buf2 = Buffer.from([72, 111, 108, 97]);
console.log(buf2.toString()); // 'Hola'

// Buffer vacío de 10 bytes
const buf3 = Buffer.alloc(10);
```

## 🧪 Métodos útiles de Buffer
```js
const buf = Buffer.from('Node.js');

// Acceder a bytes
console.log(buf[0]); // 78 (código ASCII de 'N')

// Convertir a string
console.log(buf.toString()); // 'Node.js'

// Escribir en buffer
buf.write('Hola');
console.log(buf.toString()); // 'Hola.js'

```
## ⚠️ Notas importantes
- Buffers son de tamaño fijo.

- Muy usados internamente por Streams.

- Puedes trabajar con diferentes codificaciones: 'utf8', 'ascii', 'base64', 'hex', etc.


 ## ¿Qué es process en Node.js?
 process es un objeto global que proporciona información sobre el proceso de Node.js en ejecución, como las variables de entorno.

```js
console.log(process.env.PATH);  // Muestra las variables de entorno del sistema.
```

## . ¿Qué es setTimeout() en Node.js?
setTimeout() es una función que ejecuta un código después de un retraso especificado.

```js
setTimeout(() => {
  console.log('Este mensaje aparece después de 2 segundos');
}, 2000);
```

## ¿Qué es setInterval() en Node.js?
setInterval() ejecuta una función de manera repetitiva con un intervalo de tiempo determinado.

```js
setInterval(() => {
  console.log('Este mensaje aparece cada 1 segundo');
}, 1000);
```
## ¿Qué es clearInterval() en Node.js?
clearInterval() detiene la ejecución repetitiva de setInterval().

```js
const id = setInterval(() => {
  console.log('Cada segundo');
}, 1000);

setTimeout(() => {
  clearInterval(id);  // Detiene el intervalo después de 5 segundos
}, 5000);
```

## http

El módulo **`http`** en Node.js es un módulo nativo que permite crear servidores HTTP y manejar solicitudes y respuestas. Es fundamental para construir aplicaciones web y APIs en Node.js sin necesidad de frameworks adicionales.

---

### Características principales:
1. **Crear servidores HTTP**: Permite crear un servidor que escuche solicitudes en un puerto específico.
2. **Manejar solicitudes y respuestas**: Proporciona objetos `req` (request) y `res` (response) para interactuar con las solicitudes y enviar respuestas.
3. **Soporte para métodos HTTP**: Maneja métodos como `GET`, `POST`, `PUT`, `DELETE`, etc.
4. **Ligero y eficiente**: Diseñado para aplicaciones de alto rendimiento.

---

### Ejemplo básico de un servidor HTTP:

```js
const http = require('http');

// Crear un servidor
const server = http.createServer((req, res) => {
  // Configurar la respuesta
  res.statusCode = 200; // Código de estado HTTP
  res.setHeader('Content-Type', 'text/plain'); // Tipo de contenido
  res.end('¡Hola, mundo!'); // Respuesta al cliente
});

// Escuchar en el puerto 3000
server.listen(3000, () => {
  console.log('Servidor ejecutándose en http://localhost:3000');
});
```

---

### Explicación del código:
1. **`http.createServer()`**:
   - Crea un servidor HTTP.
   - Recibe un callback con los objetos `req` (solicitud) y `res` (respuesta).

2. **`res.statusCode`**:
   - Define el código de estado HTTP de la respuesta (por ejemplo, `200` para éxito).

3. **`res.setHeader()`**:
   - Configura los encabezados HTTP de la respuesta (por ejemplo, `Content-Type`).

4. **`res.end()`**:
   - Finaliza la respuesta y envía datos al cliente.

5. **`server.listen()`**:
   - Hace que el servidor escuche en un puerto específico (en este caso, el puerto `3000`).

---

### Ejemplo avanzado con rutas:

```js
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.url === '/' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end('<h1>Bienvenido a la página principal</h1>');
  } else if (req.url === '/api' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ mensaje: 'Hola desde la API' }));
  } else {
    res.writeHead(404, { 'Content-Type': 'text/plain' });
    res.end('Página no encontrada');
  }
});

server.listen(3000, () => {
  console.log('Servidor ejecutándose en http://localhost:3000');
});
```

---

### Ventajas del módulo `http`:
- **Ligero**: No requiere dependencias externas.
- **Control total**: Permite manejar solicitudes y respuestas de manera personalizada.
- **Integración con otros módulos**: Se puede combinar con módulos como `fs` para servir archivos.

---

### Limitaciones:
- **Código más complejo**: Para aplicaciones grandes, manejar rutas y lógica puede volverse complicado.
- **No incluye middleware**: A diferencia de frameworks como Express, no tiene soporte integrado para middleware.

---

### Uso en combinación con frameworks:
Aunque el módulo `http` es poderoso, frameworks como **Express** se construyen sobre él para simplificar el desarrollo de aplicaciones web. Por ejemplo:

```js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('¡Hola, mundo con Express!');
});

app.listen(3000, () => {
  console.log('Servidor ejecutándose en http://localhost:3000');
});
```

El módulo `http` sigue siendo la base de cualquier servidor en Node.js, incluso cuando se usan frameworks.


## process.nextTick()

es un método que permite ejecutar una función de callback inmediatamente después de que el Event Loop termine la fase actual, antes de que continúe con las siguientes fases. Es útil para priorizar la ejecución de ciertas tareas asincrónicas.

---

### Características principales:
1. **Prioridad alta**: Las funciones pasadas a `process.nextTick()` se ejecutan antes de cualquier tarea en la cola de eventos (como `setTimeout` o `setImmediate`).
2. **No bloquea el Event Loop**: Se ejecuta después de la operación actual, pero antes de que el Event Loop procese otras tareas pendientes.
3. **Uso común**: Se utiliza para manejar errores, inicializar datos o dividir operaciones largas en partes más pequeñas.

---

### Ejemplo básico:

```js
console.log('Inicio');

process.nextTick(() => {
  console.log('Callback de nextTick');
});

console.log('Fin');
```

**Salida**:
```
Inicio
Fin
Callback de nextTick
```

---

### Comparación con `setImmediate`:
- **`process.nextTick()`**: Se ejecuta antes de que el Event Loop pase a la siguiente fase.
- **`setImmediate()`**: Se ejecuta al final de la fase de I/O del Event Loop.

```js
setImmediate(() => {
  console.log('setImmediate');
});

process.nextTick(() => {
  console.log('nextTick');
});

console.log('Fin');
```

**Salida**:
```
Fin
nextTick
setImmediate
```

---

### Uso práctico:
#### 1. **Manejo de errores antes de continuar**:
```js
function ejemplo() {
  process.nextTick(() => {
    console.log('Esto se ejecuta antes de continuar');
  });
  console.log('Operación actual');
}

ejemplo();
```

---

#### 2. **Evitar bloqueos en operaciones largas**:
Si tienes una operación que podría bloquear el Event Loop, puedes dividirla en partes más pequeñas usando `process.nextTick()`.

```js
function operacionLarga() {
  if (contador < 5) {
    console.log(`Iteración ${contador}`);
    contador++;
    process.nextTick(operacionLarga); // Divide la operación
  }
}

let contador = 0;
operacionLarga();
```

---

### Resumen:
- **`process.nextTick()`** es una herramienta poderosa para priorizar tareas asincrónicas.
- Se ejecuta antes de cualquier tarea en la cola de eventos.
- Útil para manejar errores, inicializar datos o dividir operaciones largas.

## Middleware
un middleware es una función que se ejecuta entre que una petición llega al servidor y antes de que se envíe la respuesta. Aunque Node.js como tal no tiene un sistema de middlewares integrado, Express.js (el framework más usado) sí lo utiliza ampliamente.

## 💡 ¿Qué hace un middleware?
- Puede modificar la request (req) y la response (res).

- Puede terminar el ciclo de la petición enviando una respuesta.

- O puede pasar el control al siguiente middleware usando next().

  ## 🧱 Sintaxis de un middleware en Express

```js
function miMiddleware(req, res, next) {
  console.log('Middleware ejecutado');
  next(); // pasa al siguiente middleware o ruta
}
app.use(miMiddleware);
```

## 🧪 Ejemplo práctico

```js
const express = require('express');
const app = express();

// Middleware global
app.use((req, res, next) => {
  console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
  next(); // continúa con la siguiente función
});

// Ruta
app.get('/', (req, res) => {
  res.send('Hola mundo!');
});

app.listen(3000, () => {
  console.log('Servidor corriendo en puerto 3000');
});
```

## 🧠 Tipos de middleware en Express
- Middleware de aplicación: afecta a toda la app (app.use()).

- Middleware de ruta: solo afecta rutas específicas.

- Middleware de terceros: como body-parser, cors, morgan, etc.

- Middleware de error: maneja errores ((err, req, res, next)).

## 🛠️ Ejemplo de middleware para validar un token

```js
function verificarToken(req, res, next) {
  const token = req.headers['authorization'];
  if (token === 'secreto123') {
    next();
  } else {
    res.status(401).send('No autorizado');
  }
}

app.get('/protegido', verificarToken, (req, res) => {
  res.send('Acceso concedido');
});
```

## fs
El módulo **`fs`** en Node.js es un módulo nativo que proporciona una API para interactuar con el sistema de archivos. Permite realizar operaciones como leer, escribir, actualizar, eliminar y manipular archivos y directorios.

---

### Características principales:
1. **Sincrónico y asincrónico**: Ofrece métodos tanto sincrónicos (bloqueantes) como asincrónicos (no bloqueantes).
2. **Manipulación de archivos**: Permite leer, escribir, copiar, renombrar y eliminar archivos.
3. **Manipulación de directorios**: Permite crear, leer y eliminar directorios.
4. **Streams**: Soporta operaciones de lectura y escritura en streams para manejar grandes volúmenes de datos.

---

### Ejemplo básico: Leer un archivo

```js
const fs = require('fs');

// Leer un archivo de forma asincrónica
fs.readFile('archivo.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error al leer el archivo:', err);
    return;
  }
  console.log('Contenido del archivo:', data);
});
```

---

### Métodos comunes del módulo `fs`:

#### 1. **`fs.readFile`**: Leer un archivo
```js
fs.readFile('archivo.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

#### 2. **`fs.writeFile`**: Escribir en un archivo
```js
fs.writeFile('archivo.txt', 'Hola, mundo!', (err) => {
  if (err) throw err;
  console.log('Archivo escrito con éxito');
});
```

#### 3. **`fs.appendFile`**: Agregar contenido a un archivo
```js
fs.appendFile('archivo.txt', '\nNueva línea', (err) => {
  if (err) throw err;
  console.log('Contenido agregado');
});
```

#### 4. **`fs.unlink`**: Eliminar un archivo
```js
fs.unlink('archivo.txt', (err) => {
  if (err) throw err;
  console.log('Archivo eliminado');
});
```

#### 5. **`fs.mkdir`**: Crear un directorio
```js
fs.mkdir('nueva_carpeta', (err) => {
  if (err) throw err;
  console.log('Directorio creado');
});
```

#### 6. **`fs.readdir`**: Leer el contenido de un directorio
```js
fs.readdir('.', (err, files) => {
  if (err) throw err;
  console.log('Archivos en el directorio:', files);
});
```

---

### Uso con Promesas:
Desde Node.js 10, puedes usar el módulo `fs.promises` para trabajar con promesas en lugar de callbacks.

```js
const fs = require('fs').promises;

async function leerArchivo() {
  try {
    const data = await fs.readFile('archivo.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error('Error al leer el archivo:', err);
  }
}

leerArchivo();
```

---

### Streams con `fs`:
El módulo `fs` también permite trabajar con streams para manejar grandes volúmenes de datos de manera eficiente.

#### Leer un archivo como stream:
```js
const readStream = fs.createReadStream('archivo_grande.txt', 'utf8');
readStream.on('data', (chunk) => {
  console.log('Chunk recibido:', chunk);
});
```

#### Escribir en un archivo como stream:
```js
const writeStream = fs.createWriteStream('archivo_salida.txt');
writeStream.write('Primera línea\n');
writeStream.end('Última línea');
```


## Event Emitter

En Node.js, un **EventEmitter** es una clase del módulo nativo **`events`** que permite manejar eventos personalizados. Es la base del sistema de eventos en Node.js y se utiliza para emitir y escuchar eventos en aplicaciones.

---

### Características principales:
1. **Emitir eventos**: Puedes emitir eventos personalizados con datos asociados.
2. **Escuchar eventos**: Puedes registrar funciones (listeners) que se ejecuten cuando se emita un evento.
3. **Herencia**: Muchas clases en Node.js, como `http.Server` o `fs.ReadStream`, heredan de `EventEmitter`.

---

### Ejemplo básico:

```js
const EventEmitter = require('events');

// Crear una instancia de EventEmitter
const emisor = new EventEmitter();

// Registrar un listener para el evento 'saludo'
emisor.on('saludo', (nombre) => {
  console.log(`¡Hola, ${nombre}!`);
});

// Emitir el evento 'saludo'
emisor.emit('saludo', 'Juan');
```

**Salida**:
```
¡Hola, Juan!
```

---

### Métodos principales de `EventEmitter`:

1. **`on(event, listener)`**:
   - Registra un listener para un evento.
   ```js
   emisor.on('evento', () => console.log('Evento recibido'));
   ```

2. **`emit(event, [args])`**:
   - Emite un evento, ejecutando todos los listeners registrados.
   ```js
   emisor.emit('evento', 'dato');
   ```

3. **`once(event, listener)`**:
   - Registra un listener que se ejecuta solo una vez.
   ```js
   emisor.once('evento', () => console.log('Evento recibido una vez'));
   ```

4. **`removeListener(event, listener)`**:
   - Elimina un listener específico para un evento.
   ```js
   const listener = () => console.log('Listener eliminado');
   emisor.on('evento', listener);
   emisor.removeListener('evento', listener);
   ```

5. **`removeAllListeners([event])`**:
   - Elimina todos los listeners de un evento o de todos los eventos.
   ```js
   emisor.removeAllListeners('evento');
   ```

---

### Ejemplo avanzado: Contador de eventos

```js
const EventEmitter = require('events');
const emisor = new EventEmitter();

let contador = 0;

// Listener para contar eventos
emisor.on('incrementar', () => {
  contador++;
  console.log(`Contador: ${contador}`);
});

// Emitir el evento varias veces
emisor.emit('incrementar');
emisor.emit('incrementar');
emisor.emit('incrementar');
```

**Salida**:
```
Contador: 1
Contador: 2
Contador: 3
```

---

### Uso en Node.js:
Muchas clases en Node.js heredan de `EventEmitter`, como:

1. **`http.Server`**:
   ```js
   const http = require('http');
   const server = http.createServer();

   server.on('request', (req, res) => {
     res.end('Solicitud recibida');
   });

   server.listen(3000, () => console.log('Servidor en http://localhost:3000'));
   ```

2. **`fs.ReadStream`**:
   ```js
   const fs = require('fs');
   const stream = fs.createReadStream('archivo.txt');

   stream.on('data', (chunk) => {
     console.log('Chunk recibido:', chunk.toString());
   });
   ```

---

### Resumen:
- **`EventEmitter`** es una clase central en Node.js para manejar eventos personalizados.
- Permite emitir y escuchar eventos de manera eficiente.
- Es ampliamente utilizado en módulos nativos como `http`, `fs`, y `net`.
- Facilita la creación de aplicaciones basadas en eventos.

## ¿Qué es dotenv en Node.js?
dotenv es una librería para cargar variables de entorno desde un archivo .env.

### Resumen:
El módulo **`fs`** es esencial para trabajar con el sistema de archivos en Node.js. Ofrece una API flexible que soporta operaciones sincrónicas, asincrónicas y basadas en promesas, lo que lo hace ideal para manejar archivos y directorios de manera eficiente.
```js
require('dotenv').config();
console.log(process.env.MI_VARIABLE);
```

## express.static

En **Express.js**, `express.static` es un middleware integrado que se utiliza para servir archivos estáticos, como HTML, CSS, JavaScript, imágenes, fuentes, etc., desde un directorio específico en tu aplicación.

---

### Características principales:
1. **Sirve archivos estáticos**: Permite que los clientes accedan a archivos directamente desde el servidor.
2. **Directorio público**: Define un directorio donde se almacenan los archivos estáticos.
3. **Rendimiento**: Optimiza la entrega de archivos estáticos al manejar encabezados HTTP como `Cache-Control`.

---

### Sintaxis:
```js
app.use(express.static(root, [options]));
```

- **`root`**: Ruta del directorio que contiene los archivos estáticos.
- **`options`**: Opciones adicionales (opcional), como configuración de caché.

---

### Ejemplo básico:
Supongamos que tienes un directorio llamado `public` con un archivo `index.html`.

**Estructura del proyecto**:
```
/public
  └── index.html
  └── styles.css
  └── script.js
app.js
```

**Código en `app.js`**:
```js
const express = require('express');
const app = express();

// Servir archivos estáticos desde el directorio "public"
app.use(express.static('public'));

// Iniciar el servidor
app.listen(3000, () => {
  console.log('Servidor ejecutándose en http://localhost:3000');
});
```

**Acceso a los archivos estáticos**:
- `http://localhost:3000/index.html`
- `http://localhost:3000/styles.css`
- `http://localhost:3000/script.js`

---

### Ejemplo con prefijo de ruta:
Puedes agregar un prefijo para los archivos estáticos.

```js
app.use('/static', express.static('public'));
```

Ahora, los archivos estáticos estarán disponibles en:
- `http://localhost:3000/static/index.html`
- `http://localhost:3000/static/styles.css`

---

### Opciones comunes:
1. **`maxAge`**: Configura la caché para los archivos estáticos.
   ```js
   app.use(express.static('public', { maxAge: '1d' })); // 1 día de caché
   ```

2. **`fallthrough`**: Si está en `false`, devuelve un error 404 si no se encuentra el archivo.
   ```js
   app.use(express.static('public', { fallthrough: false }));
   ```

---

### Resumen:
- `express.static` es un middleware para servir archivos estáticos como HTML, CSS, imágenes, etc.
- Es útil para aplicaciones web que necesitan entregar recursos estáticos al cliente.
- Puedes personalizar su comportamiento con opciones como caché y prefijos de ruta.


## callback hell
El **callback hell** en Node.js ocurre cuando se anidan múltiples funciones de callback, lo que hace que el código sea difícil de leer, mantener y depurar. Es un problema común en aplicaciones que manejan operaciones asincrónicas, como lectura de archivos, consultas a bases de datos o solicitudes HTTP.

---

### Ejemplo de callback hell:

```js
const fs = require('fs');

fs.readFile('archivo1.txt', 'utf8', (err, data1) => {
  if (err) return console.error(err);

  fs.readFile('archivo2.txt', 'utf8', (err, data2) => {
    if (err) return console.error(err);

    fs.readFile('archivo3.txt', 'utf8', (err, data3) => {
      if (err) return console.error(err);

      console.log('Datos:', data1, data2, data3);
    });
  });
});
```

En este ejemplo, las funciones de callback están anidadas unas dentro de otras, lo que genera un código en forma de "pirámide" que es difícil de seguir.

---

### Problemas del callback hell:
1. **Dificultad para leer**: El código se vuelve confuso y difícil de entender.
2. **Mantenimiento complicado**: Agregar o modificar lógica en callbacks anidados puede introducir errores.
3. **Manejo de errores**: Es difícil manejar errores de manera centralizada.
4. **Escalabilidad limitada**: A medida que aumenta la complejidad, el código se vuelve inmanejable.

---

### Soluciones al callback hell:

#### 1. **Usar Promesas**
Las promesas permiten encadenar operaciones asincrónicas de manera más legible.

```js
const fs = require('fs').promises;

fs.readFile('archivo1.txt', 'utf8')
  .then((data1) => {
    console.log(data1);
    return fs.readFile('archivo2.txt', 'utf8');
  })
  .then((data2) => {
    console.log(data2);
    return fs.readFile('archivo3.txt', 'utf8');
  })
  .then((data3) => {
    console.log(data3);
  })
  .catch((err) => {
    console.error(err);
  });
```

---

#### 2. **Usar `async/await`**
`async/await` simplifica aún más el manejo de operaciones asincrónicas, haciendo que el código se parezca a uno síncrono.

```js
const fs = require('fs').promises;

async function leerArchivos() {
  try {
    const data1 = await fs.readFile('archivo1.txt', 'utf8');
    console.log(data1);

    const data2 = await fs.readFile('archivo2.txt', 'utf8');
    console.log(data2);

    const data3 = await fs.readFile('archivo3.txt', 'utf8');
    console.log(data3);
  } catch (err) {
    console.error(err);
  }
}

leerArchivos();
```

---

#### 3. **Usar librerías como `async`**
La librería `async` proporciona utilidades para manejar operaciones asincrónicas de manera más estructurada.

```js
const async = require('async');
const fs = require('fs');

async.parallel(
  [
    (callback) => fs.readFile('archivo1.txt', 'utf8', callback),
    (callback) => fs.readFile('archivo2.txt', 'utf8', callback),
    (callback) => fs.readFile('archivo3.txt', 'utf8', callback),
  ],
  (err, results) => {
    if (err) return console.error(err);
    console.log('Datos:', results);
  }
);
```

---

### Resumen:
- **Callback hell** ocurre cuando las funciones de callback están anidadas excesivamente, dificultando la legibilidad y el mantenimiento del código.
- **Soluciones**:
  1. Usar **promesas** para encadenar operaciones.
  2. Usar **async/await** para un código más limpio y legible.
  3. Usar librerías como **`async`** para manejar flujos complejos.
- Estas técnicas ayudan a escribir código asincrónico más limpio, escalable y fácil de mantener.

## ¿Qué es async/await en Node.js?
async/await es una forma de escribir código asincrónico de manera más legible, utilizando funciones asincrónicas y esperando resultados sin usar callbacks.

```js
async function obtenerDatos() {
  let respuesta = await fetch('https://api.example.com/data');
  let datos = await respuesta.json();
  console.log(datos);
}

```

## urlencoded
En **Express.js**, `express.urlencoded` es un middleware integrado que se utiliza para analizar (parsear) los datos enviados en el cuerpo de una solicitud HTTP con el formato **`application/x-www-form-urlencoded`**. Este formato es común cuando se envían formularios HTML.

---

### Características principales:
1. **Analiza datos del cuerpo**: Convierte los datos enviados en el cuerpo de la solicitud en un objeto JavaScript accesible a través de `req.body`.
2. **Formato soportado**: Funciona con datos codificados como `application/x-www-form-urlencoded`.
3. **Configuración opcional**: Permite opciones como el límite de tamaño del cuerpo y el manejo de arrays.

---

### Sintaxis:
```js
app.use(express.urlencoded([options]));
```

- **`options`**: Un objeto opcional para configurar el middleware. Algunas opciones comunes son:
  - **`extended`**: Si es `true`, usa la librería `qs` para analizar datos complejos (como objetos anidados). Si es `false`, usa la librería `querystring`.
  - **`limit`**: Tamaño máximo permitido para el cuerpo de la solicitud.

---

### Ejemplo básico:
Supongamos que tienes un formulario HTML que envía datos al servidor:

**Formulario HTML**:
```html
<form action="/submit" method="POST">
  <input type="text" name="nombre" />
  <input type="text" name="edad" />
  <button type="submit">Enviar</button>
</form>
```

**Servidor Express**:
```js
const express = require('express');
const app = express();

// Middleware para analizar datos urlencoded
app.use(express.urlencoded({ extended: true }));

app.post('/submit', (req, res) => {
  const { nombre, edad } = req.body;
  res.send(`Nombre: ${nombre}, Edad: ${edad}`);
});

app.listen(3000, () => {
  console.log('Servidor ejecutándose en http://localhost:3000');
});
```

Cuando el formulario se envía, los datos estarán disponibles en `req.body` como un objeto:
```js
// Ejemplo de req.body
{
  nombre: 'Juan',
  edad: '25'
}
```

---

### Opción `extended`:
- **`extended: true`**: Permite analizar objetos anidados y datos complejos usando la librería `qs`.
- **`extended: false`**: Analiza datos simples usando la librería `querystring`.

**Ejemplo con datos anidados**:
Formulario que envía datos anidados:
```html
<form action="/submit" method="POST">
  <input type="text" name="usuario[nombre]" value="Juan" />
  <input type="text" name="usuario[edad]" value="25" />
  <button type="submit">Enviar</button>
</form>
```

Con `extended: true`, los datos se analizarán como:
```js
{
  usuario: {
    nombre: 'Juan',
    edad: '25'
  }
}
```

Con `extended: false`, los datos se analizarán como:
```js
{
  'usuario[nombre]': 'Juan',
  'usuario[edad]': '25'
}
```

---

### Resumen:
- **`express.urlencoded`** es un middleware para analizar datos enviados en el cuerpo de solicitudes HTTP con el formato `application/x-www-form-urlencoded`.
- Es útil para manejar formularios HTML.
- La opción `extended` define cómo se analizan los datos (simples o complejos).
- Los datos analizados están disponibles en `req.body`.

## ¿Qué es process.env?
process.env es un objeto que contiene las variables de entorno del sistema.
```js
console.log(process.env.NODE_ENV);  // Muestra el entorno (por ejemplo, 'production')
```

## ¿Qué es path en Node.js?
path es un módulo integrado en Node.js que permite trabajar con rutas de archivos y directorios.

```js
const path = require('path');
const rutaCompleta = path.join(__dirname, 'archivo.txt');
console.log(rutaCompleta);  // Muestra la ruta completa del archivo
````
## ¿Qué es url en Node.js?
El módulo url permite analizar y resolver URLs en Node.js.

```js
const url = require('url');
const miUrl = new URL('https://example.com/path?nombre=juan');

console.log(miUrl.hostname);  // Imprime 'example.com'
console.log(miUrl.pathname);  // Imprime '/path'
```


## child_process

El módulo **`child_process`** en Node.js permite crear y controlar procesos secundarios desde un programa Node.js. Esto es útil para ejecutar comandos del sistema, scripts externos o dividir tareas pesadas en procesos separados.

---

### Características principales:
1. **Ejecutar comandos del sistema**: Puedes ejecutar comandos como `ls`, `pwd`, o cualquier comando de shell.
2. **Crear procesos secundarios**: Permite ejecutar otros programas o scripts Node.js en procesos separados.
3. **Comunicación entre procesos**: Los procesos secundarios pueden comunicarse con el proceso principal mediante streams (`stdin`, `stdout`, `stderr`).

---

### Métodos principales de `child_process`:

1. **`exec`**:
   - Ejecuta un comando en el shell y devuelve el resultado como un callback.
   - Ideal para comandos simples.

   ```js
   const { exec } = require('child_process');

   exec('ls', (err, stdout, stderr) => {
     if (err) {
       console.error(`Error: ${err.message}`);
       return;
     }
     console.log(`Salida: ${stdout}`);
   });
   ```

---

2. **`spawn`**:
   - Crea un proceso secundario para ejecutar un comando.
   - Devuelve un objeto `ChildProcess` que permite manejar streams (`stdout`, `stderr`).
   - Ideal para tareas que generan grandes volúmenes de datos.

   ```js
   const { spawn } = require('child_process');

   const proceso = spawn('ls', ['-lh', '/usr']);

   proceso.stdout.on('data', (data) => {
     console.log(`Salida: ${data}`);
   });

   proceso.stderr.on('data', (data) => {
     console.error(`Error: ${data}`);
   });

   proceso.on('close', (code) => {
     console.log(`Proceso terminado con código ${code}`);
   });
   ```

---

3. **`fork`**:
   - Crea un proceso secundario específicamente para ejecutar otro archivo Node.js.
   - Permite comunicación directa entre el proceso principal y el secundario mediante mensajes.

   ```js
   const { fork } = require('child_process');

   const proceso = fork('hijo.js');

   proceso.on('message', (mensaje) => {
     console.log(`Mensaje del hijo: ${mensaje}`);
   });

   proceso.send('Hola desde el proceso principal');
   ```

   **Archivo `hijo.js`**:
   ```js
   process.on('message', (mensaje) => {
     console.log(`Mensaje recibido: ${mensaje}`);
     process.send('Hola desde el proceso hijo');
   });
   ```

---

4. **`execFile`**:
   - Similar a `exec`, pero ejecuta directamente un archivo sin usar un shell.
   - Más seguro porque no interpreta comandos del shell.

   ```js
   const { execFile } = require('child_process');

   execFile('node', ['-v'], (err, stdout, stderr) => {
     if (err) {
       console.error(`Error: ${err.message}`);
       return;
     }
     console.log(`Versión de Node.js: ${stdout}`);
   });
   ```

---

### Diferencias entre `exec`, `spawn`, `fork` y `execFile`:

| Método      | Uso principal                          | Comunicación | Shell utilizado |
|-------------|----------------------------------------|--------------|-----------------|
| **`exec`**  | Ejecutar comandos del sistema          | No           | Sí              |
| **`spawn`** | Ejecutar comandos con streams          | Sí           | No              |
| **`fork`**  | Ejecutar scripts Node.js               | Sí           | No              |
| **`execFile`** | Ejecutar archivos directamente       | No           | No              |

---

### Ejemplo práctico: Ejecutar un script Node.js en un proceso secundario

**Archivo principal (`main.js`)**:
```js
const { fork } = require('child_process');

const proceso = fork('worker.js');

proceso.on('message', (mensaje) => {
  console.log(`Mensaje del proceso secundario: ${mensaje}`);
});

proceso.send('Inicia el trabajo');
```

**Archivo secundario (`worker.js`)**:
```js
process.on('message', (mensaje) => {
  console.log(`Mensaje recibido: ${mensaje}`);
  process.send('Trabajo completado');
});
```

**Salida**:
```
Mensaje recibido: Inicia el trabajo
Mensaje del proceso secundario: Trabajo completado
```

---

### Resumen:
- **`child_process`** permite ejecutar comandos del sistema y crear procesos secundarios.
- Métodos como `exec`, `spawn`, `fork` y `execFile` ofrecen diferentes formas de manejar procesos.
- Es útil para tareas como ejecutar scripts externos, dividir cargas de trabajo y manejar procesos en paralelo.


## ¿Qué es os en Node.js?
El módulo os proporciona información sobre el sistema operativo, como el nombre, la plataforma y la memoria disponible.

```js
const os = require('os');
console.log(os.platform());  // Imprime el sistema operativo (por ejemplo, 'linux')
```

## process.exit()

En **Node.js**, `process.exit()` es un método que finaliza el proceso en ejecución de manera inmediata, devolviendo un código de salida al sistema operativo. Este método se utiliza para detener la ejecución de un programa cuando se ha completado una tarea o cuando ocurre un error crítico.

---

### Sintaxis:
```js
process.exit([code]);
```

- **`code`**: (Opcional) Un número entero que representa el código de salida. Por convención:
  - `0`: Indica que el programa terminó correctamente.
  - Cualquier otro número: Indica que ocurrió un error.

---

### Ejemplo básico:
```js
console.log('Inicio del programa');

// Finaliza el proceso con éxito
process.exit(0);

console.log('Esto no se ejecutará');
```

**Salida**:
```
Inicio del programa
```

---

### Ejemplo con código de error:
```js
if (!process.env.API_KEY) {
  console.error('Error: Falta la variable de entorno API_KEY');
  process.exit(1); // Finaliza con un código de error
}
```

---

### Cuándo usar `process.exit()`:
1. **Finalizar el programa después de un error crítico**:
   - Si ocurre un error que no puede ser manejado, puedes usar `process.exit()` para detener el programa.
2. **Finalizar después de completar una tarea específica**:
   - Por ejemplo, en scripts que realizan una tarea única, como migraciones de bases de datos.

---

### Advertencia:
- **Evitar usarlo innecesariamente**: `process.exit()` detiene el Event Loop de inmediato, incluso si hay operaciones pendientes (como callbacks o promesas). Esto puede causar comportamientos inesperados.
- **Alternativa**: En lugar de usar `process.exit()`, permite que el programa termine naturalmente cuando no haya más tareas pendientes.

---

### Ejemplo con promesas pendientes:
```js
console.log('Inicio del programa');

setTimeout(() => {
  console.log('Esto no se ejecutará si usas process.exit()');
}, 1000);

process.exit(0); // Finaliza inmediatamente
```

---

### Resumen:
- **`process.exit()`** detiene el proceso de Node.js inmediatamente.
- Útil para manejar errores críticos o finalizar scripts específicos.
- Usa con precaución, ya que puede interrumpir tareas pendientes en el Event Loop.


## global

En **Node.js**, **`global`** es un objeto global que actúa como el espacio de nombres principal para todas las variables y funciones globales. Es similar a `window` en los navegadores, pero está diseñado específicamente para el entorno de Node.js.

---

### Características principales:
1. **Acceso global**: Las propiedades y métodos definidos en `global` están disponibles en todo el programa sin necesidad de importarlos.
2. **No es necesario declararlo**: Puedes usar las propiedades de `global` directamente.
3. **Evitar abusos**: Aunque es accesible en todo el programa, se recomienda evitar agregar variables personalizadas a `global` para prevenir conflictos.

---

### Ejemplo básico:
```js
console.log(global); // Muestra todas las propiedades globales
```

---

### Propiedades y métodos comunes de `global`:

1. **`console`**:
   - Proporciona métodos para imprimir mensajes en la consola.
   ```js
   console.log('Hola, mundo');
   ```

2. **`setTimeout` y `setInterval`**:
   - Métodos para ejecutar funciones después de un tiempo o de manera repetitiva.
   ```js
   setTimeout(() => console.log('Hola después de 1 segundo'), 1000);
   setInterval(() => console.log('Hola cada 2 segundos'), 2000);
   ```

3. **`process`**:
   - Proporciona información y control sobre el proceso en ejecución.
   ```js
   console.log(process.pid); // ID del proceso
   ```

4. **`Buffer`**:
   - Maneja datos binarios.
   ```js
   const buffer = Buffer.from('Hola');
   console.log(buffer.toString());
   ```

5. **`__dirname` y `__filename`**:
   - Variables globales que indican el directorio y el archivo actual.
   ```js
   console.log(__dirname); // Ruta del directorio actual
   console.log(__filename); // Ruta completa del archivo actual
   ```

---

### Definir variables en `global`:
Aunque puedes agregar variables al objeto `global`, **no es una buena práctica** porque puede causar conflictos y dificultar el mantenimiento del código.

```js
global.miVariable = 'Hola, mundo';
console.log(miVariable); // Hola, mundo
```

---

### Diferencia entre `global` y variables locales:
Las variables definidas en `global` están disponibles en todo el programa, mientras que las variables locales solo están disponibles en el archivo o función donde se definen.

```js
// Variable global
global.miVariable = 'Soy global';

// Variable local
const miVariableLocal = 'Soy local';

console.log(global.miVariable); // Funciona
console.log(miVariableLocal);   // Funciona
```

---

### Resumen:
- **`global`** es el objeto principal en Node.js que contiene propiedades y métodos globales.
- Incluye herramientas como `console`, `setTimeout`, `process`, `Buffer`, entre otros.
- Aunque puedes agregar variables personalizadas a `global`, no es recomendable por razones de mantenimiento y posibles conflictos.


## process.argv


En **Node.js**, **`process.argv`** es una propiedad del objeto global `process` que contiene un array con los argumentos pasados al script cuando se ejecuta desde la línea de comandos.

---

### Características principales:
1. **Array de argumentos**: Contiene todos los argumentos proporcionados al ejecutar el script.
2. **Estructura**:
   - El primer elemento (`process.argv[0]`) es la ruta del ejecutable de Node.js.
   - El segundo elemento (`process.argv[1]`) es la ruta del archivo del script que se está ejecutando.
   - Los elementos restantes (`process.argv[2]` en adelante) son los argumentos proporcionados por el usuario.

---

### Ejemplo básico:
Supongamos que ejecutas el siguiente script con argumentos:

```bash
node script.js arg1 arg2 arg3
```

**Código (`script.js`)**:
```js
console.log(process.argv);
```

**Salida**:
```bash
[
  '/usr/local/bin/node',  // Ruta del ejecutable de Node.js
  '/path/to/script.js',   // Ruta del archivo del script
  'arg1',                 // Primer argumento
  'arg2',                 // Segundo argumento
  'arg3'                  // Tercer argumento
]
```

---

### Ejemplo práctico: Leer argumentos personalizados

```js
const args = process.argv.slice(2); // Ignorar los dos primeros elementos
console.log('Argumentos:', args);
```

**Ejecución**:
```bash
node script.js --name=Juan --age=30
```

**Salida**:
```bash
Argumentos: [ '--name=Juan', '--age=30' ]
```

---

### Ejemplo avanzado: Parsear argumentos

Puedes procesar los argumentos para extraer valores clave.

```js
const args = process.argv.slice(2);
const params = {};

args.forEach(arg => {
  const [key, value] = arg.split('=');
  params[key.replace('--', '')] = value;
});

console.log(params);
```

**Ejecución**:
```bash
node script.js --name=Juan --age=30
```

**Salida**:
```bash
{ name: 'Juan', age: '30' }
```

---

### Usos comunes:
1. **Configurar opciones del script**:
   - Pasar parámetros como nombres de archivos, configuraciones, etc.
2. **Automatización**:
   - Usar argumentos para personalizar tareas en scripts de automatización.
3. **CLI (Command Line Interface)**:
   - Crear herramientas de línea de comandos.

---

### Resumen:
- **`process.argv`** es un array que contiene los argumentos pasados al script desde la línea de comandos.
- Es útil para crear scripts dinámicos y herramientas CLI.
- Puedes procesar los argumentos para extraer valores clave y personalizar el comportamiento del script.
