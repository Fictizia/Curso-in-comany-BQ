### Bower

![Bower Logo](http://image.slidesharecdn.com/bower-phxjs-140515152011-phpapp02/95/bower-phoenix-javascript-meetup-1-638.jpg?cb=1400167728)

> Web sites are made of lots of things — frameworks, libraries, assets, utilities, and rainbows. Bower manages all these things for you.

- [Bower](http://bower.io/)
- [Tendencias Bower](http://bower.io/stats/)
- [Buscador Bower](http://bower.io/search/)


**Bower**
Instalamos Bower globalmente

```
  sudo npm install -g bower
```

Dependencias
```
  /home/ubuntu/.nvm/versions/node/v4.1.1/bin/bower -> /home/ubuntu/.nvm/versions/node/v4.1.1/lib/node_modules/bower/bin/bower
  bower@1.6.6 /home/ubuntu/.nvm/versions/node/v4.1.1/lib/node_modules/bower
  ├── is-root@1.0.0
  ├── destroy@1.0.3
  ├── stringify-object@1.0.1
  ├── junk@1.0.2
  ├── chmodr@1.0.2
  ├── user-home@1.1.1
  ├── q@1.4.1
  ├── abbrev@1.0.7
  ├── opn@1.0.2
  ├── bower-endpoint-parser@0.2.2
  ├── bower-logger@0.2.2
  ├── lockfile@1.0.1
  ├── archy@1.0.0
  ├── graceful-fs@3.0.8
  ├── nopt@3.0.6
  ├── lru-cache@2.7.3
  ├── retry@0.6.1
  ├── tmp@0.0.24
  ├── semver@2.3.2
  ├── md5-hex@1.1.0 (md5-o-matic@0.1.1)
  ├── fs-write-stream-atomic@1.0.4 (graceful-fs@4.1.2)
  ├── p-throttler@0.1.1 (q@0.9.7)
  ├── request-progress@0.3.1 (throttleit@0.0.2)
  ├── shell-quote@1.4.3 (array-filter@0.0.1, array-reduce@0.0.0, jsonify@0.0.0, array-map@0.0.0)
  ├── chalk@1.1.1 (escape-string-regexp@1.0.3, supports-color@2.0.0, ansi-styles@2.1.0, strip-ansi@3.0.0, has-ansi@2.0.0)
  ├── bower-json@0.4.0 (intersect@0.0.3, deep-extend@0.2.11, graceful-fs@2.0.3)
  ├── promptly@0.2.0 (read@1.0.7)
  ├── fstream@1.0.8 (inherits@2.0.1, graceful-fs@4.1.2)
  ├── which@1.2.0 (is-absolute@0.1.7)
  ├── bower-registry-client@1.0.0 (async@0.2.10, graceful-fs@4.1.2, request-replay@0.2.0, mkdirp@0.3.5)
  ├── mkdirp@0.5.0 (minimist@0.0.8)
  ├── glob@4.5.3 (inherits@2.0.1, inflight@1.0.4, once@1.3.3, minimatch@2.0.10)
  ├── fstream-ignore@1.0.3 (inherits@2.0.1, minimatch@3.0.0)
  ├── rimraf@2.4.4 (glob@5.0.15)
  ├── insight@0.7.0 (object-assign@4.0.1, async@1.5.0, tough-cookie@2.2.1, lodash.debounce@3.1.1, configstore@1.3.0, os-name@1.0.3)
  ├── bower-config@1.2.2 (graceful-fs@4.1.2, osenv@0.1.3, optimist@0.6.1)
  ├── github@0.2.4 (mime@1.3.4)
  ├── tar-fs@1.8.1 (pump@1.0.1, tar-stream@1.3.1)
  ├── request@2.53.0 (forever-agent@0.5.2, aws-sign2@0.5.0, caseless@0.9.0, tunnel-agent@0.4.1, oauth-sign@0.6.0, isstream@0.1.2, stringstream@0.0.5, json-stringify-safe@5.0.1, tough-cookie@2.2.1, qs@2.3.3, node-uuid@1.4.7, form-data@0.2.0, mime-types@2.0.14, combined-stream@0.0.7, http-signature@0.10.1, bl@0.9.4, hawk@2.3.1)
  ├── cardinal@0.4.4 (ansicolors@0.2.1, redeyed@0.4.4)
  ├── update-notifier@0.3.2 (is-npm@1.0.0, string-length@1.0.1, semver-diff@2.1.0, latest-version@1.0.1)
  ├── decompress-zip@0.1.0 (mkpath@0.1.0, touch@0.0.3, readable-stream@1.1.13, binary@0.3.0)
  ├── handlebars@2.0.0 (optimist@0.3.7, uglify-js@2.3.6)
  ├── inquirer@0.10.0 (strip-ansi@3.0.0, ansi-regex@2.0.0, figures@1.4.0, ansi-escapes@1.1.0, cli-width@1.1.0, rx-lite@3.1.2, through@2.3.8, readline2@1.0.1, cli-cursor@1.0.2, run-async@0.1.0, lodash@3.10.1)
  ├── mout@0.11.1
  └── configstore@0.3.2 (object-assign@2.1.1, xdg-basedir@1.0.1, uuid@2.0.1, osenv@0.1.3, js-yaml@3.4.5)
```

Arrancamos bower.json
```
  bower init
```

```javascript
  {
    "name": "pruebas_bower",
    "homepage": "https://github.com/UlisesGascon/Curso-in-company-NexTReT",
    "authors": [
      "ulisesgascon"
    ],
    "description": "",
    "main": "",
    "moduleType": [],
    "license": "MIT",
    "private": true,
    "ignore": [
      "**/.*",
      "node_modules",
      "bower_components",
      "test",
      "tests"
    ]
  }
```

Buscamos paquetes
```
  bower search <paquete>
  bower search jquery
```

Instalando Paquetes
```
  bower install <paquete>
  bower install jquery
```

Instalando versiones especificas del paquete
```
  bower install <package>#<version>
```

Instalando Paquetes y guardandolos en bower.json
```
  bower install <paquete> -save
  bower install bootstrap -save
```

```
  ulisesgascon:~/workspace/profe/pruebas_bower (master) $ bower install bootstrap -save
  bower jquery#~2.1.4             cached git://github.com/jquery/jquery.git#2.1.4
  bower jquery#~2.1.4           validate 2.1.4 against git://github.com/jquery/jquery.git#~2.1.4
  bower bootstrap#*           not-cached git://github.com/twbs/bootstrap.git#*
  bower bootstrap#*              resolve git://github.com/twbs/bootstrap.git#*
  bower bootstrap#*             download https://github.com/twbs/bootstrap/archive/v3.3.5.tar.gz
  bower bootstrap#*              extract archive.tar.gz
  bower bootstrap#*             resolved git://github.com/twbs/bootstrap.git#3.3.5
  bower jquery#~2.1.4            install jquery#2.1.4
  bower bootstrap#~3.3.5         install bootstrap#3.3.5
```

```javascript
  // bower.json
  {
    "name": "pruebas_bower",
    "homepage": "https://github.com/UlisesGascon/Curso-in-company-NexTReT",
    "authors": [
      "ulisesgascon"
    ],
    "description": "",
    "main": "",
    "moduleType": [],
    "license": "MIT",
    "private": true,
    "ignore": [
      "**/.*",
      "node_modules",
      "bower_components",
      "test",
      "tests"
    ],
    "dependencies": {
      "jquery": "~2.1.4",
      "bootstrap": "~3.3.5"
    }
  }
```

Borrando paquetes 
```
  bower uninstall <paquete>
  bower uninstall jquery
```

Borrando paquetes  y guardandolos en bower.json
```
  bower uninstall <paquete>
  bower uninstall jquery
```

Verificando los paquetes instalados y sus dependencias
```
  bower list
```

```
  ulisesgascon:~/workspace/profe/pruebas_bower (master) $ bower list
  bower check-new     Checking for new versions of the project dependencies...
  pruebas_bower /home/ubuntu/workspace/profe/pruebas_bower
  ├─┬ bootstrap#3.3.5 (latest is 4.0.0-alpha)
  │ └── jquery#2.1.4 (3.0.0-alpha1+compat available)
  └── jquery#2.1.4 (latest is 3.0.0-alpha1+compat)
```

Actualizando todo
```
  bower update
```

Actualizando un paquete específico
```
  bower update <package>
```

Usando Bower
```
  bower list -paths
```

```
  ulisesgascon:~/workspace/profe/pruebas_bower (master) $ bower list -paths
  
    bootstrap: [
      'public/vendor/bootstrap/less/bootstrap.less',
      'public/vendor/bootstrap/dist/js/bootstrap.js'
    ],
    jquery: 'public/vendor/jquery/dist/jquery.js'
```

```html
  <!DOCTYPE html>
  <html lang="es">
    <head>
      <meta charset="utf-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <!-- The above 3 meta tags *must* come first in the head; any other head content must come *after* these tags -->
      <title>Bootstrap 101 Template</title>
  
      <!-- Bootstrap -->
      <link href="public/vendor/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet">
  
    </head>
    <body>
      <h1>Hello, world!</h1>
  
      <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
      <script src="public/vendor/jquery/dist/jquery.js"></script>
      <!-- Include all compiled plugins (below), or include individual files as needed -->
      <script src="public/vendor/bootstrap/dist/js/bootstrap.js"></script>
    </body>
  </html>
```

**Bower (Entendiendo el funcionamiento)**

bower.json. ¿Qué necesitamos?
```javascript
  {
      "name": "Mi Aplicación",
      "version": "1.0.0",
      "dependencies": {
          "modernizr": "*",
          "jquery": "~2.0.2",
          "bootstrap": "*",
          "requirejs": "*"
      }
  }
```

.bowerrc ¿Donde lo necesitamos?
```javascript
  {
      "directory": "public/vendor",
      "json": "bower.json"
  }
```

Instalamos todo lo anterior
```
  bower install
```


**Bower (Trucos)**

- Se puede instalar componentes aislados primero y luego hacer *bower init* para generar el *bower.json* con todo incluido.
- Ignoramos la carpeta *bower_components* con *.gitignore*. Recuerda que haciendo *bower.init* se instala todo de nuevo.
- Instalación de paquetes más alla de los definidos en search:

- Paquetes registrados:
```
  $ bower install jquery
```

- Acesso directo -> GitHub:
```
  $ bower install desandro/masonry
```

- .git:
```
  $ bower install git://github.com/user/package.git
```

- URLs:
```
  $ bower install http://example.com/script.js
```

### Gulp 

![Gulp](http://anexsoft.com/uploads/60dbd15f5f2a87bc51375dbcaa7e4f05.jpg)
![Gulp_anatomy](http://i2.wp.com/joellongie.com/wp-content/uploads/2015/02/web-gulp-anatomy.jpg)


- **Grunt vs. Gulp**
![Grunt_WF](http://image.slidesharecdn.com/automatingyourworkflowwithgulp-140719201504-phpapp01/95/automating-your-workflow-with-gulpjs-21-638.jpg?cb=1405801149)
![Gulp_WF](http://image.slidesharecdn.com/automatingyourworkflowwithgulp-140719201504-phpapp01/95/automating-your-workflow-with-gulpjs-22-638.jpg?cb=1405801149)
- [Más información](http://www.slideshare.net/appleboy/automating-your-workflow-with-gulp)

Instalamos Gulp global
```
npm install --global gulp
```

Incluimos la dependencia en *package.json*
```
npm install --save-dev gulp
```

Creamos *gulpfile.js* y agregamos dependencias y la primera tarea por defecto
```javascript
var gulp = require('gulp');

gulp.task('default', function() {
  // place code for your default task here
});
```

[Ejemplo de gulpfile.js](https://gist.github.com/torgeir/8507130)

Ejecutamos Gulp
```
gulp
```

**Entendiendo Gulp**

- gulp.src():
  - Un solo archivo
  ```javascript
    gulp.src('client/templates/*.jade')
    // .pipe(...)
  ```
  - Multiples archivos
  ```javascript
    gulp.src(['client/*.js', '!client/b*.js', 'client/bad.js'])
    // .pipe(...)
  ```
- gulp.dest():
```javascript
gulp.src('./client/templates/*.jade')
  .pipe(jade())
  .pipe(gulp.dest('./build/templates'))
  .pipe(minify())
  .pipe(gulp.dest('./build/minified_templates'));
```



**Plugins destacados**
- [Todos los Plugins](http://gulpjs.com/plugins/)
- [uncss](https://www.npmjs.com/package/gulp-uncss/)
- [gulp-load-plugins](https://www.npmjs.com/package/gulp-load-plugins/)
- [gulp-clean](https://github.com/peter-vilja/gulp-clean)
- [gulp-concat](https://github.com/contra/gulp-concat)
- [gulp-uglify](https://github.com/terinjokes/gulp-uglify)
- [gulp-reveal](https://www.npmjs.com/package/gulp-reveal)

### Yeoman
![Yeoman Logo](https://raw.githubusercontent.com/yeoman/media/master/optimized/yeoman-masthead.png)
> The Yeoman workflow comprises three types of tools for improving your productivity and satisfaction when building a web app: the scaffolding tool (yo), the build tool (Grunt, Gulp, etc) and the package manager (like Bower and npm).

- [Yeoman Instalation Working Flow](https://www.youtube.com/watch?v=zBt2g9ekiug)
- [Yeoman - Generator-webapp](https://github.com/yeoman/generator-webapp)
- [Yeoman - Santa Barbara JavaScript Meetup](http://www.slideshare.net/tim_doherty/yeoman-santa-barbara-bjava-scriptmeetup)
- [Automating Your Front-end Workflow with Yeoman 1.0 (Addy Osmani)](https://www.youtube.com/watch?v=1OAfGm_cI6Y)


**Yeoman**
Instalamos Yeoman global (incluye Grunt, Bower...)
```
  npm install yo -g
```

Instalamos globalmente el generador de proyectos web
```
  npm install --global generator-gulp-webapp
```

En la carpeta deseada lanzamos el generador para que se cree un pryecto completo
```
  yo gulp-webapp
```

Acabada la instalación con exito 
```
  gulp serve
```

Preparando todo para producción
```
  gulp 
```

**Yeoman (gestión de errores de instalación)**

Verificamos que es lo que no funciona.
```
  yo doctor
```

[ NO RECOMENDADO ] Entramos como root
```
  sudo yo 
```

[ NO RECOMENDADO ] Forzamos la instalación de un paquete global especificando la versión.
```
  sudo npm install -force -g <paquete>@version 
```

Instalación Manual de dependencias
```
  npm install && bower install
```

- [Yeoman in c9.io](https://c9.io/blog/how-to-use-yeoman-on-cloud9/)

 

### WebSockets

![WS_Sockets](http://fernetjs.com/wp-content/uploads/2012/11/websocket-lifecycle.png)

Entendiendo los eventos

![Sockets](http://cdn.sandsmedia.com/ps/onlineartikel/pspic/picture_file/53/WebSocket4dd23ade6df2a.png)


**Negociación del protocolo WebSocket**

> Para establecer una conexión WebSocket, el cliente manda una petición de negociación WebSocket, y el servidor manda una respuesta de negociación WebSocket, como se puede ver en el siguiente ejemplo:
> [WebSockets en Wikiwand](https://www.wikiwand.com/es/WebSocket)

- Cliente:
```
  GET /demo HTTP/1.1
  Host: example.com
  Connection: Upgrade
  Sec-WebSocket-Key2: 12998 5 Y3 1 .P00
  Sec-WebSocket-Protocol: sample
  Upgrade: WebSocket
  Sec-WebSocket-Key1: 4 @1 46546xW%0l 1 5
  Origin: http://example.com
  
  ^n:ds[4U
```

- Servidor:
```
  HTTP/1.1 101 WebSocket Protocol Handshake
  Upgrade: WebSocket
  Connection: Upgrade
  Sec-WebSocket-Origin: http://example.com
  Sec-WebSocket-Location: ws://example.com/demo
  Sec-WebSocket-Protocol: sample

  8jKS'y:G*Co,Wxa-
```
> Los 8 bytes con valores numéricos que acompañan a los campos Sec-WebSocket-Key1 y Sec-WebSocket-Key2 son tokens aleatorios que el servidor utilizará para construir un token de 16 bytes al final de la negociación para confirmar que ha leído correctamente la petición de negociación del cliente.


**Sockets.io**
![Sockets](https://camo.githubusercontent.com/b74075d1deca125ad36f8fded4055f896d9f2108/687474703a2f2f666f746f732e73756265666f746f732e636f6d2f32376135653361633065393936666134663063643066613239386635356366636f2e706e67)

- Con HTTP directamente:
```javascript
  var server = require('http').createServer();
  var io = require('socket.io')(server);
  io.on('connection', function(socket){
    socket.on('event', function(data){});
    socket.on('disconnect', function(){});
  });
  server.listen(3000);
```

- Con Express:
```javascript
  var app = require('express')();
  var server = require('http').createServer(app);
  var io = require('socket.io')(server);
  io.on('connection', function(){ /* … */ });
  server.listen(3000);
```

- [Socket.io en Github](https://github.com/socketio/socket.io)
- [Socket.io - Express 3/4](http://socket.io/docs/#using-with-express-3/4)

**Ejercicios**

2 - Partiendo de este [proyecto](https://github.com/losmescaleros/twitter-sentiments) realiza mejoras de contenido y visuales
- Objetivos:
  - Fork y lanzamiento en el entorno de desarrollo 
  - Mejorar la interfaz (estáticos)
  - Cambiar los hashtags y mejorar el sistema de analisis usando librerias
- Objetivos opcionales:
  - Refactoriza y evoluciona este repositorio para crear una aplicación que analices Tweets con un contenido especifico.
  - [Ejemplo](http://it-pulse.herokuapp.com/)




**Patrónes**

- [Patrón Iterator](https://www.wikiwand.com/es/Iterador_(patr%C3%B3n_de_dise%C3%B1o))
	- Acceso secuencial a los elementos de un array o propiedades de un objeto sin exponerlos.

- Array
```javascript
// Patrón Iterador
var iterador = (function() {

  var indice = 0,
      datos = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
      totalDatos = datos.length;

  return {
      siguiente: function() {
          var elemento;
          if (!this.tieneSiguiente()) {
              return null;
          }
          elemento = datos[indice];
          indice ++;
          return elemento;
      },
      tieneSiguiente: function() {
          return indice < totalDatos;
      },
      rebobinar: function() {
          indice = 0;
          return datos[indice];
      },
      actual: function() {
          return datos[indice];
      }
  };

}());

/* Probando
while(iterador.tieneSiguiente()) {  
    console.log(iterador.siguiente());
}

iterador.rebobinar();  
console.log(iterador.actual());  
*/
```

- Objeto
```javascript
var iterador = (function() {

  var indice = 0,
      datos = { primerDato: 1, segundoDato: 'dos', tercerDato: 'tercero' },
      llaves = Object.keys(datos),
      totalDatos = llaves.length;

  return {
      siguiente: function() {
          var elemento;
          if (!this.tieneSiguiente()) {
              return null;
          }
          elemento = datos[llaves[indice]];
          indice ++;
          return elemento;
      },
      tieneSiguiente: function() {
          return indice < totalDatos;
      },
      rebobinar: function() {
          indice = 0;
          return datos[llaves[indice]];
      },
      actual: function() {
          return datos[llaves[indice]];
      }
  };

}());

/* Probando
while(iterador.tieneSiguiente()) {  
    console.log(iterador.siguiente());
}

iterador.rebobinar();  
console.log(iterador.actual());  
*/ 
```

- [Patrón decorator](https://www.wikiwand.com/es/Iterador_(patr%C3%B3n_de_dise%C3%B1o))
	- Extender objetos.
	- Sobreescribir dinamicamente los métodos.

- Añadiendo una funcionalidad
```javascript
function constructorCoches( color ){
  this.marca = "Seat";
  this.modelo = "Ibiza";
  this.antiguedad = 20;
  this.color = color || "rojo";
  this.detalles = function (){
    console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años y color "+this.color);
  }
}


var cocheRojo = new constructorCoches();
cocheRojo.detalles();


var otroCoche = new constructorCoches( "Azul" );
otroCoche.detalles();


// Decorator
otroCoche.definirModelo = function( nuevoModelo ){
this.modelo = nuevoModelo;
};

otroCoche.definirColor = function( nuevoColor ){
this.color = nuevoColor;
};

otroCoche.definirModelo( "Panda" );
otroCoche.definirColor( "Azul Oscuro" );
otroCoche.detalles();

var nuevoCoche = new constructorCoches( "Verde" );
nuevoCoche.detalles();
```

- Añadiendo multiples funcionalidades
```javascript
// Constructor
function constructorCoches( color ){
  this.marca = "Seat";
  this.modelo = "Ibiza";
  this.antiguedad = 20;
  this.color = color || "rojo";
  this.extras = 0;
  this.detalles = function (){
    console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años y color "+this.color);
  }
}

// Decorator 1
function gps( coche ) {
  coche.gps = true;
  coche.extras++;
}

// Decorator 2
function aireAcondiccionado( coche ){
  coche["aire acondiccionado"] = true;
  coche.extras++;
}

// Decorator 3
function elevaLunas( coche ){
  coche.elevaLunas = true;
  coche.extras++;
}

// Decorator 4
function farosLed( coche ){
  coche["faros led"] = true;
  coche.extras++;
}

// Decorator 5
function detallesTecnicos( coche ){
  coche.detallesTecnicos = function(){
    if(coche.extras > 0){
      console.info("El coche tiene "+coche.extras+" extras: \n");
      (coche.gps) ? console.log("- GPS"):console.log("- SIN GPS");
      (coche["aire acondiccionado"]) ? console.log("- Aire acondiccionado"):console.log("- SIN Aire acondiccionado");
      (coche["faros led"]) ? console.log("- Faros Led"):console.log("- SIN Faros Led");
      (coche.elevaLunas) ? console.log("- Elevalunas"):console.log("- SIN Elevalunas");
    } else {
      console.info("Parece.. que no se han añadido extras aun.");
    }
  };
}

var cocheRojo = new constructorCoches();
cocheRojo.detalles();


// Aplicando cambios
detallesTecnicos(cocheRojo);
cocheRojo.detallesTecnicos();

// Aplicando más cambios
gps(cocheRojo);
aireAcondiccionado(cocheRojo);
elevaLunas(cocheRojo);
farosLed(cocheRojo);
cocheRojo.detallesTecnicos();


var nuevoCoche = new constructorCoches( "Verde" );
nuevoCoche.detalles();
```


- [Patrón Façade (Fachada)](https://www.wikiwand.com/es/Iterador_(patr%C3%B3n_de_dise%C3%B1o))
	- Creación de interfaces de alto nivel.
	- Muy usado en librerías
	- Oculta el código más complejo
	- Desacoplarnos de código externo

```javascript	
var moduloRobotAutonomo = (function() {
 
    var _privado = {
        velocidad: 0,  // Km/h
        velocidadMax: 20, // Km/h
        velocidadMin: 2, // Km/h

        // ... más propiedades relativos a sensores, navegación, etc...
        
        velocidadActual: function() {
            console.log( "Velocidad Actual:" + _privado.velocidad);
        },
        ajustarVelocidad: function( valor ) {
            this.velocidad = valor;
        },
        acelerar: function() {
          if (_privado.velocidad >= _privado.velocidadMax ) {
            console.warn("Máxima velocidad Alcanzada!");
            _privado.velocidadActual();
          } else if (_privado.velocidad < _privado.velocidadMax){
              _privado.ajustarVelocidad (_privado.velocidad+1)
              _privado.velocidadActual();
          };
        },
        desacelerar: function() {
          if (_privado.velocidad <= _privado.velocidadMin ) {
            console.warn("Mínima velocidad Alcanzada!");
            _privado.velocidadActual();
          } else if (_privado.velocidad > _privado.velocidadMin){
              _privado.ajustarVelocidad (_privado.velocidad-1)
              _privado.velocidadActual();
          };
        },
        parar: function(){
          _privado.velocidad = 0;
          console.log("Robot parado");
        },
        validarVelocidad: function (valor) {
          if( valor <= _privado.velocidadMax && valor >= _privado.velocidadMin ){
            return true
          }else {
            return false
          }  
        }
		
		// más métodos relativos a sensores, navegación, etc...
    };
 
    return {
        facadeAPI: {
          velocidadCrucero: function(valor){
            if(_privado.validarVelocidad(valor)){
              _privado.ajustarVelocidad(valor);
              _privado.velocidadActual();
            }else{
              console.warn("La velocidad deseada "+valor+"Km/h no esta entre "+_privado.velocidadMin+"Km/h y los "+_privado.velocidadMax+"Km/h. permitidos" )
            }
          },
          masLento: _privado.desacelerar,
          masRapido: _privado.acelerar,
          stop:_privado.parar
        } 
    };
}());
 
/* Jugando con el robot
var robot = moduloRobotAutonomo.facadeAPI;
robot.velocidadCrucero(20); // velocidad = 20
robot.masRapido(); // Max alcanzado
robot.stop(); // Parado
robot.masLento(); // Min alcanzado
*/
```


- [Patrón Prototipo](https://www.wikiwand.com/es/Prototype_(patr%C3%B3n_de_dise%C3%B1o))

- Clonación simple
```javascript
	var coche = {
	    marca: "Seat",
	    modelo: "Panda",
	    antiguedad: 20,
	    color: "azul",
	    tipo: "turismo"
	};

	var clonCoche = Object.create(coche);

	console.log(clonCoche.marca+" "+clonCoche.modelo);	
```

- Clonación compleja
```javascript
var coche = {
  marca: "Land Rover",
  modelo: "Santana Aníbal",
  antiguedad: 35,
  color: "Marrón tierra",
  tipo: "4x4",
  detalles: dameDetalles
};

var furgon = {
  taraMinima: 1200,
  cargaUtil: 768,
  volumenCarga: 4.5,
  detalles: detallesTecnicos
};

var conductor = {
  nombre: "Yo",
  apellido: "Mismo",
  experiencia: 10000,
  limite: 120,
  detalles: function(){
    console.info("El conductor es "+ this.nombre + " " +this.apellido+". Con "+this.experiencia+" horas de experiencia y una restricción a "+this.limite+"Km/h.");
  }
}

function dameDetalles(){
  console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
};

function detallesTecnicos(){
  console.warn("Tu coche tiene una Tara mínima de "+this.taraMinima+". Carga útil de "+this.cargaUtil+" y un volumen de carga de "+this.volumenCarga+"m3");
};

// Patrón de Prototype
var miPickup = Object.create(coche, { 
    'conductor': { value: conductor },
    'carga': { value: furgon} 
  });


miPickup.detalles();
miPickup.carga.detalles();
miPickup.conductor.detalles();
console.log("Es \"coche\" prototipo de \"miPickup\" ? "+coche.isPrototypeOf(miPickup));
console.log("Es \"conductor\" prototipo de \"miPickup\" ? "+conductor.isPrototypeOf(miPickup));
console.log("Es \"furgon\" prototipo de \"miPickup\" ? "+furgon.isPrototypeOf(miPickup));
```

- [Patrón Mediador](https://es.wikipedia.org/wiki/Mediator_(patr%C3%B3n_de_dise%C3%B1o))
	- Una interfaz única - Objeto central.
	- Todos los módulos comunican con este módulo central.

```javascript
	// Patron de Mediador
	var moduloCentral = (function(){

	    // Storage for topics that can be broadcast or listened to
	    var _temas = {};

	    // Subscribe to a topic, supply a callback to be executed
	    // when that topic is broadcast to
	    var _suscribir = function( tema, fn ){
	        if ( !_temas[tema] ){
	            _temas[tema] = [];
	        }
	        _temas[tema].push( { context: this, callback: fn } );
	        return this;
	    };

	    // Publish/broadcast an event to the rest of the application
	    var _publicar = function( tema ){
	        var args;
	        if ( !_temas[tema] ){
	            return false;
	        }
	        args = Array.prototype.slice.call( arguments, 1 );
	        for ( var i = 0, l = _temas[tema].length; i < l; i++ ) {
	            var subscription = _temas[tema][i];
	            subscription.callback.apply( subscription.context, args );
	        }
	        return this;
	    };

	    return {
	        verTemas: _temas,
	        publicar: _publicar,
	        suscribir: _suscribir,
	        instalarEn: function( obj ){
	            obj.suscribir = _suscribir;
	            obj.publicar = _publicar;
	        }
	    };

	}());

	// Creamos dos Objetos
	var modulo1 = {};
	var modulo2 = {};
	console.clear();

	// Instalamos ...
	moduloCentral.instalarEn(modulo1);
	moduloCentral.instalarEn(modulo2);

	// Ajustamos las suscripciones
	modulo1.suscribir("test", function(){
	    console.info("\"modulo1\" suscrito a \"test\". Callback disparado! ")
	});

	modulo2.suscribir("test2", function(){
	    console.info("\"modulo2\" suscrito a \"test2\". Callback disparado! ")
	});

	moduloCentral.suscribir("testCentral", function(){
	    console.info("\"moduloCentral\" suscrito a \"testCentral\". Callback disparado! ")
	});

	// Suscripciones extra...
	moduloCentral.suscribir("test", function(){
	    console.info("\"moduloCentral\" suscrito a \"test\". Callback disparado! ")
	});
	moduloCentral.suscribir("test2", function(){
	    console.info("\"moduloCentral\" suscrito a \"test2\". Callback disparado! ")
	});
	console.clear();

	// Disparamos las publicaciones
	modulo2.publicar("testCentral");
	modulo2.publicar("test2");
	modulo2.publicar("test");

	modulo1.publicar("testCentral");
	modulo1.publicar("test2");
	modulo1.publicar("test");

	moduloCentral.publicar("testCentral");
	moduloCentral.publicar("test2");
	moduloCentral.publicar("test");
```


### Require.js & AMD

![Require & AMD logo](http://d348unuw4205d6.cloudfront.net/wp-content/uploads/2014/06/amd_and_require.jpg)

- *Asincronia*
![Asincronia](http://www.codeproject.com/KB/scripting/625262/AMD.png)

- *Dependencias y modularidad*
![Modularidad](http://1.bp.blogspot.com/-RWKQH6r6AQ8/Uutpgj0letI/AAAAAAAAAnk/Rd7hmZ-0-Rg/s1600/fig01.png)


**Entendiendo la utilidad de Require.js**
- Código convencional (Código espagueti):
  - [Código espagueti](https://www.wikiwand.com/es/C%C3%B3digo_espagueti)
  - index.html:
  ```html
    <!doctype html>
    
    <html lang="en">
    <head>
      <meta charset="utf-8">
    
      <title>Testing Requirejs</title>
    
    
    </head>
    
    <body>
      <script src="calculadora.js"></script>
    </body>
    </html>
  ```

  - calculadora.js
  ```javascript
  function sumar (x, y) {
      return x+y
  };
  
  function restar (x, y) {
      return x-y
  };
  
  function multiplicar (x, y) {
      return x*y
  };
  
  
  function dividir (x, y) {
      return x/y
  };
  ```

- Código convencional (Creando un objeto):

  - calculadora.js
  ```javascript
  var calculadora = {};

  calculadora.sumar = function (x,y) {
      return x + y
  };
  calculadora.restar = function (x, y) {
      return x - y
  }
  calculadora.multiplicar = function (x, y) {
      return x * y
  }
  calculadora.divir = function (x, y) {
      return x / y
  }
  ```
  
  
- Código convencional (Mejorando la escalabilidad "dividiendo el objeto"):
  - index.html:
  ```html
  <script src="sumar.js"></script>
  <script src="restar.js"></script>
  <script src="divir.js"></script>
  <script src="multiplicar.js"></script>
  ```
  
  - /sumar.js
  ```javascript
  var calculadora = calculadora || {};
  calculadora.sumar = function (x,y) {
      return x + y
  };
  ```
  
  - /restar.js
  ```javascript
  var calculadora = calculadora || {};
  calculadora.restar = function (x, y) {
      return x - y
  }
  ``` 

  - /dividir.js
  ```javascript
  var calculadora = calculadora || {};
  calculadora.divir = function (x, y) {
      return x / y
  }
  ```


  - /multiplicar.js
  ```javascript
  var calculadora = calculadora || {};
  calculadora.multiplicar = function (x, y) {
      return x * y
  }
  ```


**Usando Require.js**
- AMD:
  - [Asynchronous module definition](https://www.wikiwand.com/es/Asynchronous_module_definition)
  
  - index.html:
  ```html
  <script data-main="calculadora" src="require.js"></script>
  ```
  - /calculadora.js
  ```javascript
  require(['calculadora/sumar', 'calculadora/restar', 'calculadora/cuadrado'], function (sum, res, cua) {
	console.info(sum(1,2)); // 1 + 2
	console.info(res(3,1)); // 3 - 1 
	console.log(cua(2)); // 2 * 2
  });
  ```

  - calculadora/sumar.js
  ```javascript
  define(function () {
  	return function (x, y) {
  		return x + y;
  	};
  });
  ```

  - calculadora/restar.js
  ```javascript
  define(function () {
  	return function (x, y) {
  		return x - y;
  	};
  });
  ```

  - calculadora/multiplicar.js
  ```javascript
  define(function () {
  	return function (x, y) {
  		return x * y;
  	};
  });
  ```

  - calculadora/cuadrado.js
  ```javascript
  define(['calculadora/multiplicar'], function (multiplicar) {
  	return function (x) {
  		return multiplicar(x, x);
  	};
  });
  ```


**Require.js - Modo Avanzado**

- Require.js con dependencias externas:
  - vendor/jquery.min.js (en local)

  - script.js
  ```javascript
  require(['vendor/jquery'], function($){
      $('#hola').html("<h1>HOLA! Hola!</h1>");
  });
  ```


- Require.js varios modulos en el mismo archivo:
  - script.js
  ```javascript
  require(['hola', 'adios'], function(hola, adios){
      $('#hola').html("<h1>"+hola+" y "+adios+"!</h1>");
  });
  ```

  - hola.js
  ```javascript
  define(function() {
      return "Hola";
  });
  
  define('adios', function() {
      return "adios";
  });
  ```

- Require.js configurando baseUrl:

  - Estructura del proyecto: 
  ```  
    www/
        /assets/
        /css/
        /js/
            /App/
                main.js
        /vendor/
            bootstrap.js
            jquery.js
  ```

  - config.js:
  ```javascript    
  requirejs.config({
      baseUrl: '.assets/js'
  });
  ```
  
  - *.js
  ```javascript 
  require(['vendor/jquery', 'vendor/bootstrap', 'app/main']);
  ```


- Require.js configurando Paths:

  - Estructura del proyecto: 
  ```  
    www/
        /assets/
        /css/
        /js/
            /App/
                main.js
        /vendor/
            bootstrap.js
            jquery.js
                
  ```  

  - config.js:
  ```javascript 
  requirejs.config({
      baseUrl: '.assets/js',
      paths: {
          'jquery': 'vendor/jquery',
          'bootstrap': 'vendor/bootstrap',
          'main': 'app/main'
      }
  });
  ```
  
  - *.js:
  ```javascript 
  require(['jquery', 'bootstrap', 'main']);
  ```
