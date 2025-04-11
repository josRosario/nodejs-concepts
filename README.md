# nodejs-concepts


## ¿Qué es Node.js?

**Node.js** es un entorno de ejecución para JavaScript en el lado del servidor basado en el motor V8 de Google Chrome.

**Node.js** es ideal para aplicaciones que necesitan manejar muchos datos, porque trabaja de manera asíncrona y se basa en eventos. Puedes usarlo para hacer aplicaciones web que manejan muchos datos, como sitios de videos en streaming. También es útil para crear: aplicaciones web en tiempo real, aplicaciones de red, aplicaciones generales

---
## ¿Por qué utilizar Node.js?
Node.js facilita la creación de programas de red escalables. Algunas de sus ventajas incluyen:

- Generalmente es rápido
- Rara vez se bloquea
- Todo es asincrónico 
- Produce una gran concurrencia
---
## ¿Cómo funciona Node.js?

- Motor V8 de Google Chrome: Node.js utiliza el motor V8, que es el mismo que usa Google Chrome para ejecutar JavaScript. Este motor convierte el código JavaScript en un lenguaje que la computadora pueda entender y ejecutar rápidamente.

- Modelo asíncrono y basado en eventos: Node.js utiliza un modelo de ejecución asíncrona. Esto significa que, en lugar de esperar a que una tarea termine antes de empezar la siguiente, Node.js puede hacer varias cosas al mismo tiempo. Esto es muy útil cuando se manejan muchas solicitudes de datos, como en las aplicaciones web en tiempo real.

- Event Loop (Bucle de eventos): Node.js tiene un "bucle de eventos", que es una forma en que se gestionan las tareas. Cuando una tarea (como una consulta a la base de datos) tarda un tiempo en completarse, Node.js no se queda esperando. En lugar de eso, sigue ejecutando otras tareas y cuando la tarea que estaba esperando termina, se ejecuta la función correspondiente. Esto mejora la eficiencia y el rendimiento.

- Non-blocking (No bloqueante): Node.js no bloquea el hilo principal mientras espera que se completen las tareas. Esto significa que puede manejar muchas conexiones a la vez sin quedar "congelado", lo que lo hace ideal para aplicaciones con alta carga de usuarios, como chats en tiempo real o aplicaciones de streaming.

  ---
## ¿Por qué Node.js es de un solo subproceso?

**Node.js** es de un solo subproceso porque su modelo asíncrono y el bucle de eventos le permiten manejar múltiples tareas de manera eficiente sin necesitar varios hilos, lo que lo hace más rápido y menos demandante en términos de recursos.

---
## ¿Qué es concurrencia?

- La concurrencia se refiere a la capacidad de un sistema para manejar múltiples tareas en el mismo período de tiempo, pero no necesariamente al mismo tiempo. En un sistema concurrente, las tareas pueden estar siendo ejecutadas de manera intercalada (una se ejecuta, luego se detiene para dejar que otra se ejecute, y luego vuelve a la primera). No requiere que todas las tareas se ejecuten exactamente al mismo tiempo, pero sí que el sistema sea capaz de manejarlas sin que se bloqueen entre sí.

---
## ¿Qué es paralelismo?
- El paralelismo, por otro lado, es cuando un sistema ejecuta múltiples tareas al mismo tiempo, usando varios procesadores o hilos. Esto significa que las tareas realmente se están ejecutando al mismo tiempo, en lugar de intercalarse entre sí.
---
## Si Node.js es de un solo subproceso, ¿cómo maneja la concurrencia?

- Aunque Node.js usa un solo hilo para ejecutar el código, maneja la concurrencia de manera eficiente gracias a su modelo asíncrono, su bucle de eventos y la delegación de tareas al sistema operativo para operaciones pesadas. Esto le permite manejar múltiples tareas simultáneamente sin bloquearse, lo que lo hace muy adecuado para aplicaciones con muchas solicitudes simultáneas.

---
## Explique la devolución de llamada en Node.js.

- Operaciones asíncronas: En Node.js, muchas operaciones, como leer archivos, hacer consultas a bases de datos o realizar solicitudes de red, son asíncronas. Esto significa que no podemos esperar a que una operación termine antes de seguir con la siguiente, porque podría tardar mucho tiempo.

- Paso de la devolución de llamada: En lugar de esperar bloqueado a que una operación termine, Node.js recibe una función callback que se ejecutará cuando la operación asíncrona termine. Esta función callback es pasada como argumento a la función que maneja la tarea asíncrona.

- Ejecución de la devolución de llamada: Una vez que la operación asíncrona se completa, la función callback es llamada (es decir, ejecutada). Si la tarea fue exitosa, la callback maneja los resultados. Si hubo un error, la callback también puede manejar el error.

---
## ¿Cuáles son las ventajas de utilizar promesas en lugar de devoluciones de llamadas?

- Legibilidad: Las promesas hacen que el código sea más limpio y fácil de leer.

- Manejo de errores centralizado: El manejo de errores es más sencillo y no necesitas verificar los errores en cada nivel.

- Encadenamiento y flujo claro: Las operaciones asíncronas se pueden encadenar de manera más clara y secuencial.

- Composición fácil de múltiples tareas: Herramientas como Promise.all() y Promise.race() facilitan el manejo de varias tareas simultáneas.

- Integración con async/await: Las promesas permiten usar una sintaxis más clara y fácil de entender mediante async/await.

---
## ¿Cómo definirías el término E/S? 

- En Node.js, E/S se refiere a Entrada/Salida (Input/Output en inglés) y describe las operaciones mediante las cuales un programa interactúa con el mundo exterior, como leer archivos, recibir solicitudes HTTP, escribir en la consola, acceder a bases de datos, etc.
---
## ¿Por qué se prefiere Node.js sobre otras tecnologías de backend como Java y PHP?

Algunas de las razones por las que se prefiere Node.js incluyen:

- Node.js es muy rápido
- Node Package Manager tiene más de 50.000 paquetes disponibles a disposición del desarrollador
- Perfecto para aplicaciones web en tiempo real con uso intensivo de datos, ya que Node.js nunca espera a que una API devuelva datos.
- Mejor sincronización de código entre el servidor y el cliente debido a la misma base de código
- Es fácil para los desarrolladores web comenzar a utilizar Node.js en sus proyectos, ya que es una biblioteca de JavaScript.

---
## ¿Qué base de datos se utiliza más popularmente con Node.js?
MongoDB es la base de datos más común utilizada con Node.js.  Es una base de datos NoSQL multiplataforma y orientada a documentos que ofrece alto rendimiento, alta disponibilidad y fácil escalabilidad.

---
##  ¿Cuál es el comando utilizado para importar bibliotecas externas?

En Node.js, el comando o instrucción que se utiliza para importar bibliotecas externas depende del sistema de módulos que estés usando:
**CommonJS (el sistema clásico de Node.js):**

Usa require() para importar bibliotecas.
```js
  const express = require('express');
```
**ES Modules (ESM) (más moderno):**
Usa import para importar módulos, similar a cómo se hace en el navegador.
```js
  import express from 'express';
```
**Para usar import, necesitas:**

- Que el archivo tenga la extensión .mjs o

- Que tu package.json tenga "type": "module"

---
## ¿Qué es la NPM?
NPM significa Node Package Manager, responsable de administrar todos los paquetes y módulos de Node.js.

- Node Package Manager proporciona dos funcionalidades principales:
- 
- Proporciona repositorios en línea para paquetes/módulos de node.js, que se pueden buscar en search.nodejs.org
Proporciona una utilidad de línea de comandos para instalar paquetes de Node.js y también administra versiones y dependencias de Node.js.  
---
## ¿Cuáles son los pros y contras de Node.js?

**Ventajas de Node.js**
- Procesamiento rápido y un modelo basado en eventos
- Utiliza JavaScript, que es muy conocido entre los desarrolladores.
- Node Package Manager tiene más de 50.000 paquetes que proporcionan la funcionalidad a una aplicación
- Más adecuado para la transmisión de grandes cantidades de datos y operaciones intensivas de E/S

**Desventajas de Node.js**
- No apto para tareas computacionales pesadas
- El uso de devoluciones de llamada es complejo ya que terminas con varias devoluciones de llamada anidadas
- Trabajar con bases de datos relacionales no es una buena opción para Node.js
- Dado que Node.js es de un solo subproceso, las tareas que requieren un uso intensivo de la CPU no son su punto fuerte.
  
---
## ¿Qué significa programación basada en eventos?

Un enfoque de programación basada en eventos utiliza eventos para activar diversas funciones. Un evento puede ser cualquier cosa, como pulsar una tecla o hacer clic en un botón del ratón. Una función de retrollamada ya está registrada en el elemento y se ejecuta cada vez que se activa un evento.

---

## ¿Cuáles son los dos tipos de funciones API en Node.js?
Los dos tipos de funciones API en Node.js son:

- Funciones asincrónicas y no bloqueantes
- Funciones síncronas y de bloqueo

---

## ¿Qué es el archivo package.json?

El archivo package.json es un componente fundamental en proyectos de Node.js y en general en cualquier proyecto que utilice npm (Node Package Manager) o yarn para la gestión de dependencias. Este archivo actúa como el manifiesto del proyecto, conteniendo información clave sobre el proyecto, sus dependencias, scripts y configuración.

---

## ¿Cómo instalar, actualizar y eliminar una dependencia?

```js
  npm install dependency
  npm uninstall dependency
  npm update dependency

```
---

## ¿Qué es REPL en Node.js?
REPL en Node.js significa **Read-Eval-Print Loop**. Es un entorno interactivo que permite ejecutar comandos de JavaScript en tiempo real. Es útil para probar fragmentos de código, depurar, o aprender cómo funcionan ciertas funciones de Node.js.

### Componentes de REPL:
1. **Read**: Lee la entrada del usuario.
2. **Eval**: Evalúa (ejecuta) el código ingresado.
3. **Print**: Muestra el resultado de la evaluación.
4. **Loop**: Vuelve al paso de lectura para aceptar más entradas.

### Cómo acceder al REPL:
1. Abre una terminal.
2. Escribe `node` y presiona Enter.

### Ejemplo:
```bash
$ node
> const sum = (a, b) => a + b;
undefined
> sum(5, 3);
8
```

Para salir del REPL, puedes usar el comando `.exit` o presionar `Ctrl + C` dos veces.
---

## ¿Qué es la función de flujo de control?

En Node.js, una función de flujo de control es un mecanismo que permite manejar la ejecución de código asíncrono de manera ordenada y predecible. Dado que Node.js es una plataforma basada en eventos y no bloqueante, muchas operaciones (como leer archivos, realizar solicitudes HTTP, etc.) son asíncronas. Las funciones de flujo de control ayudan a coordinar estas operaciones para evitar problemas como el **callback hell** o la dificultad de manejar múltiples tareas asíncronas.

### Ejemplos de funciones de flujo de control en Node.js:

1. **Callbacks**: Son funciones que se ejecutan después de que una operación asíncrona se completa.
   ```javascript
   const fs = require('fs');

   fs.readFile('archivo.txt', 'utf8', (err, data) => {
       if (err) {
           console.error(err);
           return;
       }
       console.log(data);
   });
   ```

2. **Promises**: Introducen un enfoque más limpio para manejar la asincronía.
   ```javascript
   const fs = require('fs').promises;

   fs.readFile('archivo.txt', 'utf8')
       .then(data => console.log(data))
       .catch(err => console.error(err));
   ```

3. **Async/Await**: Una forma más moderna y legible de manejar Promises.
   ```javascript
   const fs = require('fs').promises;

   async function leerArchivo() {
       try {
           const data = await fs.readFile('archivo.txt', 'utf8');
           console.log(data);
       } catch (err) {
           console.error(err);
       }
   }

   leerArchivo();
   ```

4. **Librerías de control de flujo**: Herramientas como `async` (librería externa) que proporcionan utilidades para manejar tareas asíncronas en paralelo, en serie, etc.

Estas funciones son esenciales para manejar la naturaleza asíncrona de Node.js y garantizar que el código sea eficiente y fácil de mantener.

---

## ¿Cómo gestiona el flujo de control las llamadas de función

En Node.js, el flujo de control para las llamadas de función se gestiona principalmente a través de su modelo de ejecución basado en el **event loop** y la **pila de llamadas (call stack)**. Este modelo permite manejar tanto operaciones síncronas como asíncronas de manera eficiente.

### Gestión del flujo de control en llamadas de función:

1. **Síncronas**:
   - Las funciones se ejecutan en el orden en que son llamadas.
   - Cada función se coloca en la pila de llamadas (call stack) y se ejecuta completamente antes de pasar a la siguiente.
   - Ejemplo:
     ```javascript
     function saludo() {
         console.log("Hola");
     }

     function despedida() {
         console.log("Adiós");
     }

     saludo(); // Se ejecuta primero
     despedida(); // Se ejecuta después
     ```

2. **Asíncronas**:
   - Las operaciones asíncronas no bloquean la ejecución del programa.
   - Cuando se encuentra una operación asíncrona (como una lectura de archivo o una solicitud HTTP), esta se delega al sistema operativo o a un subproceso, y la función principal continúa ejecutándose.
   - Una vez que la operación asíncrona se completa, su callback o promesa se coloca en la **cola de tareas (task queue)** y espera a que el event loop la procese.

   Ejemplo con un `setTimeout`:
   ```javascript
   console.log("Inicio");

   setTimeout(() => {
       console.log("Tarea asíncrona");
   }, 1000);

   console.log("Fin");
   ```
   **Salida**:
   ```
   Inicio
   Fin
   Tarea asíncrona
   ```

3. **Event Loop**:
   - El **event loop** es el mecanismo que gestiona el flujo de control en Node.js.
   - Funciona revisando continuamente la pila de llamadas y la cola de tareas. Si la pila está vacía, toma las tareas pendientes de la cola y las ejecuta.

4. **Promesas y Async/Await**:
   - Las promesas y `async/await` introducen un flujo de control más estructurado para manejar asincronía.
   - Las promesas se colocan en la **cola de microtareas (microtask queue)**, que tiene mayor prioridad que la cola de tareas normales.

   Ejemplo con `async/await`:
   ```javascript
   async function ejemplo() {
       console.log("Inicio");
       await new Promise(resolve => setTimeout(resolve, 1000));
       console.log("Después del await");
   }

   ejemplo();
   console.log("Fin");
   ```
   **Salida**:
   ```
   Inicio
   Fin
   Después del await
   ```

### Resumen:
Node.js gestiona el flujo de control mediante:
- **Call Stack**: Para ejecutar funciones síncronas.
- **Event Loop**: Para coordinar tareas asíncronas.
- **Task Queue y Microtask Queue**: Para manejar callbacks y promesas, respectivamente.

Esto permite que Node.js sea eficiente y no bloqueante, ideal para aplicaciones que requieren manejar múltiples operaciones concurrentes.

---
## ¿Cuál es la diferencia entre los métodos fork() y spawn() en Node.js?

En Node.js, los métodos `fork()` y `spawn()` son utilizados para crear procesos secundarios (child processes), pero tienen diferencias clave en su propósito y funcionamiento. Ambos forman parte del módulo `child_process`.

### **1. `spawn()`**
- **Propósito**: Se utiliza para ejecutar un comando o programa externo en un proceso secundario.
- **Uso**: Ideal para ejecutar comandos del sistema o programas externos, como `ls`, `grep`, o scripts en otros lenguajes.
- **Comunicación**: Permite la comunicación con el proceso secundario a través de flujos estándar (`stdin`, `stdout`, `stderr`).
- **Características**:
  - No establece un canal de comunicación adicional entre el proceso principal y el secundario.
  - Es más genérico y flexible para ejecutar cualquier comando o programa.

**Ejemplo con `spawn()`**:
```javascript
const { spawn } = require('child_process');

// Ejecuta el comando 'ls' para listar archivos en el directorio actual
const proceso = spawn('ls', ['-lh']);

proceso.stdout.on('data', (data) => {
    console.log(`Salida: ${data}`);
});

proceso.stderr.on('data', (data) => {
    console.error(`Error: ${data}`);
});

proceso.on('close', (code) => {
    console.log(`Proceso terminado con código: ${code}`);
});
```

---

### **2. `fork()`**
- **Propósito**: Se utiliza específicamente para crear un nuevo proceso Node.js que ejecuta un módulo JavaScript.
- **Uso**: Ideal para dividir tareas pesadas o paralelizar operaciones dentro de una aplicación Node.js.
- **Comunicación**: Establece un canal de comunicación dedicado entre el proceso principal y el secundario mediante mensajes (usando `process.send()` y `process.on('message')`).
- **Características**:
  - Está diseñado específicamente para ejecutar scripts Node.js.
  - Proporciona un canal de comunicación más sencillo y directo entre procesos.

**Ejemplo con `fork()`**:
Archivo principal (`main.js`):
```javascript
const { fork } = require('child_process');

// Crea un proceso secundario que ejecuta 'child.js'
const child = fork('./child.js');

// Envía un mensaje al proceso secundario
child.send({ saludo: 'Hola desde el proceso principal' });

// Escucha mensajes del proceso secundario
child.on('message', (message) => {
    console.log('Mensaje del proceso secundario:', message);
});
```

Archivo secundario (`child.js`):
```javascript
process.on('message', (message) => {
    console.log('Mensaje recibido del proceso principal:', message);

    // Envía un mensaje de vuelta al proceso principal
    process.send({ respuesta: 'Hola desde el proceso secundario' });
});
```

---

### **Diferencias clave entre `fork()` y `spawn()`**

| Característica            | `spawn()`                              | `fork()`                              |
|---------------------------|-----------------------------------------|---------------------------------------|
| **Propósito**             | Ejecutar comandos/programas externos.  | Ejecutar módulos Node.js.             |
| **Comunicación**          | Flujos estándar (`stdin`, `stdout`).    | Canal dedicado con `process.send()`.  |
| **Uso principal**         | Comandos del sistema o programas.       | Tareas Node.js paralelas.             |
| **Canal de comunicación** | No tiene un canal adicional.           | Tiene un canal de mensajes integrado. |

### **Conclusión**
- Usa `spawn()` cuando necesites ejecutar comandos o programas externos.
- Usa `fork()` cuando necesites ejecutar un módulo Node.js y comunicarte fácilmente entre procesos.

---

## ¿Qué es la canalización en Node.js?

En Node.js, la **canalización** (o *piping*) es un mecanismo que permite conectar flujos de datos (*streams*) de manera que la salida de un flujo se convierta en la entrada de otro. Esto es especialmente útil para manejar datos de forma eficiente y en tiempo real, sin necesidad de cargar todo el contenido en memoria.

La canalización se implementa principalmente con el método `.pipe()` que está disponible en los objetos de tipo *stream* en Node.js.

---

### **¿Cómo funciona la canalización?**
1. **Flujos (Streams)**: Los flujos en Node.js son objetos que permiten leer o escribir datos de manera secuencial. Hay cuatro tipos principales de flujos:
   - **Readable**: Flujos de lectura (por ejemplo, leer un archivo).
   - **Writable**: Flujos de escritura (por ejemplo, escribir en un archivo).
   - **Duplex**: Flujos que son tanto de lectura como de escritura.
   - **Transform**: Flujos que pueden modificar o transformar los datos mientras pasan a través de ellos.

2. **Método `.pipe()`**: Este método conecta un flujo de lectura con un flujo de escritura o transformación. Los datos fluyen automáticamente desde el flujo de origen al flujo de destino.

---

### **Ejemplo básico de canalización**
Copiar el contenido de un archivo a otro usando flujos y canalización:
```javascript
const fs = require('fs');

// Crear un flujo de lectura y un flujo de escritura
const flujoLectura = fs.createReadStream('archivoOrigen.txt');
const flujoEscritura = fs.createWriteStream('archivoDestino.txt');

// Canalizar los datos del flujo de lectura al flujo de escritura
flujoLectura.pipe(flujoEscritura);

console.log('Archivo copiado con éxito.');
```

En este ejemplo:
- Los datos se leen de `archivoOrigen.txt` en fragmentos (chunks).
- Esos fragmentos se escriben directamente en `archivoDestino.txt` sin cargar todo el archivo en memoria.

---

### **Ejemplo con transformación**
Comprimir un archivo usando el módulo `zlib` y canalización:
```javascript
const fs = require('fs');
const zlib = require('zlib');

// Crear un flujo de lectura, un flujo de compresión y un flujo de escritura
const flujoLectura = fs.createReadStream('archivo.txt');
const flujoCompresion = zlib.createGzip();
const flujoEscritura = fs.createWriteStream('archivo.txt.gz');

// Canalizar los datos a través del flujo de compresión y luego al flujo de escritura
flujoLectura.pipe(flujoCompresion).pipe(flujoEscritura);

console.log('Archivo comprimido con éxito.');
```

En este caso:
- Los datos se leen de `archivo.txt`.
- Se comprimen usando `zlib.createGzip()`.
- Los datos comprimidos se escriben en `archivo.txt.gz`.

---

### **Ventajas de la canalización**
1. **Eficiencia**: Los datos se procesan en fragmentos, lo que reduce el uso de memoria.
2. **Simplicidad**: El método `.pipe()` simplifica la conexión entre flujos.
3. **Procesamiento en tiempo real**: Los datos se procesan a medida que están disponibles, sin necesidad de esperar a que se cargue todo el contenido.

---

### **Conclusión**
La canalización en Node.js es una herramienta poderosa para manejar flujos de datos de manera eficiente y escalable. Es ampliamente utilizada en tareas como la manipulación de archivos, la compresión, la transmisión de datos en redes y más.

---

## ¿Cuáles son algunas de las banderas utilizadas en las operaciones de lectura/escritura en archivos?

En Node.js, al realizar operaciones de lectura y escritura en archivos mediante el módulo `fs`, se pueden usar **banderas (flags)** para especificar cómo se debe abrir o manipular un archivo. Estas banderas controlan el comportamiento de las operaciones, como si se debe leer, escribir, sobrescribir, agregar contenido, etc.

A continuación, se enumeran algunas de las banderas más comunes:

---

### **Banderas comunes para operaciones de lectura/escritura**

| **Bandera** | **Descripción**                                                                 |
|-------------|---------------------------------------------------------------------------------|
| `'r'`       | Abre el archivo en modo de **lectura**. Lanza un error si el archivo no existe. |
| `'r+'`      | Abre el archivo en modo de **lectura y escritura**. Lanza un error si no existe.|
| `'w'`       | Abre el archivo en modo de **escritura**. Si el archivo existe, lo sobrescribe; si no, lo crea. |
| `'w+'`      | Abre el archivo en modo de **lectura y escritura**. Sobrescribe el archivo si existe; lo crea si no. |
| `'a'`       | Abre el archivo en modo de **agregar (append)**. Si no existe, lo crea.         |
| `'a+'`      | Abre el archivo en modo de **lectura y agregar**. Si no existe, lo crea.        |
| `'ax'`      | Similar a `'a'`, pero lanza un error si el archivo ya existe.                  |
| `'ax+'`     | Similar a `'a+'`, pero lanza un error si el archivo ya existe.                 |
| `'wx'`      | Similar a `'w'`, pero lanza un error si el archivo ya existe.                  |
| `'wx+'`     | Similar a `'w+'`, pero lanza un error si el archivo ya existe.                 |

---

### **Ejemplos prácticos**

1. **Lectura de un archivo (`'r'`)**:
   ```javascript
   const fs = require('fs');

   fs.open('archivo.txt', 'r', (err, fd) => {
       if (err) {
           console.error('Error al abrir el archivo:', err);
           return;
       }
       console.log('Archivo abierto en modo lectura.');
       fs.close(fd, () => console.log('Archivo cerrado.'));
   });
   ```

2. **Escritura en un archivo (`'w'`)**:
   ```javascript
   const fs = require('fs');

   fs.writeFile('archivo.txt', 'Contenido nuevo', { flag: 'w' }, (err) => {
       if (err) {
           console.error('Error al escribir en el archivo:', err);
           return;
       }
       console.log('Archivo sobrescrito con éxito.');
   });
   ```

3. **Agregar contenido a un archivo (`'a'`)**:
   ```javascript
   const fs = require('fs');

   fs.appendFile('archivo.txt', '\nContenido adicional', { flag: 'a' }, (err) => {
       if (err) {
           console.error('Error al agregar contenido:', err);
           return;
       }
       console.log('Contenido agregado con éxito.');
   });
   ```

4. **Evitar sobrescribir un archivo existente (`'wx'`)**:
   ```javascript
   const fs = require('fs');

   fs.writeFile('archivo.txt', 'Contenido nuevo', { flag: 'wx' }, (err) => {
       if (err) {
           console.error('Error: el archivo ya existe.');
           return;
       }
       console.log('Archivo creado con éxito.');
   });
   ```

---

### **Resumen**
- Las banderas permiten controlar cómo se abren y manipulan los archivos.
- Son útiles para definir si se debe leer, escribir, sobrescribir, agregar contenido o evitar conflictos con archivos existentes.
- Estas banderas se pueden usar con métodos como `fs.open()`, `fs.writeFile()`, `fs.appendFile()`, entre otros.

Para más detalles, puedes consultar la [documentación oficial de Node.js](https://nodejs.org/api/fs.html#file-system-flags).

---

## ¿Qué es un patrón de reactor en Node.js?
El **patrón de reactor** es un diseño arquitectónico que subyace en el funcionamiento de Node.js y su modelo de concurrencia. Este patrón permite manejar múltiples operaciones de entrada/salida (I/O) de manera eficiente y no bloqueante, lo que es ideal para aplicaciones que necesitan manejar muchas conexiones simultáneas, como servidores web.

---

### **¿Qué es el patrón de reactor?**
El patrón de reactor es un mecanismo que utiliza un bucle de eventos (*event loop*) para gestionar múltiples eventos de entrada/salida de forma asíncrona. En lugar de bloquear el programa mientras espera que una operación de I/O (como leer un archivo o recibir datos de una red) se complete, el reactor delega estas operaciones al sistema operativo y continúa ejecutando otras tareas. Cuando la operación de I/O está lista, el reactor invoca un *callback* asociado para manejar el resultado.

---

### **Cómo funciona en Node.js**
Node.js implementa el patrón de reactor a través de su **event loop** y la biblioteca subyacente **libuv**. El flujo general es el siguiente:

1. **Registro de eventos**:
   - Cuando se realiza una operación de I/O (como leer un archivo o escuchar una conexión de red), Node.js registra esta operación en el sistema operativo y asocia un *callback* para manejar el resultado.

2. **Delegación al sistema operativo**:
   - Node.js delega la operación de I/O al sistema operativo, que es más eficiente en la gestión de estas tareas.

3. **Event loop**:
   - Mientras el sistema operativo maneja las operaciones de I/O, el *event loop* de Node.js sigue ejecutando otras tareas disponibles, como ejecutar código JavaScript o manejar otros eventos.

4. **Notificación y ejecución del callback**:
   - Cuando el sistema operativo completa la operación de I/O, notifica a Node.js. El *event loop* entonces ejecuta el *callback* asociado para manejar el resultado.

---

### **Ejemplo práctico**
Un ejemplo típico del patrón de reactor en Node.js es el manejo de solicitudes HTTP:

```javascript
const http = require('http');

// Crear un servidor HTTP
const server = http.createServer((req, res) => {
    // Este callback se ejecuta cuando llega una solicitud
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hola, mundo!\n');
});

// Escuchar en el puerto 3000
server.listen(3000, () => {
    console.log('Servidor escuchando en el puerto 3000');
});
```

En este ejemplo:
1. El servidor registra un evento para escuchar conexiones en el puerto 3000.
2. Cuando llega una solicitud, el *event loop* invoca el *callback* asociado (`(req, res) => { ... }`).
3. Mientras tanto, el servidor puede manejar otras solicitudes sin bloquearse.

---

### **Ventajas del patrón de reactor**
1. **Eficiencia**: Permite manejar miles de conexiones simultáneamente sin bloquear el programa.
2. **Escalabilidad**: Ideal para aplicaciones que requieren alta concurrencia, como servidores web o aplicaciones en tiempo real.
3. **No bloqueante**: Las operaciones de I/O no detienen la ejecución del programa.

---

### **Limitaciones**
1. **Operaciones intensivas de CPU**: El patrón de reactor no es ideal para tareas que consumen mucha CPU, ya que el *event loop* podría bloquearse.
2. **Complejidad**: Manejar asincronía puede ser más complejo, especialmente en aplicaciones grandes.

---

### **Conclusión**
El patrón de reactor es la base del modelo de concurrencia de Node.js, permitiendo manejar operaciones de I/O de manera eficiente y no bloqueante. Esto lo hace ideal para aplicaciones que necesitan manejar muchas conexiones simultáneamente, como servidores web, aplicaciones en tiempo real y sistemas de transmisión de datos.

---
## ¿Qué es una pirámide de pruebas en Node.js?


La **pirámide de pruebas** es un concepto en el desarrollo de software que describe cómo estructurar y priorizar diferentes tipos de pruebas para garantizar la calidad del código. En el contexto de **Node.js**, la pirámide de pruebas se aplica para organizar las pruebas de una aplicación en niveles, asegurando que las pruebas sean eficientes, rápidas y confiables.

---

### **Estructura de la pirámide de pruebas**
La pirámide de pruebas tiene tres niveles principales, organizados de la base a la cima:

1. **Pruebas unitarias (Base de la pirámide)**:
   - **Descripción**: Son pruebas que verifican unidades individuales de código, como funciones o métodos, de forma aislada.
   - **Objetivo**: Garantizar que cada componente funcione correctamente de manera independiente.
   - **Características**:
     - Son rápidas de ejecutar.
     - No dependen de bases de datos, redes u otros servicios externos.
   - **Ejemplo en Node.js**:
     ```javascript
     const assert = require('assert');
     const suma = (a, b) => a + b;

     describe('Pruebas unitarias', () => {
         it('Debería sumar dos números correctamente', () => {
             assert.strictEqual(suma(2, 3), 5);
         });
     });
     ```

2. **Pruebas de integración (Nivel intermedio)**:
   - **Descripción**: Verifican cómo interactúan diferentes módulos o componentes entre sí.
   - **Objetivo**: Asegurar que las dependencias entre módulos funcionen correctamente.
   - **Características**:
     - Pueden incluir interacciones con bases de datos, APIs u otros servicios.
     - Son más lentas que las pruebas unitarias.
   - **Ejemplo en Node.js**:
     ```javascript
     const request = require('supertest');
     const app = require('./app'); // Tu aplicación Express

     describe('Pruebas de integración', () => {
         it('Debería responder con un mensaje de bienvenida', async () => {
             const res = await request(app).get('/');
             expect(res.statusCode).toBe(200);
             expect(res.text).toBe('Bienvenido a la API');
         });
     });
     ```

3. **Pruebas end-to-end (Cima de la pirámide)**:
   - **Descripción**: Simulan el comportamiento del usuario final y prueban el sistema completo, desde el frontend hasta el backend.
   - **Objetivo**: Validar que la aplicación funcione correctamente como un todo.
   - **Características**:
     - Son las más lentas y costosas de ejecutar.
     - Requieren un entorno completo y configurado.
   - **Ejemplo en Node.js** (usando una herramienta como `Playwright` o `Cypress`):
     ```javascript
     const { chromium } = require('playwright');

     describe('Pruebas end-to-end', () => {
         it('Debería cargar la página principal', async () => {
             const browser = await chromium.launch();
             const page = await browser.newPage();
             await page.goto('http://localhost:3000');
             const title = await page.title();
             expect(title).toBe('Mi Aplicación');
             await browser.close();
         });
     });
     ```

---

### **Importancia de la pirámide de pruebas**
1. **Eficiencia**:
   - Las pruebas unitarias son rápidas y económicas, por lo que deben ser la mayoría.
   - Las pruebas de integración y end-to-end son más lentas y costosas, por lo que deben ser menos frecuentes.

2. **Confiabilidad**:
   - Una base sólida de pruebas unitarias ayuda a detectar errores rápidamente.
   - Las pruebas de integración y end-to-end aseguran que los componentes trabajen bien juntos y que la experiencia del usuario sea correcta.

3. **Mantenimiento**:
   - Seguir la pirámide de pruebas ayuda a mantener un equilibrio entre la cobertura de pruebas y el tiempo de ejecución.

---

### **Conclusión**
En **Node.js**, la pirámide de pruebas es una guía para estructurar las pruebas de manera eficiente:
- **Pruebas unitarias**: La base, rápidas y numerosas.
- **Pruebas de integración**: En el medio, para validar interacciones entre componentes.
- **Pruebas end-to-end**: En la cima, para probar el sistema completo.

Este enfoque asegura que las pruebas sean rápidas, confiables y escalables, ayudando a mantener la calidad del código y la experiencia del usuario.

---
## Describe los códigos de salida de Node.js.

En Node.js, los **códigos de salida** son valores numéricos que un proceso devuelve al sistema operativo cuando termina su ejecución. Estos códigos indican si el proceso finalizó correctamente o si ocurrió algún error. Los códigos de salida son útiles para depurar y manejar errores en aplicaciones o scripts.

---

### **Códigos de salida comunes en Node.js**

1. **Código `0`**:
   - **Descripción**: Indica que el proceso terminó correctamente, sin errores.
   - **Ejemplo**:
     ```javascript
     process.exit(0); // Finaliza el proceso con éxito
     ```

2. **Código distinto de `0`**:
   - **Descripción**: Indica que el proceso terminó con un error o de manera anormal.
   - **Ejemplo**:
     ```javascript
     process.exit(1); // Finaliza el proceso con un error genérico
     ```

---

### **Códigos de salida específicos de Node.js**

Node.js tiene algunos códigos de salida predefinidos que indican errores específicos:

| **Código** | **Descripción**                                                                 |
|------------|---------------------------------------------------------------------------------|
| `1`        | Error genérico no manejado.                                                    |
| `3`        | Error interno de JavaScript (por ejemplo, un error en el motor V8).            |
| `4`        | Error de inicialización fatal.                                                 |
| `5`        | Error fatal en el sistema de depuración.                                       |
| `6`        | Solicitud de depuración inválida.                                              |
| `7`        | Error interno de asignación de memoria.                                        |
| `9`        | Argumento inválido pasado a una opción de Node.js.                             |
| `10`       | Error interno de JavaScript al iniciar el proceso.                             |
| `12`       | Error de asignación de memoria al intentar cargar el motor V8.                |
| `13`       | Error de inicialización del motor V8.                                          |
| `>128`     | El proceso fue terminado por una señal del sistema (por ejemplo, `SIGKILL`).   |

---

### **Cómo manejar códigos de salida en Node.js**

1. **Establecer un código de salida manualmente**:
   Puedes usar `process.exit(code)` para finalizar un proceso con un código específico.
   ```javascript
   if (error) {
       console.error('Ocurrió un error');
       process.exit(1); // Finaliza con un código de error
   } else {
       console.log('Proceso completado con éxito');
       process.exit(0); // Finaliza correctamente
   }
   ```

2. **Detectar el código de salida de un proceso secundario**:
   Si usas el módulo `child_process` para ejecutar procesos secundarios, puedes capturar su código de salida.
   ```javascript
   const { spawn } = require('child_process');

   const proceso = spawn('node', ['script.js']);

   proceso.on('close', (code) => {
       console.log(`El proceso terminó con el código: ${code}`);
   });
   ```

3. **Manejar errores no capturados**:
   Puedes capturar errores no manejados y establecer un código de salida personalizado.
   ```javascript
   process.on('uncaughtException', (err) => {
       console.error('Error no capturado:', err);
       process.exit(1); // Finaliza con un código de error
   });

   // Ejemplo de error no capturado
   throw new Error('Esto es un error no manejado');
   ```

---

### **Códigos de salida relacionados con señales del sistema**
Cuando un proceso es terminado por una señal del sistema (como `SIGKILL` o `SIGTERM`), el código de salida será mayor a `128`. Por ejemplo:
- `137`: El proceso fue terminado con la señal `SIGKILL` (`128 + 9`).
- `143`: El proceso fue terminado con la señal `SIGTERM` (`128 + 15`).

---

### **Conclusión**
Los códigos de salida en Node.js son esenciales para indicar el estado de finalización de un proceso. El código `0` indica éxito, mientras que los códigos distintos de `0` representan errores o terminaciones anormales. Comprender y manejar estos códigos es fundamental para depurar aplicaciones y garantizar un comportamiento predecible en entornos de producción.

---
## ¿Cuáles son los diferentes tipos de solicitudes HTTP?

Los diferentes tipos de solicitudes HTTP (también conocidos como **métodos HTTP**) son comandos que indican la acción que se desea realizar en un recurso del servidor. Estos métodos son fundamentales en el desarrollo de aplicaciones web y APIs. A continuación, se describen los métodos más comunes:

---

### **1. GET**
- **Descripción**: Se utiliza para **obtener** datos de un servidor.
- **Características**:
  - No tiene cuerpo en la solicitud.
  - Es idempotente (realizar la misma solicitud varias veces no cambia el estado del servidor).
  - Generalmente se utiliza para recuperar información.
- **Ejemplo**:
  ```http
  GET /usuarios HTTP/1.1
  Host: ejemplo.com
  ```

---

### **2. POST**
- **Descripción**: Se utiliza para **enviar datos** al servidor y crear un nuevo recurso.
- **Características**:
  - Incluye un cuerpo en la solicitud con los datos a enviar.
  - No es idempotente (enviar la misma solicitud varias veces puede crear múltiples recursos).
- **Ejemplo**:
  ```http
  POST /usuarios HTTP/1.1
  Host: ejemplo.com
  Content-Type: application/json

  {
      "nombre": "Juan",
      "edad": 30
  }
  ```

---

### **3. PUT**
- **Descripción**: Se utiliza para **actualizar** un recurso existente o **crear** uno si no existe.
- **Características**:
  - Incluye un cuerpo en la solicitud con los datos del recurso.
  - Es idempotente.
- **Ejemplo**:
  ```http
  PUT /usuarios/1 HTTP/1.1
  Host: ejemplo.com
  Content-Type: application/json

  {
      "nombre": "Juan",
      "edad": 31
  }
  ```

---

### **4. PATCH**
- **Descripción**: Se utiliza para **actualizar parcialmente** un recurso existente.
- **Características**:
  - Similar a `PUT`, pero solo modifica los campos especificados en el cuerpo de la solicitud.
  - No siempre es idempotente.
- **Ejemplo**:
  ```http
  PATCH /usuarios/1 HTTP/1.1
  Host: ejemplo.com
  Content-Type: application/json

  {
      "edad": 32
  }
  ```

---

### **5. DELETE**
- **Descripción**: Se utiliza para **eliminar** un recurso del servidor.
- **Características**:
  - Es idempotente.
- **Ejemplo**:
  ```http
  DELETE /usuarios/1 HTTP/1.1
  Host: ejemplo.com
  ```

---

### **6. HEAD**
- **Descripción**: Similar a `GET`, pero solo recupera los encabezados de la respuesta, sin el cuerpo.
- **Características**:
  - Útil para verificar si un recurso existe o para obtener metadatos.
  - Es idempotente.
- **Ejemplo**:
  ```http
  HEAD /usuarios HTTP/1.1
  Host: ejemplo.com
  ```

---

### **7. OPTIONS**
- **Descripción**: Se utiliza para describir las opciones de comunicación disponibles para un recurso.
- **Características**:
  - Devuelve los métodos HTTP permitidos para un recurso.
  - Es idempotente.
- **Ejemplo**:
  ```http
  OPTIONS /usuarios HTTP/1.1
  Host: ejemplo.com
  ```

---

### **8. TRACE**
- **Descripción**: Se utiliza para realizar una prueba de diagnóstico, devolviendo lo que el servidor recibe.
- **Características**:
  - Generalmente se utiliza para depuración.
  - No es comúnmente usado por razones de seguridad.
- **Ejemplo**:
  ```http
  TRACE /usuarios HTTP/1.1
  Host: ejemplo.com
  ```

---

### **9. CONNECT**
- **Descripción**: Se utiliza para establecer un túnel hacia el servidor, generalmente para conexiones seguras como HTTPS.
- **Características**:
  - Específico para proxies.
- **Ejemplo**:
  ```http
  CONNECT ejemplo.com:443 HTTP/1.1
  ```

---

### **Resumen de los métodos más comunes**

| **Método** | **Propósito**                  | **Idempotente** | **Cuerpo permitido** |
|------------|--------------------------------|-----------------|-----------------------|
| `GET`      | Obtener datos                  | Sí              | No                    |
| `POST`     | Crear un recurso               | No              | Sí                    |
| `PUT`      | Crear o reemplazar un recurso  | Sí              | Sí                    |
| `PATCH`    | Actualizar parcialmente        | No              | Sí                    |
| `DELETE`   | Eliminar un recurso            | Sí              | No (generalmente)     |
| `HEAD`     | Obtener solo los encabezados   | Sí              | No                    |
| `OPTIONS`  | Consultar métodos permitidos   | Sí              | No                    |

---

### **Conclusión**
Los métodos HTTP son fundamentales para la comunicación entre clientes y servidores. Cada método tiene un propósito específico y debe usarse adecuadamente para garantizar que las aplicaciones sean eficientes, seguras y fáciles de mantener.

---
## ¿Cuál es el propósito de NODE_ENV?
El propósito de la variable de entorno `NODE_ENV` en Node.js es definir el **entorno de ejecución** en el que se encuentra la aplicación. Esto permite configurar el comportamiento de la aplicación según el entorno, como **desarrollo**, **producción** o **pruebas**. Es una práctica común en aplicaciones Node.js para optimizar el rendimiento, habilitar o deshabilitar características específicas y gestionar configuraciones de manera eficiente.

---

### **Valores comunes de `NODE_ENV`**
1. **`development`**:
   - Indica que la aplicación está en un entorno de desarrollo.
   - Se utiliza para habilitar herramientas como depuradores, mensajes detallados de error y recarga automática del servidor.
   - Ejemplo:
     ```bash
     NODE_ENV=development node app.js
     ```

2. **`production`**:
   - Indica que la aplicación está en un entorno de producción.
   - Se utiliza para optimizar el rendimiento, deshabilitar mensajes de depuración y activar configuraciones específicas para producción.
   - Ejemplo:
     ```bash
     NODE_ENV=production node app.js
     ```

3. **`test`**:
   - Indica que la aplicación está en un entorno de pruebas.
   - Se utiliza para configurar bases de datos de prueba, deshabilitar logs innecesarios y preparar el entorno para ejecutar pruebas automatizadas.
   - Ejemplo:
     ```bash
     NODE_ENV=test mocha
     ```

---

### **Cómo usar `NODE_ENV` en Node.js**
Puedes acceder al valor de `NODE_ENV` mediante `process.env.NODE_ENV` en tu código. Esto permite condicionar el comportamiento de la aplicación según el entorno.

**Ejemplo**:
```javascript
if (process.env.NODE_ENV === 'development') {
    console.log('Modo desarrollo: habilitando herramientas de depuración.');
} else if (process.env.NODE_ENV === 'production') {
    console.log('Modo producción: optimizando el rendimiento.');
} else {
    console.log('Entorno no especificado, usando configuración predeterminada.');
}
```

---

### **Configuración de `NODE_ENV`**
1. **En sistemas Unix/Linux o macOS**:
   Puedes establecer `NODE_ENV` directamente en la línea de comandos:
   ```bash
   NODE_ENV=production node app.js
   ```

2. **En Windows**:
   Usa el comando `set` para definir la variable:
   ```cmd
   set NODE_ENV=production && node app.js
   ```

3. **Usando herramientas como `dotenv`**:
   Puedes definir `NODE_ENV` en un archivo `.env` para cargarlo automáticamente:
   ```env
   NODE_ENV=development
   ```
   Luego, usa la librería `dotenv` para cargar las variables:
   ```javascript
   require('dotenv').config();
   console.log(`El entorno actual es: ${process.env.NODE_ENV}`);
   ```

---

### **Beneficios de usar `NODE_ENV`**
1. **Optimización del rendimiento**:
   - En modo `production`, muchas librerías (como Express) deshabilitan características innecesarias, como el registro detallado de errores.
   - Ejemplo: Express verifica `NODE_ENV` para habilitar o deshabilitar el middleware de manejo de errores detallados.

2. **Configuraciones específicas por entorno**:
   - Puedes cargar configuraciones diferentes según el entorno.
   ```javascript
   const config = require(`./config.${process.env.NODE_ENV}.js`);
   ```

3. **Facilita el desarrollo y despliegue**:
   - Permite separar configuraciones de desarrollo, pruebas y producción, evitando errores al mover la aplicación entre entornos.

---

### **Conclusión**
`NODE_ENV` es una variable de entorno clave en Node.js que permite configurar el comportamiento de la aplicación según el entorno de ejecución. Usarla correctamente mejora la eficiencia, facilita el desarrollo y asegura que la aplicación esté optimizada para producción.

---

## Enumere las distintas características de sincronización de Node.js
Node.js es conocido por su modelo de ejecución **asíncrono y no bloqueante**, pero también proporciona características de sincronización para manejar tareas que requieren ejecución secuencial o control de concurrencia. A continuación, se enumeran las principales características de sincronización en Node.js:

---

### **1. Callbacks**
- **Descripción**: Los callbacks son funciones que se ejecutan después de que una operación asíncrona se completa.
- **Uso en sincronización**: Permiten ejecutar código en un orden específico al encadenar funciones.
- **Ejemplo**:
  ```javascript
  const fs = require('fs');

  fs.readFile('archivo.txt', 'utf8', (err, data) => {
      if (err) throw err;
      console.log('Contenido del archivo:', data);
  });
  ```

---

### **2. Promesas**
- **Descripción**: Las promesas son una forma más estructurada de manejar asincronía, permitiendo encadenar operaciones y manejar errores de manera más limpia.
- **Uso en sincronización**: Facilitan la ejecución secuencial de tareas asíncronas mediante `.then()` y `.catch()`.
- **Ejemplo**:
  ```javascript
  const fs = require('fs').promises;

  fs.readFile('archivo.txt', 'utf8')
      .then(data => console.log('Contenido del archivo:', data))
      .catch(err => console.error('Error:', err));
  ```

---

### **3. Async/Await**
- **Descripción**: `async/await` es una sintaxis moderna que permite escribir código asíncrono de manera más legible, como si fuera síncrono.
- **Uso en sincronización**: Garantiza que las operaciones asíncronas se ejecuten en el orden esperado.
- **Ejemplo**:
  ```javascript
  const fs = require('fs').promises;

  async function leerArchivo() {
      try {
          const data = await fs.readFile('archivo.txt', 'utf8');
          console.log('Contenido del archivo:', data);
      } catch (err) {
          console.error('Error:', err);
      }
  }

  leerArchivo();
  ```

---

### **4. Eventos y el EventEmitter**
- **Descripción**: Node.js utiliza el patrón de eventos para manejar la comunicación entre diferentes partes de una aplicación.
- **Uso en sincronización**: Permite coordinar tareas basadas en eventos personalizados.
- **Ejemplo**:
  ```javascript
  const EventEmitter = require('events');
  const emisor = new EventEmitter();

  emisor.on('evento', () => {
      console.log('Evento recibido');
  });

  emisor.emit('evento');
  ```

---

### **5. Temporizadores (`setTimeout`, `setInterval`, `setImmediate`)**
- **Descripción**: Los temporizadores permiten ejecutar código después de un intervalo de tiempo o en el siguiente ciclo del event loop.
- **Uso en sincronización**: Controlan cuándo se ejecutan ciertas tareas.
- **Ejemplo**:
  ```javascript
  console.log('Inicio');

  setTimeout(() => {
      console.log('Ejecutado después de 1 segundo');
  }, 1000);

  console.log('Fin');
  ```

---

### **6. Flujos (Streams)**
- **Descripción**: Los flujos son objetos que permiten leer o escribir datos de manera secuencial.
- **Uso en sincronización**: Facilitan el manejo de grandes cantidades de datos en fragmentos (chunks), sincronizando la lectura y escritura.
- **Ejemplo**:
  ```javascript
  const fs = require('fs');

  const flujoLectura = fs.createReadStream('archivo.txt', { encoding: 'utf8' });
  flujoLectura.on('data', (chunk) => {
      console.log('Fragmento recibido:', chunk);
  });
  ```

---

### **7. Mutexes y Semáforos (a través de librerías)**
- **Descripción**: Aunque Node.js no tiene soporte nativo para mutexes o semáforos, se pueden implementar mediante librerías externas para controlar el acceso concurrente a recursos compartidos.
- **Uso en sincronización**: Garantizan que solo una tarea acceda a un recurso a la vez.
- **Ejemplo** (usando la librería `async-mutex`):
  ```javascript
  const { Mutex } = require('async-mutex');
  const mutex = new Mutex();

  async function tareaCritica() {
      const release = await mutex.acquire();
      try {
          console.log('Accediendo al recurso compartido');
      } finally {
          release();
      }
  }

  tareaCritica();
  ```

---

### **8. Worker Threads**
- **Descripción**: Los hilos de trabajo permiten ejecutar tareas intensivas de CPU en paralelo sin bloquear el event loop.
- **Uso en sincronización**: Sincronizan la comunicación entre el hilo principal y los hilos de trabajo.
- **Ejemplo**:
  ```javascript
  const { Worker } = require('worker_threads');

  const worker = new Worker('./worker.js');
  worker.on('message', (message) => {
      console.log('Mensaje del worker:', message);
  });
  worker.postMessage('Iniciar tarea');
  ```

---

### **9. `process.nextTick()`**
- **Descripción**: Permite ejecutar una función en la siguiente iteración del event loop, antes de que se procesen otras tareas asíncronas.
- **Uso en sincronización**: Útil para priorizar tareas.
- **Ejemplo**:
  ```javascript
  console.log('Inicio');

  process.nextTick(() => {
      console.log('Ejecutado en el siguiente ciclo del event loop');
  });

  console.log('Fin');
  ```

---

### **10. Promesas combinadas (`Promise.all`, `Promise.race`, etc.)**
- **Descripción**: Métodos para manejar múltiples promesas simultáneamente.
- **Uso en sincronización**: Sincronizan la ejecución de varias tareas asíncronas.
- **Ejemplo**:
  ```javascript
  const promesa1 = Promise.resolve('Tarea 1 completada');
  const promesa2 = Promise.resolve('Tarea 2 completada');

  Promise.all([promesa1, promesa2]).then((resultados) => {
      console.log(resultados);
  });
  ```

---

### **Conclusión**
Node.js ofrece varias características de sincronización, desde callbacks y promesas hasta herramientas más avanzadas como `Worker Threads` y librerías externas para mutexes. Estas herramientas permiten manejar tanto tareas asíncronas como sincronizar operaciones críticas de manera eficiente.

---
## ¿Qué es WASI y por qué se está introduciendo?

En el contexto de **Node.js**, **WASI** (WebAssembly System Interface) se está introduciendo para permitir que los módulos de **WebAssembly (Wasm)** interactúen con el sistema operativo de manera segura y eficiente, ampliando las capacidades de WebAssembly dentro del ecosistema de Node.js.

---

### **¿Qué es WASI en Node.js?**
WASI en Node.js es una interfaz que permite ejecutar módulos WebAssembly con acceso controlado a recursos del sistema, como el sistema de archivos, la red y otros servicios del sistema operativo. Node.js incluye soporte para WASI a través del módulo integrado `wasi`, que facilita la ejecución de módulos Wasm en un entorno compatible con WASI.

---

### **¿Por qué se introduce WASI en Node.js?**

1. **Extender WebAssembly más allá del navegador**:
   - WASI permite que los módulos Wasm se ejecuten en Node.js, lo que abre la puerta a casos de uso como herramientas CLI, procesamiento de datos y aplicaciones de servidor.

2. **Portabilidad**:
   - Los módulos Wasm con WASI pueden ejecutarse en cualquier entorno compatible con WASI, incluido Node.js, sin necesidad de modificar el código.

3. **Seguridad**:
   - WASI utiliza un modelo de seguridad basado en capacidades, lo que significa que los módulos Wasm solo tienen acceso a los recursos explícitamente otorgados, como un directorio específico o un archivo.

4. **Ecosistema más amplio**:
   - WASI en Node.js permite integrar módulos Wasm en aplicaciones Node.js, combinando la eficiencia de WebAssembly con la flexibilidad de Node.js.

5. **Rendimiento**:
   - WebAssembly es conocido por su alto rendimiento, y WASI permite aprovechar esta ventaja en aplicaciones Node.js para tareas intensivas de CPU o procesamiento de datos.

---

### **Ejemplo de uso de WASI en Node.js**

1. **Instalar un módulo Wasm compatible con WASI**:
   Supongamos que tienes un módulo Wasm que realiza cálculos matemáticos.

2. **Código en Node.js para ejecutar el módulo Wasm con WASI**:
   ```javascript
   const fs = require('fs');
   const { WASI } = require('wasi');

   // Crear una instancia de WASI
   const wasi = new WASI({
       args: process.argv,
       env: process.env,
       preopens: {
           '/sandbox': './sandbox' // Directorio accesible para el módulo Wasm
       }
   });

   // Cargar el módulo Wasm
   const wasmBuffer = fs.readFileSync('./modulo.wasm');
   const wasmModule = new WebAssembly.Module(wasmBuffer);

   // Crear una instancia de WebAssembly con WASI
   const instance = new WebAssembly.Instance(wasmModule, {
       wasi_snapshot_preview1: wasi.wasiImport
   });

   // Iniciar el módulo Wasm
   wasi.start(instance);
   ```

   En este ejemplo:
   - Se crea una instancia de WASI con acceso limitado al directorio `./sandbox`.
   - Se carga un módulo Wasm y se ejecuta en un entorno seguro dentro de Node.js.

---

### **Ventajas de WASI en Node.js**

1. **Integración con el ecosistema Node.js**:
   - WASI permite combinar la potencia de WebAssembly con las capacidades de Node.js, como el acceso a módulos npm y APIs del sistema.

2. **Seguridad**:
   - WASI restringe el acceso de los módulos Wasm a recursos específicos, proporcionando un entorno aislado y seguro.

3. **Portabilidad**:
   - Los módulos Wasm con WASI pueden ejecutarse en cualquier entorno compatible, incluido Node.js, sin necesidad de cambios.

4. **Rendimiento**:
   - WebAssembly es ideal para tareas intensivas de CPU, y WASI permite aprovechar este rendimiento en aplicaciones Node.js.

---

### **Casos de uso de WASI en Node.js**

1. **Herramientas CLI**:
   - Crear herramientas de línea de comandos que utilicen módulos Wasm para cálculos rápidos y portables.

2. **Procesamiento de datos**:
   - Usar WebAssembly para tareas intensivas de CPU, como procesamiento de imágenes o cálculos matemáticos complejos.

3. **Aplicaciones de servidor**:
   - Integrar módulos Wasm en aplicaciones Node.js para mejorar el rendimiento en tareas específicas.

4. **Entornos aislados**:
   - Ejecutar código de terceros en un entorno seguro y controlado mediante WASI.

---

### **Conclusión**
WASI en Node.js amplía las capacidades de WebAssembly al permitir que los módulos Wasm interactúen con el sistema operativo de manera segura y eficiente. Esto abre nuevas posibilidades para combinar el rendimiento de WebAssembly con la flexibilidad y el ecosistema de Node.js, haciendo que sea una herramienta poderosa para aplicaciones modernas.

---

## ¿Qué son las versiones LTS de Node.js?
LTS significa soporte a largo plazo. Las versiones LTS de Node.js reciben soporte durante un periodo prolongado, normalmente 30 meses desde su lanzamiento. Estas versiones suelen ser más estables y fiables que las versiones no LTS y se recomiendan para producción.


---

## ¿Qué es el Event Loop en Node.js?
**El Event Loop de Node.js** es el mecanismo que permite a Node manejar operaciones asíncronas de manera no bloqueante. Está basado en la arquitectura de libuv, una biblioteca C que proporciona un loop de eventos multiplataforma.


### **Índice de las partes del Event Loop en Node.js**
1. **Call Stack (Pila de llamadas)**  
   - Donde se ejecuta el código sincrónico.
   
2. **Node APIs y libuv**  
   - Manejan operaciones asíncronas como temporizadores, E/S, y más.

3. **Callback Queue (Cola de tareas)**  
   - Donde se colocan las tareas asíncronas listas para ejecutarse.

4. **Microtask Queue (Cola de Microtareas)**  
   - Cola de tareas de alta prioridad como `Promise.then` y `process.nextTick`.

5. **Fases del Event Loop**  
   - **Timers**: Maneja `setTimeout` y `setInterval`.
   - **Callbacks**: Maneja callbacks de operaciones asíncronas como E/S.
   - **Poll**: Procesa operaciones de E/S pendientes.
   - **Check**: Maneja `setImmediate`.
   - **Close Callbacks**: Maneja eventos de cierre como `socket.on('close')`.

---

### **1. Call Stack (Pila de llamadas)**

**Concepto**:  
El **Call Stack** es donde se ejecuta el código sincrónico. Cada vez que llamas a una función, esta se agrega al Call Stack. Cuando termina, se elimina.

**Ejemplo**:
```javascript
function primera() {
    console.log("Primera función");
    segunda();
}

function segunda() {
    console.log("Segunda función");
}

primera();
console.log("Fin del programa");
```

**Salida**:
```
Primera función
Segunda función
Fin del programa
```

**Explicación**:
1. `primera()` se agrega al Call Stack y se ejecuta.
2. Dentro de `primera()`, se llama a `segunda()`, que también se agrega al Call Stack.
3. Cuando `segunda()` termina, se elimina del Call Stack.
4. Finalmente, `console.log("Fin del programa")` se ejecuta.

---

### **2. Node APIs y libuv**

**Concepto**:  
Node.js utiliza **libuv**, una biblioteca que maneja operaciones asíncronas como temporizadores, E/S, y más. Estas operaciones se delegan a las APIs de Node y se procesan fuera del Call Stack.

**Ejemplo**:
```javascript
console.log("Inicio");

setTimeout(() => {
    console.log("setTimeout ejecutado");
}, 1000);

console.log("Fin");
```

**Explicación**:
1. `console.log("Inicio")` y `console.log("Fin")` se ejecutan en el Call Stack.
2. `setTimeout` delega su callback a las APIs de Node y se procesa en **libuv**.
3. Después de 1 segundo, el callback de `setTimeout` se coloca en la **Callback Queue**.

---

### **3. Callback Queue (Cola de tareas)**

**Concepto**:  
La **Callback Queue** almacena las tareas asíncronas listas para ejecutarse, como los callbacks de `setTimeout` o `setInterval`. El Event Loop mueve estas tareas al Call Stack cuando está vacío.

**Ejemplo**:
```javascript
console.log("Inicio");

setTimeout(() => {
    console.log("Callback de setTimeout");
}, 0);

console.log("Fin");
```

**Salida**:
```
Inicio
Fin
Callback de setTimeout
```

**Explicación**:
1. `console.log("Inicio")` y `console.log("Fin")` se ejecutan primero.
2. El callback de `setTimeout` se coloca en la **Callback Queue** y se ejecuta después de que el Call Stack esté vacío.

---

### **4. Microtask Queue (Cola de Microtareas)**

**Concepto**:  
La **Microtask Queue** tiene tareas de alta prioridad como `Promise.then` y `process.nextTick`. Estas tareas se ejecutan antes de las tareas en la Callback Queue.

**Ejemplo**:
```javascript
console.log("Inicio");

setTimeout(() => {
    console.log("Callback de setTimeout");
}, 0);

Promise.resolve().then(() => {
    console.log("Microtask: Promise.then");
});

process.nextTick(() => {
    console.log("Microtask: process.nextTick");
});

console.log("Fin");
```

**Salida**:
```
Inicio
Fin
Microtask: process.nextTick
Microtask: Promise.then
Callback de setTimeout
```

**Explicación**:
1. `console.log("Inicio")` y `console.log("Fin")` se ejecutan primero.
2. `process.nextTick` y `Promise.then` se ejecutan antes que el callback de `setTimeout` porque están en la **Microtask Queue**.

---

### **5. Fases del Event Loop**

#### **Fase 1: Timers**
Maneja los callbacks de `setTimeout` y `setInterval`.

**Ejemplo**:
```javascript
setTimeout(() => {
    console.log("Fase de Timers: setTimeout");
}, 1000);
```

---

#### **Fase 2: Callbacks**
Maneja los callbacks de operaciones asíncronas como E/S.

**Ejemplo**:
```javascript
const fs = require("fs");

fs.readFile("archivo.txt", "utf8", (err, data) => {
    if (err) throw err;
    console.log("Fase de Callbacks: Lectura de archivo completada");
});
```

---

#### **Fase 3: Poll**
Procesa operaciones de E/S pendientes y espera nuevas tareas.

**Ejemplo**:
```javascript
const fs = require("fs");

fs.readFile("archivo.txt", "utf8", (err, data) => {
    if (err) throw err;
    console.log("Fase de Poll: Lectura de archivo completada");
});

setTimeout(() => {
    console.log("Fase de Timers: setTimeout");
}, 0);
```

---

#### **Fase 4: Check**
Maneja los callbacks de `setImmediate`.

**Ejemplo**:
```javascript
setImmediate(() => {
    console.log("Fase de Check: setImmediate");
});
```

---

#### **Fase 5: Close Callbacks**
Maneja eventos de cierre como `socket.on('close')`.

**Ejemplo**:
```javascript
const net = require("net");

const server = net.createServer((socket) => {
    socket.end("Conexión cerrada");
});

server.listen(8080, () => {
    console.log("Servidor escuchando en el puerto 8080");
});

server.on("close", () => {
    console.log("Fase de Close Callbacks: Servidor cerrado");
});

server.close();
```

---

### **Resumen del flujo del Event Loop**

1. Ejecuta el código sincrónico en el **Call Stack**.
2. Procesa las **Microtasks** (`Promise.then`, `process.nextTick`).
3. Procesa las tareas en la fase de **Timers** (`setTimeout`, `setInterval`).
4. Procesa las tareas en la fase de **Callbacks** (operaciones de E/S).
5. Procesa las tareas en la fase de **Poll** (espera de E/S).
6. Procesa las tareas en la fase de **Check** (`setImmediate`).
7. Procesa las tareas en la fase de **Close Callbacks** (eventos de cierre).

---

### **Ejemplo completo del Event Loop**

```javascript
console.log("Inicio");

setTimeout(() => {
    console.log("Fase de Timers: setTimeout");
}, 0);

setImmediate(() => {
    console.log("Fase de Check: setImmediate");
});

Promise.resolve().then(() => {
    console.log("Microtask: Promise.then");
});

process.nextTick(() => {
    console.log("Microtask: process.nextTick");
});

console.log("Fin");
```

**Salida**:
```
Inicio
Fin
Microtask: process.nextTick
Microtask: Promise.then
Fase de Timers: setTimeout
Fase de Check: setImmediate
```

---

### **Conclusión**
El Event Loop en Node.js es el núcleo de su modelo asíncrono. Entender cómo funcionan sus partes (Call Stack, libuv, Microtask Queue, Callback Queue) y las fases del Event Loop te permitirá escribir código más eficiente y predecible.


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

## ¿Qué es morgan en Node.js?
 morgan es un middleware que se usa para registrar las solicitudes HTTP en el servidor.

 ```js
const morgan = require('morgan');
app.use(morgan('dev'));  // Registra las solicitudes HTTP en formato de desarrollo

```


## helmet

**Helmet** es un middleware de seguridad para aplicaciones **Express.js** que ayuda a protegerlas configurando encabezados HTTP de manera adecuada. Su objetivo principal es reducir las vulnerabilidades comunes relacionadas con los encabezados HTTP, como ataques de **Cross-Site Scripting (XSS)**, **Clickjacking**, y **Inyección de código**.

---

### Características principales:
1. **Protección contra XSS**: Configura encabezados para evitar la ejecución de scripts maliciosos.
2. **Prevención de Clickjacking**: Usa el encabezado `X-Frame-Options` para evitar que tu sitio sea incrustado en iframes.
3. **Ocultación de tecnología**: Elimina el encabezado `X-Powered-By` para no revelar que tu aplicación usa Express.
4. **Control de caché**: Configura encabezados para manejar el almacenamiento en caché.
5. **Configuración modular**: Puedes habilitar o deshabilitar protecciones específicas según tus necesidades.

---

### Instalación:
Para usar Helmet, primero instálalo con **npm**:

```bash
npm install helmet
```

---

### Uso básico:
```js
const express = require('express');
const helmet = require('helmet');

const app = express();

// Usar Helmet para proteger la aplicación
app.use(helmet());

app.get('/', (req, res) => {
  res.send('Hola, mundo seguro!');
});

app.listen(3000, () => {
  console.log('Servidor ejecutándose en http://localhost:3000');
});
```

---

### Funcionalidades específicas:
Helmet incluye varias protecciones que puedes habilitar o deshabilitar según tus necesidades:

1. **`helmet.hidePoweredBy()`**:
   - Elimina el encabezado `X-Powered-By` para no revelar que usas Express.
   ```js
   app.use(helmet.hidePoweredBy());
   ```

2. **`helmet.frameguard()`**:
   - Previene ataques de Clickjacking configurando el encabezado `X-Frame-Options`.
   ```js
   app.use(helmet.frameguard({ action: 'deny' }));
   ```

3. **`helmet.xssFilter()`**:
   - Habilita el filtro XSS en navegadores antiguos.
   ```js
   app.use(helmet.xssFilter());
   ```

4. **`helmet.noSniff()`**:
   - Previene que los navegadores intenten adivinar el tipo de contenido.
   ```js
   app.use(helmet.noSniff());
   ```

5. **`helmet.hsts()`**:
   - Habilita HTTP Strict Transport Security (HSTS) para forzar conexiones HTTPS.
   ```js
   app.use(helmet.hsts({ maxAge: 31536000 })); // 1 año
   ```

6. **`helmet.contentSecurityPolicy()`**:
   - Configura una política de seguridad de contenido (CSP) para controlar qué recursos pueden cargarse.
   ```js
   app.use(
     helmet.contentSecurityPolicy({
       directives: {
         defaultSrc: ["'self'"],
         scriptSrc: ["'self'", "'unsafe-inline'"],
       },
     })
   );
   ```

---

### Configuración avanzada:
Puedes personalizar Helmet habilitando o deshabilitando protecciones específicas:

```js
app.use(
  helmet({
    contentSecurityPolicy: false, // Deshabilitar CSP
    frameguard: { action: 'sameorigin' }, // Permitir iframes del mismo origen
  })
);
```

---

### Resumen:
- **Helmet** es un middleware de seguridad para Express.js que protege tu aplicación configurando encabezados HTTP.
- Es fácil de usar y modular, lo que te permite habilitar o deshabilitar protecciones según tus necesidades.
- Es una herramienta esencial para mejorar la seguridad de aplicaciones web en Node.js.


##  ¿Qué es req.body en Express?
req.body contiene los datos enviados en el cuerpo de una solicitud HTTP POST o PUT. Para acceder a él, es necesario usar middleware como express.json() o express.urlencoded().

```js
app.use(express.json());  // Middleware para analizar JSON

app.post('/data', (req, res) => {
  console.log(req.body);  // Muestra los datos del cuerpo de la solicitud
  res.send('Datos recibidos');
});

```

## ¿Qué es req.query en Express?
req.query es un objeto que contiene los parámetros de la cadena de consulta (query string) de la URL en una solicitud GET.

```js
app.get('/saludo', (req, res) => {
  console.log(req.query.nombre);  // Muestra el valor del parámetro 'nombre' en la URL
  res.send(`Hola, ${req.query.nombre}`);
});
```

## ¿Qué es req.params en Express?
req.params contiene los parámetros de ruta definidos en las rutas dinámicas de Express.

```js
app.get('/usuario/:id', (req, res) => {
  console.log(req.params.id);  // Muestra el valor del parámetro 'id' de la ruta
  res.send(`Usuario con ID: ${req.params.id}`);
});

```

## ¿Qué es res.send() en Express?
res.send() se usa para enviar una respuesta al cliente. Puede ser un texto, un objeto o un buffer.

```js
app.get('/', (req, res) => {
  res.send('Hola Mundo');
});

```

 ¿Qué es res.json() en Express?
res.json() se utiliza para enviar una respuesta JSON al cliente.
```js
app.get('/usuario', (req, res) => {
  res.json({ nombre: 'Juan', edad: 25 });
});

```

## ¿Cómo utilizar console.time() y console.timeEnd()?
console.time() y console.timeEnd() se usan para medir el tiempo de ejecución de un bloque de código.

```js
console.time('miTiempo');

setTimeout(() => {
  console.timeEnd('miTiempo');  // Muestra el tiempo que pasó desde 'miTiempo'
}, 1000);
```

## ¿Cómo manejar múltiples versiones de una API en Express?
Puedes manejar diferentes versiones de una API utilizando rutas con prefijos que representan la versión.

```js
app.get('/v1/usuario', (req, res) => {
  res.send('Versión 1 de la API');
});

app.get('/v2/usuario', (req, res) => {
  res.send('Versión 2 de la API');
});
```
