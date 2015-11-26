### Eventos (custom)
```javascript
document.body.addEventListener("eventoCustom", function(e) {
	
	console.info("Detalles del evento: ", e);
	console.info("Información adiccional: ", e.detail);
	e.detail.metodo1();
});

var miEvento = new CustomEvent("eventoCustom", {
  detail: {
    dato1: "Hola!",
    metodo1: function(){
        console.log(this.dato1);
    }
  }
});

document.body.dispatchEvent(miEvento);
```

- [Soporte](http://caniuse.com/#search=customEvent)


### Javascript Avanzado (Patrones de Código)

**3 Capas**

- CSS (Diseño)
    - en archivos.css 

- HTML (Contenido)
    - Nada de css o js en línea
    - Manejo de eventos en archivos.js

- JS (Funcionalidad)
    - en archivos.js

**Namespace**
- Reducir el número de objetos globales
- Todo forma parte de un único objeto
- Se puede trabajar en diversos archivos .js

- Namespace (función anónima):
    ```javascript
        var myApp = (function () {
            // privado
            var metodoPrivado1 = function () {
                console.info("Método Privado 1");
            };
            var metodoPrivado2 = function () {
                console.info("Método Privado 2");           
            };
            var propiedadPrivada1 = 'dato1';
            return {
                // público
                metodoPublico1: metodoPrivado1,
                propiedadesPublicas:{
                    propiedad1: propiedadPrivada1,
                    otro: "otro"
                },
                mas:{
                    MetodoPublico2: metodoPrivado2
                }
                //...
            }
        })();
    ```

- Namespace (Extensión):
    ```javascript
        var myApp = myApp || {};

        (function( namespace ){
            namespace.propiedad1 = "Propiedad 1";
            namespace.metodo1 = function(){
                return "metodo1";
            };
        })(myApp);
        console.log(myApp); 
    ```

- Usando Namespace:
    ```javascript
        // global
        var myApp = myApp || {};
        
        // sub-objeto
        myApp.ejemploDatos = {}
        
        myApp.ejemploDatos = {
            metodo: function () {
                console.log("esto es un metodo");           
            },
            propiedad1: 1,
            propiedad2: "dos"
        }
    ```

- Simplificar la creación de elementos:
    ```javascript
        var myApp = myApp || {};
        
        myApp.crearElemento = function(nombre){
            var partes = nombre.split('.');
            var nameSpace = myApp;
            for (var i in partes) {
                if (!nameSpace[partes[i]]) {
                    nameSpace[partes[i]] = {};
                }
                nameSpace = nameSpace[partes[i]];
            }
        }
        
        myApp.crearElemento('uno.dos.tres.cuatro.cinco.y.mas.niveles');
        myApp.uno.dos.tres.cuatro.cinco.y.mas.niveles = "Funciona!"
    ```


**Init-time branching**
- Cuando algo no cambia durante la ejecucción
- Se carga una vez al principio y devuelve funciones segun la condicción

```javascript

    var myApp = {};
    
    myApp.eventos = {
        agregar: null,
        quitar: null,
        manejador: function(evento){
        
            console.log("-----------------------------")
            console.log("Type: "+evento.type); // Tipo
            console.log("Bubbles: "+evento.bubbles); // sube por el DOM
            console.log("Cancelable: "+evento.cancelable);
            console.log("CurrentTarget: ", evento.currentTarget);
            console.log("DefaultPrevented: "+evento.defaultPrevented);
            console.log("EventPhase: "+evento.eventPhase);
            console.log("Target: ", evento.target);
            console.log("TimeStamp: "+evento.timeStamp);
            console.log("IsTrusted: "+evento.isTrusted); // true - Usuario o false - Script
            console.log("=============================")
        
        }
    };
    
    if (typeof window.addEventListener === 'function') {
        myApp.eventos.agregar = function(el, type, fn) {
            el.addEventListener(type, fn, false);
        };
        myApp.eventos.quitar = function(el, type, fn) {
            el.removeEventListener(type, fn, false);
        };
    } else { // IE8
        myApp.eventos.agregar = function(el, type, fn) {
            el.attachEvent('on' + type, fn);
        };
        myApp.eventos.quitar = function(el, type, fn) {
            el.detachEvent('on' + type, fn);
        };
    }
    
    /*
        myApp.eventos.agregar(window, 'click', myApp.eventos.manejador);
        myApp.eventos.quitar(window, 'click', myApp.eventos.manejador);
    */
    
```

**Lazy Definition**
- Se crean las funciones cuando se ejecuta por primera vez 
```javascript
    
    var myApp = {};
    
    myApp.eventos = {
        agregar: function(el, type, fn) {
            if (typeof window.addEventListener === 'function') {
                myApp.eventos.agregar = function(el, type, fn) {
                    el.addEventListener(type, fn, false);
                };
            } else { // IE8
                myApp.eventos.agregar = function(el, type, fn) {
                    el.attachEvent('on' + type, fn);
                };
            }
            
            myApp.eventos.agregar(el, type, fn);
        },
        quitar: function(el, type, fn) {
            if (typeof window.addEventListener === 'function') {
                myApp.eventos.quitar = function(el, type, fn) {
                    el.removeEventListener(type, fn, false);
                };
            } else { // IE8
                myApp.eventos.quitar = function(el, type, fn) {
                    el.detachEvent('on' + type, fn);
                };
            }
            myApp.eventos.quitar(el, type, fn);
        },
        manejador: function(evento){
        
            console.log("-----------------------------")
            console.log("Type: "+evento.type); // Tipo
            console.log("Bubbles: "+evento.bubbles); // sube por el DOM
            console.log("Cancelable: "+evento.cancelable);
            console.log("CurrentTarget: ", evento.currentTarget);
            console.log("DefaultPrevented: "+evento.defaultPrevented);
            console.log("EventPhase: "+evento.eventPhase);
            console.log("Target: ", evento.target);
            console.log("TimeStamp: "+evento.timeStamp);
            console.log("IsTrusted: "+evento.isTrusted); // true - Usuario o false - Script
            console.log("=============================")
        
        }
    };
    
    /*
        myApp.eventos.agregar(window, 'click', myApp.eventos.manejador);
        myApp.eventos.quitar(window, 'click', myApp.eventos.manejador);
    */

```

**Objeto de Configuración**
- Gestionar multiples parametros en funciones
    - No importa el orden (legibilidad y escalabilidad)

```javascript

    var myApp = {};
    
    myApp.eventos = {
        agregar: null,
        quitar: null,
        manejador: function(evento){
        
            console.log("-----------------------------")
            console.log("Type: "+evento.type); // Tipo
            console.log("Bubbles: "+evento.bubbles); // sube por el DOM
            console.log("Cancelable: "+evento.cancelable);
            console.log("CurrentTarget: ", evento.currentTarget);
            console.log("DefaultPrevented: "+evento.defaultPrevented);
            console.log("EventPhase: "+evento.eventPhase);
            console.log("Target: ", evento.target);
            console.log("TimeStamp: "+evento.timeStamp);
            console.log("IsTrusted: "+evento.isTrusted); // true - Usuario o false - Script
            console.log("=============================")
        
        }
    };
    
    if (typeof window.addEventListener === 'function') {
        myApp.eventos.agregar = function(config) {
            config.el.addEventListener(config.type, config.fn, false);
            if(config.consoleMessage){
                console.warn(config.message || "mensaje por defecto")
            }
        };
        myApp.eventos.quitar = function(config) {
            config.el.removeEventListener(config.type, config.fn, false);
            if(config.consoleMessage){
                console.warn(config.message || "mensaje por defecto")
            }
        };
        
    } else { // IE8
        myApp.eventos.agregar = function(config) {
            config.el.attachEvent('on' + config.type, config.fn);
            if(config.consoleMessage){
                console.warn(config.message || "mensaje por defecto")
            }
        };
        myApp.eventos.quitar = function(config) {
            config.el.detachEvent('on' + config.type, config.fn);
            if(config.consoleMessage){
                console.warn(config.message || "mensaje por defecto")
            }
        };
    }

    /*
    var config1 = {
        el: window,
        type: 'click',
        fn:  myApp.eventos.manejador,
        consoleMessage: true,
        message: "listener añadido a "+this.el
    }
    var config2 = {
        el: window,
        type: 'click',
        fn:  myApp.eventos.manejador,
        consoleMessage: true,
        message: "listener quitado de "+this.el
    }
    
    var config3 = {
        el: window,
        type: 'click',
        fn:  myApp.eventos.manejador,
        consoleMessage: true
    }

    myApp.eventos.agregar(config1);
    myApp.eventos.quitar(config2);
    
    myApp.eventos.agregar(config3);
    myApp.eventos.quitar(config3);
    */
```

**Propiedades y Métodos Privados**
- ECMA5:
    - Normalmente los nombres de variables y funciones suelen preceder de guion bajo (_varInterna) 
```javascript
    var constructorCocheEmpresa = function (marca, modelo, antiguedad, color) {
        this.marca = marca;
        this.modelo = modelo;
        this.antiguedad = antiguedad;
        this.color = color;

        var _ITVPasada = true;
        var _ITVfrecuencia = "Cada año";
        var _seguroEnRegla = true;
        var _companySeguros = "SegurExpress";
        var _tipoSeguro = "a terceros";


        function _dameDetalles(){
          console.log("Tu coche es un "+marca+" "+modelo+" con "+antiguedad+" años y color "+color);
        }

        function _datosPrivados() {
            if (_ITVPasada && _seguroEnRegla)
                console.info("INFO: Todo en Regla, tienes que pasar la ITV "+_ITVfrecuencia+". Tienes un seguro "+_tipoSeguro+" con "+_companySeguros);
            else{
                console.error("ALERTA! El coche no puede usarse. El seguro o la ITV no esta en regla.");
            }
        }

        _datosPrivados();
        _dameDetalles();
    };

    // var miCoche = new constructorCocheEmpresa ("Audi", "S8", 2, "negro", "Berlina");
```

**Private Members (Métodos Privilegiados)**
- Metodos que permiten acceder a datos privados de una manera controlada.

```javascript
    var constructorCocheEmpresa = function (marca, modelo, antiguedad, color) {
        this.marca = marca;
        this.modelo = modelo;
        this.antiguedad = antiguedad;
        this.color = color;
        var _ITVPasada = true;
        var _ITVfrecuencia = "Cada año";
        var _seguroEnRegla = true;
        var _companySeguros = "SegurExpress";
        var _tipoSeguro = "a terceros";

        this.dameDetalles = function(){
          console.log("Tu coche es un "+marca+" "+modelo+" con "+antiguedad+" años y color "+color);
        }

        this.datosPrivados = function() {
            if (_ITVPasada && _seguroEnRegla)
                console.info("INFO: Todo en Regla, tienes que pasar la ITV "+_ITVfrecuencia+". Tienes un seguro "+_tipoSeguro+" con "+_companySeguros);
            else{
                console.error("ALERTA! El coche no puede usarse. El seguro o la ITV no esta en regla.");
            }
        }
    };

    /* 
    var miCoche = new constructorCocheEmpresa ("Audi", "S8", 2, "negro", "Berlina");
    miCoche.datosPrivados()
    miCoche.dameDetalles()
    */
```


**Revealing Module Pattern**
- Incluir métodos privados en el retorno
```javascript
    var constructorCocheEmpresa = function (marca, modelo, antiguedad, color) {
        this.marca = marca;
        this.modelo = modelo;
        this.antiguedad = antiguedad;
        this.color = color;

        var _ITVPasada = true;
        var _ITVfrecuencia = "Cada año";
        var _seguroEnRegla = true;
        var _companySeguros = "SegurExpress";
        var _tipoSeguro = "a terceros";



        function _dameDetalles(){
          console.log("Tu coche es un "+marca+" "+modelo+" con "+antiguedad+" años y color "+color);
        }

        function _datosPrivados() {
            if (_ITVPasada && _seguroEnRegla)
                console.info("INFO: Todo en Regla, tienes que pasar la ITV "+_ITVfrecuencia+". Tienes un seguro "+_tipoSeguro+" con "+_companySeguros);
            else{
                console.error("ALERTA! El coche no puede usarse. El seguro o la ITV no esta en regla.");
            }
        }
        
        return {
         datosPrivados:   _datosPrivados,
         dameDetalles:   _dameDetalles
        }
    };

    /* 
    var miCoche = new constructorCocheEmpresa ("Audi", "S8", 2, "negro", "Berlina");
    miCoche.datosPrivados();
    miCoche.dameDetalles();
    */

```

**Self-Executing Anonymous Functions**

- Sintaxis:

```javascript
    (function(){
      console.log('Hola Mundo!');
    })();
```

- Incluyendo referencias y manipulando otros elementos
```javascript

    var myApp = myApp || {};
    
    (function(w, doc, ns){
      
      ns.accesoWindow = function(){
        return w === window;
      };
      ns.accesoDocument = function(){
        return doc === document;
      };
      ns.confirmacion = function(){
        console.log('Hola Mundo! Mis caracteristicas son: \n Acceso a Window: '+this.accesoWindow()+'\n Acceso a Document: '+this.accesoDocument());
      }
    })(window, document, myApp);

    
    // myApp.confirmacion()

```

**Memoization**
- Nos permite "cachear" resultados para agilizar los procesos más complejos
- Intentaremos resolver la [Sucesión de Fibonacci](https://www.wikiwand.com/es/Sucesi%C3%B3n_de_Fibonacci)
    - Fibonacci sin Cachear:
    ```javascript
        var fibonacci = function(numero) {
          return numero == 0 ? 0 :
                 numero == 1 ? 1 :
                 fibonacci(numero-1) + fibonacci(numero-2);
        };
        console.log( "fibonacci(34) = " + fibonacci(34));
    ```
    - Fibonacci cacheado (No Optimizado):
    ```javascript
        var fibonacci = function(numero) {
          return numero == 0 ? 0 :
                 numero == 1 ? 1 :
                 fibonacci(numero-1) + fibonacci(numero-2);
        };
        
        var fibonacci_cache = function(numero, cache) {
          if(!cache[numero]) {
            cache[numero] = fibonacci(numero);
          }
          return cache[numero];
        };
        
        var cache = {};
        console.warn("fibonacci_cache(34, cache) = " + fibonacci_cache(34, cache));
        console.info("fibonacci_cache(34, cache) = " + fibonacci_cache(34, cache));
    ```
    - Fibonacci cacheado (Optimizado):
    ```javascript
        var fibonacci = function(numero) {
          return numero == 0 ? 0 : 
                 numero == 1 ? 1 :
                 fibonacci(numero-1) + fibonacci(numero-2);
        };
        
        var cachify = function(f, cache) {
          return function(numero) {
            if(!cache[numero]) {
              cache[numero] = f(numero);
            }
            return cache[numero];
          };
        };
        
        var cache = {};
        fibonacci = cachify(fibonacci, cache);
        
        console.info("fibonacci(1476) = " + fibonacci(1476), cache );
        console.info("fibonacci(1476) = " + fibonacci(1476), cache );
    ```
    
    - [Rendimiento comparado: sin memoization](http://jsperf.com/fibonacci-cache)
    - [Rendimiento comparado: memoization simple vs. compleja](http://jsperf.com/fibonacci-cacheado)

**Ejercicio**

1 - Aplicaremos este mismo concepto a la función de [calculo factorial](http://www.wikiwand.com/es/Factorial) que vimos en clases anteriores.

```javascript
    // Tu solución
```


**Patrón Módulo**
- Usamos funciones anonimas autoejecutadas
- Encapsulamos la lógica
- Exponemos solo parte 

```javascript
    var mates = mates || {};
    
    mates.operaciones = (function() {
      var total = 0;
    
      return {
        sumar: function(a, b){
          var suma = a + b;
          total += suma;
          return suma;
        },
        restar: function(a, b){
          var resta = a - b;
          total -= resta;
          return resta;
        },
        total: function(){
          return total;
        }
      };
    })();
    
    mates.operaciones.total();  
    mates.operaciones.sumar(12, 21);
    mates.operaciones.total();
    mates.operaciones.restar(40, 1);
    mates.operaciones.total();
```


### Javascript Avanzado (Patrones de Diseño)

**Patrón Singleton**
- limitamos la instanciación de una clase a un objeto único

```javascript
    var miSingleton = (function () {
        var instancia;
     
        function crearInstancia() {
            var objeto = new Object();
            return objeto;
        }
     
        return {
            instanciacion: function () {
                if (!instancia) {
                    instancia = crearInstancia();
                }
                return instancia;
            }
        };
    })();
     
    /*
        var instancia1 = {};
        var instancia2 = {};
        console.info("¿Es lo mismo? " + (instancia1 === instancia2));  
        instancia1 = miSingleton.instanciacion();
        instancia2 = miSingleton.instanciacion();
        console.info("¿Es la misma instaciación? " + (instancia1 === instancia2));  
    */
```

**Patrón Factory**
- No usaremos *new*
- Un objeto Factory nos devuelve el nuevo objeto

```javascript
    var opcionesCoche = {
        marca: "Land Rover", 
        modelo: "Santana Aníbal", 
        antiguedad: 35, 
        color: "Marrón tierra", 
        tipo: "4x4"
    };
    
    var opcionesFurgon = {
        taraMinima: 1200,  
        cargaUtil:  768, 
        volumenCarga: 4.5,
        tipo: "furgon"
    };
    
    var coche = function (opciones) {
        this.marca = opciones.marca;
        this.modelo = opciones.modelo;
        this.antiguedad = opciones.antiguedad;
        this.color = opciones.color;
        this.tipo = opciones.tipo;

        this.detalles = function (){
            console.log("Tu vehículo es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
        };
    };
    
    var furgon = function (opciones) {
        this.taraMinima = opciones.taraMinima;
        this.cargaUtil = opciones.cargaUtil;
        this.volumenCarga = opciones.volumenCarga;

        this.detallesTecnicos = function(){
            console.warn("Tu vehículo tiene una Tara mínima de "+this.taraMinima+". Carga útil de "+this.cargaUtil+" y un volumen de carga de "+this.volumenCarga+"m3");
        };
    };
    
    // Patrón Factoría
    function factoriaVehiculos(){}
    
    factoriaVehiculos.prototype.claseVehiculo = coche;
    
    factoriaVehiculos.prototype.createVehicle = function(options) {
        if (options.tipo === "turismo"  || options.tipo === "4x4"  ) {
            this.claseVehiculo = coche;
        } else {
            this.claseVehiculo = furgon;
        }
        return new this.claseVehiculo(options);
    };
    
    // Aplicando el Patrón
    var factoriaCoches = new factoriaVehiculos();
    
    var miFurgon = factoriaCoches.createVehicle(opcionesFurgon);
    var mi4x4 = factoriaCoches.createVehicle(opcionesCoche);
    var miCoche = factoriaCoches.createVehicle({
        marca: "Seat", 
        modelo: "Ibiza", 
        antiguedad: 20, 
        color: "Azul Oscuro", 
        tipo: "turismo"
    });
    
    // Comprobaciones
    function chequearInstanciacion(){
        console.info("¿Es \"miCoche\" una instancia de \"coche\" ? " + (miCoche instanceof coche));
        miCoche.detalles();
        console.info("¿Es \"mi4x4\" una instancia de \"coche\" ? " + (mi4x4 instanceof coche));
        mi4x4.detalles();
        console.info("¿Es \"miFurgon\" una instancia de \"furgon\" ? " + (miFurgon instanceof furgon));
        miFurgon.detallesTecnicos();
    }
    
    chequearInstanciacion();
```

**Ejercicio**

2 - Aplicaremos algunos de los conceptos aprendidos para mejorar el cajero automático que creamos anteriormente.
- Requisitos:
    - Desarrolla el HTML y utiliza eventos para gestionar la interacción.
    - Usa una función anónima para encapsular el código
    - Utiliza métodos y propiedades privadas

- [Solución](https://github.com/UlisesGascon/Curso-in-comany-BQ/tree/master/otros/cajero)


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
{
  "name": "npm-scripts-tasks",
  "version": "1.0.0",
  "description": "",
  "main": "app.js",
  "scripts": {
    "emoji": "emoji-random",
    "versions": "node -v && npm -v",
    "bootstrap": "git clone https://github.com/twbs/bootstrap.git",
    "curso": "git clone https://github.com/UlisesGascon/Curso-in-comany-BQ",
    "status": "git status"
  },
  "devDependencies": {
    "emoji-random": "^0.1.2"
  },
  "author": "Ulises Gascon",
  "license": "ISC"
}
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
  setTimeout(function() {
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
      var http = require('http'),
          process = require('process'),
            url = require('url');
    
      http.createServer(function (req, res) {
        var pathname = url.parse(req.url).pathname;
        var hola = '<h1>Bienvenido!!</h1>';
        
        if (pathname === '/') {
          res.writeHead(200, {
            'Content-Type': 'text/html'
          });
          res.end(hola);
          
        } else if (pathname === '/quienes') {
          res.writeHead(200, {
            'Content-Type': 'text/html; charset=utf-8'
          });
          res.end(hola +'Somos una empresa que usa <b>la ñ y otros caracteres especiales! </b>....');
      
        } else if (pathname === '/donde') {
          res.writeHead(200, {
            'Content-Type': 'text/plain; charset=utf-8'
          });
          res.end('Estamos cerca de tí....');
        
        } else if (pathname === '/que') {
          res.writeHead(200, {
            'Content-Type': 'text/plain; charset=utf-8'
          });
          res.end('Hacemos cosas....');
        
        } else if (pathname === '/bug') {
          
          // Termina el proceso de Node
          process.exit(1); 
    
      
        } else if (pathname === '/contacto') {
          res.writeHead(200, {
            'Content-Type': 'text/plain; charset=utf-8'
          });
          res.end('Contactanos!....');
    
          
        } else {
            res.writeHead(404, {
            'Content-Type': 'text/plain'
          });
          res.end('L-E-G-E-N-D-A-R-I-O... 404!');
        }
        
      }).listen(process.env.PORT, process.env.IP);
      
      console.log('Servidor funcionando en http://'+process.env.IP+':'+process.env.PORT+'/');
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

### Jade

![Jade_logo](https://camo.githubusercontent.com/ed7e053f9f077321cd37b03f3c84d5f0197c4e6a/687474703a2f2f676172746864622e636f6d2f696d672f6a6164655f6272616e64696e672f6a6164652d30312e737667)

- Entendiendo la mécanica:
  - index.jade:
  ```
  doctype html
  html(lang="en")
    head
      title= pageTitle
      script(type='text/javascript').
        if (foo) {
           bar(1 + 5)
        }
    body
      h1 Jade - node template engine
      #container.col
        if youAreUsingJade
          p You are amazing
        else
          p Get on it!
        p.
          Jade is a terse and simple
          templating language with a
          strong focus on performance
          and powerful features.
  ```
  
  - index.html:
  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <title>Jade</title>
      <script type="text/javascript">
        if (foo) {
           bar(1 + 5)
        }
      </script>
    </head>
    <body>
      <h1>Jade - node template engine</h1>
      <div id="container" class="col">
        <p>You are amazing</p>
        <p>
          Jade is a terse and simple
          templating language with a
          strong focus on performance
          and powerful features.
        </p>
      </div>
    </body>
  </html>
  ```
  
- Bootstrap:
  - index.jade:
  ```
  doctype html
  html
    head
      title title
      include ./includes/styles.jade
    body
      .row
        .container
          .jumbotron
            h1 Hola, desde Bootstrap!
            p ¿Qué te parece?
            p
              a.btn.btn-primary.btn-lg(href='http://getbootstrap.com/', role='button') Aprende más!
      include ./includes/scripts.jade
  
  //- includes/styles.jade
  // Bootstrap
  link(rel='stylesheet', href='//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css')
  
  //- includes/scripts.jade
  // Jquery
  script(src='//ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js')
  // Bootstrap
  script(src='//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js')
  
  ```
  - index.html
  ```
  <!DOCTYPE html>
  <html>
      <head>
          <title>title</title>
          <!-- Bootstrap-->
          <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
          </head>
          <body>
              <div class="row">
                  <div class="container">
                      <div class="jumbotron">
                          <h1>Hello, desde Bootstrap!</h1>
                          <p>¿Qué te parece?</p>
                          <p>
                              <a href="http://getbootstrap.com/" role="button" class="btn btn-primary btn-lg">Aprende más!</a>
                          </p>
                      </div>
                  </div>
              </div>
              <!-- Jquery-->
              <script src="//ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
              <!-- Bootstrap-->
              <script src="//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js"></script>
          </body>
      </html>
  ```

- [Comparativa de Motores de plantillas](https://strongloop.com/strongblog/compare-javascript-templates-jade-mustache-dust/)
- [Jade en Github](https://github.com/jadejs/jade)
- [Jade en CLI](http://jade-lang.com/command-line/)
- [Jade API](http://jade-lang.com/api/)
- [Jade Language Ref](http://jade-lang.com/reference/)


### Express

![Express_logo](https://i.cloudup.com/zfY6lL7eFa-3000x3000.png)

- Middelware
![Mw_schema](http://image.slidesharecdn.com/introtonode-140914093424-phpapp01/95/intro-to-nodejs-14-638.jpg?cb=1410687757)

**Utilidades**

- Recuperar cabeceras:
  ```
  curl -I 127.0.0.1:3000
  ```

- [PostMan](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)
  
- [Html2Jade](http://html2jade.org/)
  
**Influencias / usos**

- Otros frameworks similares:
  - Zend (PHP)
  - Django (Python)
  - Sinatra (Ruby)

- Uso:
  - API JSON
  - Single Pages
  - App tiempo real


**Instalación**

- Instalación Global:
  ```
  npm install -g express
  ```

- Instalación versiones anteriores:
  ```
  npm install -g express@3.x
  ```

- Generar una estructura:
  ```
  express <nombre_proyecto>
  ```

- Instalamos las dependencias
  ```
  cd <nombre_proyecto> && npm install
  ```

- Estructura de un Proyecto (MVC):
  - app.js -> Iniciar la aplicación
  - /node_modules -> dependencias
  - package.json -> información de la aplicación
  - /public -> imagenes, js y css (Sin lógica de la aplicación)
  - /routes -> lógica
  - /views -> vista (jade)



**Manejando Express**

- GET Básico
  ```
  app.get('/hola', function(req, res){
      res.send('hemos abierto una nueva ruta!');
  });
  ```

- POST Básico
  - app.js 
  ```
  app.post('/', function(req, res){
    res.send(req.body);
  });
  ```

  - index.jade 
  ```
  section.container
  h1 Manda tu mensaje!

  form(method='post', action='/')
    fieldset
      legend Mandame tu mensaje:
      p.contenido
        label Tu mensaje
        input(name='mensaje')
      p.acciones
        input(type='submit', value='Enviar')
  ```

  - respuesta 
  ```javascript
  {
    "mensaje": "Hola Cracks!"
  }
  ```


- Parámetros en las rutas
  - app.js 
  ```javascript
  app.get('/hola/:usuario', function(req, res){
      res.send('Hola '+req.params.usuario+'. Hemos abierto una nueva ruta personalizada!');
  });
  ```

- Simulando una respuesta de una base de datos en las rutas:

  - app.js 
  ```javascript
  app.get('/consulta/:usuario', function(req, res){
      var datos = {
          marca: "Seat",
          modelo: "Ibiza",
          edad: 20,
          ITVPasada: true,
          seguroPasado: true
      };
      
      res.render('consulta.jade', {usuario: req.params.usuario, datos: datos});
  });
  ```

  - consulta.jade 
  ```
.datos
  h3 Datos: 
  p= "El Coche de "+usuario+" es un "+datos.marca+" "+datos.modelo
    
  h3 Detalles técnicos:
  ul
      li= "ITV en regla: " +datos.ITVPasada 
      li= "seguro en regla: " +datos.seguroPasado
  ```

- Dibujando las vistas (Necesario para JSON, HTML y XML):

```javascript
  exports.index = function(req, res){
    res.render('index', { variable: 'dato' }); // views/index.jade
  };
  
  // Evitando la renderización
  exports.index = function(req, res){
    res.render('index', { layout: false}); // Sin renderizar!
  };
```
**Ejercicio**

1 - **RETO** Tenemos una [Api Rest funcionando para gestionar nuestras peliculas usando Firebase y OMBD](https://github.com/UlisesGascon/Simple-API-REST-with-Firebase-and-IMBD).
Objetivos:
  - Instalar y probar el funcionamiento en tu entorno
  - Buscar el error en el cliente y [documentarlo en Github](https://github.com/UlisesGascon/Simple-API-REST-with-Firebase-and-IMBD/issues)
  - Buscar una solución al error
  - Compartir la solución utilizando [pull-request](https://github.com/UlisesGascon/Simple-API-REST-with-Firebase-and-IMBD/pulls)
