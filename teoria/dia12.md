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

```javascript
    // Tu solución
```