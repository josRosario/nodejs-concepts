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
