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

---

### Resumen:
El módulo **`fs`** es esencial para trabajar con el sistema de archivos en Node.js. Ofrece una API flexible que soporta operaciones sincrónicas, asincrónicas y basadas en promesas, lo que lo hace ideal para manejar archivos y directorios de manera eficiente.
