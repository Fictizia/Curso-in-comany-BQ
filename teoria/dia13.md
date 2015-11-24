### Nodejs
![Node_logo](https://nodejs.org/static/images/logos/nodejs.png)

- Versiones:
  - Pares -> Estables
  - Impares -> inestables

- Comprobar version:
  - Node
```
    node -v
```

  - Npm
```
    npm -v
```


**NPM**

![npm_logo](http://ohdoylerules.com/content/images/npm-logo.svg)

- Instalar paquetes:
  - global:
```
    npm install -g <paquete>
```  

  - local:
```
    npm install <paquete>
```    


- Instalando versiones especificas:

  - la más reciente:
```  
    npm install <paquete>@latest
```  
  
  - versión especifica:
```  
    npm install <paquete>@1.x (1.xx.xx)
```
  
  - Otra versión especifica
```
    npm install <paquete>@2.10.x (2.10.x)
```

- Paquetes desactualziados:
```
  npm outdated
```
  
- Actualizando paquetes:
```
  npm update <paquete>
```

Desinstalando paquete:
```
  npm uninstall <paquete>
```


**package.json**

- Datos proyecto
- Tareas
- Dependencias (dependencies y devDependencies)

- Dependency Hell:
  - [Nodei.co](https://nodei.co/)
  - [Dependency Hell](http://www.wikiwand.com/en/Dependency_hell)
  - [David Dm](https://david-dm.org/)
    - [Ejemplo Twitter-sentiments](https://david-dm.org/UlisesGascon/twitter-sentiments#info=dependencies&view=list)
    - [Ejemplo Grunt](https://david-dm.org/gruntjs/grunt#info=dependencies&view=table)
    - [Ejemplo Express](https://david-dm.org/strongloop/express)
    - [Ejemplo Bower](https://david-dm.org/bower/bower#info=dependencies&view=table)
  - [ShieldsIO](http://shields.io/)
    - [Your Badge Service](http://badges.github.io/gh-badges/) 

Seguridad:
  - [Seguridad](https://nodesecurity.io/resources)
  - [Seguridad Avisos](https://nodesecurity.io/advisories)


- Creación:
```
  npm init
```
  
  
Guardar nuevas dependencias:
```
 npm install <paquete> —save
```
Guardar nuevas dependencias (solo para entorno desarrollo):
```
 npm install <paquete> —save -dev
```


Guardando versiones especificas:
  - (1.xx.xx):
```
  npm install —save <paquete>@1.x
```
  
  - (2.10.x)
```
  npm install —save <paquete>@2.10.x
```
  
  - Latest
```
  npm install —save <paquete>@lastest
```
  
Quitando dependencias:
```
  npm uninstall <paquete> —save
```
  
Instalamos las dependencias en el proyecto:
  - todo:
```
  npm install (todo)
```
  
  - Solo production:
```
  npm install —production (solo producción)
```
  
  - Solo development:
```
  npm install —dev
```


**npm scripts (comandos de CLI):**

- Añadiendo comandos:

```javascript
  // ...
  "scripts": {
      "test": "npm -v",
      "start": "node -v",
      "hola": "echo 'Hola mundo!'"
  }
  // ...
```
- Mostrando todos los comandos:
```
    npm run
```

- Ejecutando comandos:
  - test
```
    npm test
```

  - start
```
    npm start
```

  - hola
```
    npm run hola
```  

**Ejercicio**

1 - Crearemos varios scripts para automatizar tareas.
    - Verificador de versiones para NPM y Nodejs
    - Verificador del status de Git
    - Descargar (Clonar) Bootstrap de Github
    - Descargar (Clonar) nuestro curso de Github
    - Emoji al azar con [emoji-random](https://www.npmjs.com/package/emoji-random)

```javascript
    // Tu solución
```


**NVM  (manejando varias versiones de Node):**

- Comrpobando la version de NVM:
```
    nvm --version
```

- Instalando una version:
```
    nvm install 0.12
```

- Desinstalando una version:
```
    nvm uninstall 0.12
```

- Usar una version (globalmente):
```
  nvm use 0.12
```
  
- Usando versiones (por proyecto):
```
    echo 0.12 > .nvmrc
```
  
```
    nvm use
```

**Hello World**

- Hola mundo!:
```javascript
  console.log("Hola Mundo!");
```

- Hola mundo! (retraso):
```javascript
  setTimeour(function() {
    console.log("Hola Futuro...!");
  }, 5000);
```

- Hola mundo! (repetición):
```javascript
  setInterval(function() {
    console.log("Hola Futuro...!");
  }, 1000);
```

**HTTP**

- Hello World con HTTP:
```javascript
  var http = require('http');
  
  var puerto = 3000;
  var direccion = "127.0.0.1";
  var mensaje = 'Hola a todos, ahora usando HTTP\n';
  
  
  http.createServer(function (req, res) {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end(mensaje);
  }).listen(puerto, direccion);
  console.log('Server running at http://'+direccion+':'+puerto+'/');
```

- Hello World desde c9.io:
```javascript
  var http = require('http');
  
  var mensaje = 'Hola a todos, ahora usando HTTP con C9.io\n';
  
  http.createServer(function(req, res) {
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.end(mensaje);
  }).listen(process.env.PORT, process.env.IP);
  
  console.log('Server running at http://'+process.env.IP+':'+process.env.PORT+'/');
```

- Rediccionamiento:
```javascript
  var http = require('http');
  
  http.createServer(function (req, res) {
    res.writeHead(301, {
      'Location': 'http://www.google.es/'
    });
      res.end();
  }).listen(process.env.PORT, process.env.IP);
  
  console.log('Servidor funcionando en http://'+process.env.IP+':'+process.env.PORT+'/');
```

**URL**

- Leyendo urls:
```javascript
  var url = require('url');
  
  var demoURL = "http://localhost:3000/ruta?parametro=dato#detalle";
  
  console.log("El host: "+url.parse(demoURL).hostname);
  console.log("El puerto: "+url.parse(demoURL).port);
  console.log("La ruta: "+url.parse(demoURL).pathname);
  console.log("La parametro: "+url.parse(demoURL).query);
  console.log("El hash(#): "+url.parse(demoURL).hash);
```

- Trabajando con rutas:
```javascript
  var http = require('http'),
      url = require('url');

  http.createServer(function (req, res) {
    var pathname = url.parse(req.url).pathname;
  
    if (pathname === '/') {
        res.writeHead(200, {
        'Content-Type': 'text/plain'
      });
      res.end('Index!');
      
    } else if (pathname === '/otro') {
        res.writeHead(200, {
        'Content-Type': 'text/plain; charset=utf-8'
      });
      res.end('sencillamente otra página');
      
  
    } else if (pathname === '/alindex') {
        res.writeHead(301, {
        'Location': '/'
      });
      res.end();    
      
    } else {
        res.writeHead(404, {
        'Content-Type': 'text/plain'
      });
      res.end('Querido... 404!');
    }
    
  }).listen(process.env.PORT, process.env.IP);
  
  console.log('Servidor funcionando en http://'+process.env.IP+':'+process.env.PORT+'/');
```


**Ejercicios**

2 - Crea las rutas básicas para tener una página web clásica (¿Quienes somos? | ¿Donde Estamos? | ¿Que hacemos? | Contacto... etc...)

```javascript
    // Tu solución
```


**Leer/Escribir Ficheros**

- Leer un archivo:
```javascript
  var fs = require('fs');
  fs.readFile('archivo.txt', 'utf8', function (err, data) {
      if (!err) {
        console.log(data);
      } else {
        throw err;
      }
  });
```

- Escribir un archivo:
```javascript
  var fs = require('fs'),
      data = "y esto... se guardará en el archivo.txt";
  fs.writeFile('archivo.txt', data, function (err) {
    if (!err) {
      console.log('Datos guardados en el archivo.txt');
    } else {
      throw err;
    }
  });
```



**Eventos**

- Ejemplo sencillo:
```javascript
  var eventos = require('events');
  
  var EmisorEventos = eventos.EventEmitter; 
  var ee = new EmisorEventos(); 
  ee.on('datos', function(fecha){ 
     console.log(fecha); 
  }); 
  setInterval(function(){ 
     ee.emit('datos', Date.now()); 
  }, 500);
```


**Ping**

- Ping (petición http):
  ```javascript
    var url = "google.es";
    
    http.get({ host: url }, function(resOrigen) {
    
        http.createServer(function (req, res) {
           
            res.writeHead(200, {'Content-Type': 'text/plain'});
            res.end("La respuesta de " +url+" es "+resOrigen.statusCode );
            console.log("La respuesta de " +url+" es "+resOrigen.statusCode );
    
        }).listen(process.env.PORT, process.env.IP);
        
        console.log('Servidor disponible en http://'+process.env.IP+':'+process.env.PORT+'/');
    
    
    }).on('error', function(e) {
        
        http.createServer(function (req, res) {
           
            res.writeHead(200, {'Content-Type': 'text/plain'});
            res.end("La respuesta de " +url+" genera un error - " + e.message  );
    
        }).listen(process.env.PORT, process.env.IP);
        
        console.log('Servidor disponible en http://'+process.env.IP+':'+process.env.PORT+'/');
        console.log("Tenemos un error!! - " + e.message);
    });
  ```
- Ping recurrente (consola):
  ```
      var http = require('http');
      var url = "google.es";
      var tiempo = 3500;
      
      setInterval(function() {
          http.get({ host: url }, function(res) {
              if (res.statusCode === 200 ) {  
                  console.log("Sin errores en " +url);
              } else {
                  console.log("Respuesta Http "+res.statusCode+" en " +url);
              }    
          }).on('error', function(e) {
                  console.log("Con errores -> La respuesta de "+url+" es "+e.message  );
          });
      }, tiempo);
  ```
  
**Asincronía**:

> El modelo de programación de Node.js es monohilo, asíncrono y dirigido por eventos. 
1. No puede haber código bloqueante o todo el servidor quedará bloqueado y esto incluye no responder a nuevas peticiones entrantes.
2. La asincronicidad implica que no sabemos cuándo ni en que orden se va a ejecutar el código, generalmente esto no es importante pero en ocasiones sí lo es y habrá que tenerlo en cuenta.
3. En caso de error inesperado debemos capturarlo y controlar el posible estado en que haya podido quedar la ejecución del código.
> Nicolas Nombela en [nnombela](http://nnombela.com/blog/2012/03/21/asincronicidad-en-node-dot-js/)

- Sincrónico - código bloqueante:

  ```
    var http = require("http");
    var util = require("util");
    var numeroPeticion = 1
    
    function writeResponse(response) {
        response.writeHead(200, {"Content-Type": "text/plain"});
        response.write("Hola Mundo!, numero de peticion "+numeroPeticion);
        response.end();
        util.log("Se termino... "+numeroPeticion);
    }
    
    function sleepSynch(seconds, response) {
        var startTime = new Date().getTime();
        while (new Date().getTime() < startTime + Math.floor((Math.random() * 1000) + 500) * seconds) {
            // Nada pasa....
        }
        writeResponse(response);
    }
    
    http.createServer(function(request, response) {
        util.log("Empezo... "+numeroPeticion);
        sleepSynch(10, response);
        numeroPeticion++;
    }).listen(process.env.PORT);
    
    console.log("en puerto ->" + process.env.PORT);
  ```

- Asincronico - timeOut()

  ```
    var http = require("http");
    var util = require("util");

    function writeResponse(response) {
        response.writeHead(200, {"Content-Type": "text/plain"});
        response.write("Hola Mundo!");
        response.end();
        util.log("Se termino... ");
    }

    function sleepAsynch(seconds, response) {
        setTimeout(function() {
        writeResponse(response);
        }, Math.floor((Math.random() * 1000) + 100) * seconds);
    }

    http.createServer(function(request, response) {

        util.log("Empezo... ");
        sleepAsynch(10, response);
    }).listen(process.env.PORT);
    
    console.log("en puerto ->" + process.env.PORT);
  ```


**Process & Child Process**

- process.argv:
  ```
  console.log(process.argv)
  /*
  1. ubicacion de node (bin)
  2. ubicación del script (location)
  3. [Otros parametros]
  */
  
  ```


- console.log("Hola"):
```
  var mensaje = "Hola"
  process.stdout.write(mensaje + '\n')
```

- Mantener Node funcionando:

  -  Se cierra:
  ```
  setTimeout(function (){
    process.stdout.write("Cerrando Node...")
  }, 1000)
  ```

  - Se mantiene:
  ```
  setInterval(function (){
    // Nada pasa... pero sigo funcionando
  }, 1000)
  ```
  
  - Programando una salida:
   ```
  var contador = 0
  setInterval(function (){
    contador++
    if(contador > 10){
      process.exit()
    } else {
    process.stdout.write("Sigo. Valor contador -> "+contador +"\n")
    }
  }, 1000);
  ``` 

- Romper con el proceso único (recomendado para procesos inestables o con mucha carga):
```
  var exec = require('child_process').exec

  // cat solo funciona en UNIX
  exec('cat texto.txt', function (err, stdout, stderr) {
    if(!err){  
        console.log('El contenido de nuestro archivo', stdout)
    } else {
        console.log('Error: '+err)
    }
  })
```

- Manejando hijos:
```
  var spawn = require('child_process').spawn

  if(process.argv[2] === 'hijo'){
    console.log('Estoy dentro del proceso hijo');
  } else {
    var hijo = spawn(process.execPath, [__filename, 'hijo'])
    hijo.stdout.pipe(process.stdout)
  }

```

- Manejando hijos (con heréncia):
```
  var spawn = require('child_process').spawn

  if(process.argv[2] === 'hijo'){
    console.log('Estoy dentro del proceso hijo');
  } else {
    var hijo = spawn(process.execPath, [__filename, 'hijo'], {
      stdio: 'inherit'
    })
  }

```

- Manejando hijos (contexto común):
```
  var spawn = require('child_process').spawn;

  var contador = 0;
  contador += 1;

  if(process.argv[2] === 'hijo'){
    console.log('hijo', contador);
    contador++;
    console.log('pero.. además el hijo.. suma otra! y son', contador);
  } else {
    var hijo = spawn(process.execPath, [__filename, 'hijo'], {
      stdio: 'inherit'
    });
    console.log('padre', contador);
  }

```

**Require**

- Exportar los datos:
```javascript
var config = {
	token: "<--- MiSecreto--->",
};

module.exports = config;
```

- Importar los datos:
```javascript
config = require('./config');

console.log(config.token);
```

**Ejercicio**

3 - Esta [aplicación](https://github.com/UlisesGascon/raspberrypi-system-info-data-to-firebase) necesita una revisión.

- Objetivos:
  - Mejorar la compatibilidad entre plataformas (Mac, c9 y Windows)
  - Optimización de Firebase
  - Eliminar código redundante

- Opcional:
  - Puedes realizar un pull-request con las mejoras ;-) 

```javascript
    // Tu solución
```