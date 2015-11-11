**Ejercicios**

> Vamos a crear un sistema acuapónico en nuestra oficina. Nuestro objetivo será desarrollar una aplicación para gestionarlo todo. Con este ejercicio nos centraremos en la POO y los prototipos

![Ilustración del sistema](http://www.cualtimexico.info/uploads/5/7/4/7/5747467/8636915.jpg)


1 - (Usando Constructores). Vamos a instalar un sistema acuapónico en la oficina, así que nuestra primera misión será definir nuestro equipamiento.
Contamos con un sistema compuesto de un tanque principal y una cama (recipiente para vegetales) donde plantaremos nuestros vegetales.

- Caracteristicas Tanque:
 - capacidad: 40 Litros
 - dimensiones: 51 cm x 25.5 de ancho x 30.5 de alto
 - color: Gris Claro
 - Nivel agua Máximo: 29 cm

- Caracteristicas Cama:
 - capacidad: 10 Litros
 - dimensiones: 51 cm x 25.5 de ancho x 10 de alto
 - color: Rojo
 - Nivel agua Máximo: 5 cm
 - Sustrato: Piedra volcánica

```javascript
    var acuApp = acuApp || {};

    // Constructores
    var constructorTanque = function (capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo) {
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho *largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.dimensionesMedida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
    };

    var constructorCama = function (capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo, sustrato) {
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho *largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.medida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
        this.sustrato = sustrato;
    };


    acuApp["tanque principal"] = new constructorTanque(40, "Litros", 30.5, 25.5, 51, "Cm", "Gris Claro", 2);
    acuApp["cama principal"] = new constructorCama(10, "Litros", 10, 25.5, 51, "Cm", "Rojo", 5, "Piedra volcánica");
```


2 - Añadamos el agua, para lo que necesitaremos un sistema para añadir y quitar agua, además de un desagüe automático que nos avise cuando el nivel del agua sea más alto de los esperado y evacue el sobrante.

```javascript
        var debugMode = true;

    function chivato (tipo, mensaje) {
        if (debugMode) {
            if(tipo == "warn"){
                console.warn(mensaje);
            } else {
                console.log(mensaje);
            }
        }
    }

    var acuApp = acuApp || {};

    // Constructores
    var constructorTanque = function (nombre, capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo) {
        this.nombre = nombre;
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho * largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.dimensionesMedida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
        this.desagueFuncionando = false;
        this.nivelAgua = 0;
        /* Funciones */

        this.agregarAgua = function(litros){
            this.nivelAgua = this.nivelAgua + litros;
            if(this.nivelAgua >= this.nivelAguaMaximo){
                if(!this.desagueFuncionando){
                    this.desagueFuncionando = true;
                    chivato("warn", "Se activó el sistema de desagüe de emergencia en "+this.nombre);
                }
                chivato("log", "nivel actual: "+this.nivelAgua);
                this.quitarAgua(this.nivelAgua-this.nivelAguaMaximo);
            }
        };
        this.quitarAgua = function(litros){
            this.nivelAgua = this.nivelAgua-litros;
            if(this.desagueFuncionando){
                this.desagueFuncionando = false;
                chivato("log", "Se desactivo el sistema de desagüe de emergencia en "+this.nombre);
            }
            chivato("log", "nivel actual: "+this.nivelAgua);
        };
    };

    var constructorCama = function (nombre, capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo, sustrato) {
        this.nombre = nombre;
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho *largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.medida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
        this.sustrato = sustrato;
        this.desagueFuncionando = false;
        this.nivelAgua = 0;
        /* Funciones */

        this.agregarAgua = function(litros){
            this.nivelAgua = this.nivelAgua + litros;
            if(this.nivelAgua >= this.nivelAguaMaximo){
                if(!this.desagueFuncionando){
                    this.desagueFuncionando = true;
                    chivato("warn", "Se activó el sistema de desagüe de emergencia en "+this.nombre);
                }
                chivato("log", "nivel actual: "+this.nivelAgua);
                this.quitarAgua(this.nivelAgua-this.nivelAguaMaximo);
            }
        };
        this.quitarAgua = function(litros){
            this.nivelAgua = this.nivelAgua-litros;
            if(this.desagueFuncionando){
                this.desagueFuncionando = false;
                chivato("log", "Se desactivo el sistema de desagüe de emergencia en "+this.nombre);
            }
            chivato("log", "nivel actual: "+this.nivelAgua);
        };
    };


    acuApp.tanque1 = new constructorTanque("Tanque principal",40, "Litros", 30.5, 25.5, 51, "Cm", "Gris Claro", 2);
    acuApp.cama1 = new constructorCama("Cama principal", 10, "Litros", 10, 25.5, 51, "Cm", "Rojo", 5, "Piedra volcánica");
    acuApp.cama1.agregarAgua(100);
    acuApp.tanque1.agregarAgua(987);
```


3 - Añadamos ahora nuestras plantas y nuestros peces
- (opcional) teniendo en cuenta sus necesidades de espacio.
- Incluir una función para quitar peces y vegetales.

```javascript
        var debugMode = true;

    function chivato (tipo, mensaje) {
        if (debugMode) {
            if(tipo == "warn"){
                console.warn(mensaje);
            } else {
                console.log(mensaje)
            }
        }
    };

    var acuApp = acuApp || {};

    // Constructores
    var constructorTanque = function (nombre, capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo) {
        this.nombre = nombre;
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho * largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.dimensionesMedida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
        this.desagueFuncionando = false;
        this.nivelAgua = 0;
        this.peces = {};
        /* Funciones */
        this.agregarPez = function (nombre, clase, peso, espacio, lugar) {
            this.peces[nombre] = {
                tipo:"pez",
                clase: clase,
                peso: peso || 100,
                pesoMedida: "gramos",
                espacio: espacio || 0.05,
                espacioMedida: "m3",
                lugar: lugar || "Tanque principal"
            };
        };

        this.quitarPez = function (nombre) {
            var temp = this.peces[nombre];
            delete this.peces[nombre];
            return temp;
        };

        this.agregarAgua = function(litros){
            this.nivelAgua = this.nivelAgua + litros;
            if(this.nivelAgua >= this.nivelAguaMaximo){
                if(!this.desagueFuncionando){
                    this.desagueFuncionando = true;
                    chivato("warn", "Se activó el sistema de desagüe de emergencia en "+this.nombre);
                }
                chivato("log", "nivel actual: "+this.nivelAgua);
                this.quitarAgua(this.nivelAgua-this.nivelAguaMaximo);
            }
        };

        this.quitarAgua = function(litros){
            this.nivelAgua = this.nivelAgua-litros;
            if(this.desagueFuncionando){
                this.desagueFuncionando = false;
                chivato("log", "Se desactivo el sistema de desagüe de emergencia en "+this.nombre);
            }
            chivato("log", "nivel actual: "+this.nivelAgua);
        };
    };

    var constructorCama = function (nombre, capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo, sustrato) {
        this.nombre = nombre;
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho *largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.medida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
        this.sustrato = sustrato;
        this.desagueFuncionando = false;
        this.nivelAgua = 0;
        this.plantas = {};
        /* Funciones */

        this.agregarPlanta = function (nombre, clase, frutosDisponibles, estadoActual, espacio, lugar) {
        this.plantas[nombre] = {
            nombre: nombre,
            tipo: "planta",
            clase: clase,
            frutosDisponibles: frutosDisponibles,
            estadoActual: estadoActual,
            espacio: espacio || 0.05,
            espacioMedida: "m3",
            lugar: lugar || "Cama principal"
            };
        };

        this.quitarPlanta = function (nombre) {
            var temp = this.plantas[nombre];
            delete this.plantas[nombre];
            return temp;
        };

        this.agregarAgua = function(litros){
            this.nivelAgua = this.nivelAgua + litros;
            if(this.nivelAgua >= this.nivelAguaMaximo){
                if(!this.desagueFuncionando){
                    this.desagueFuncionando = true;
                    chivato("warn", "Se activó el sistema de desagüe de emergencia en "+this.nombre);
                }
                chivato("log", "nivel actual: "+this.nivelAgua);
                this.quitarAgua(this.nivelAgua-this.nivelAguaMaximo);
            }
        };
        this.quitarAgua = function(litros){
            this.nivelAgua = this.nivelAgua-litros;
            if(this.desagueFuncionando){
                this.desagueFuncionando = false;
                chivato("log", "Se desactivo el sistema de desagüe de emergencia en "+this.nombre);
            }
            chivato("log", "nivel actual: "+this.nivelAgua);
        };
    };


    acuApp.tanque1 = new constructorTanque("Tanque principal",40, "Litros", 30.5, 25.5, 51, "Cm", "Gris Claro", 2);
    acuApp.cama1 = new constructorCama("Cama principal", 10, "Litros", 10, 25.5, 51, "Cm", "Rojo", 5, "Piedra volcánica");
    acuApp.cama1.agregarPlanta("zanahoria1", "hortaliza", false, "planton");
    acuApp.cama1.agregarPlanta("zanahoria2", "hortaliza", true, "cosechable");
    acuApp.cama1.agregarPlanta("zanahoria3", "hortaliza", false, "semilla");
    acuApp.cama1.agregarPlanta("zanahoria4", "hortaliza", false, "semilla");
    var zanahoriaDescartada = acuApp.cama1.quitarPlanta("zanahoria4");
    acuApp.tanque1.agregarPez("Koi1", "aguas fria", 200);
    acuApp.tanque1.agregarPez("Koi2", "aguas fria", 200);
    acuApp.tanque1.agregarPez("pleco", "invasora", 400, 0.5);
    acuApp.tanque1.agregarPez("pleco2", "invasora", 1000, 1.5);
    var plecoDescartado = acuApp.tanque1.quitarPez("pleco2");
```


**POO (Avanzado)**

- Usando this:
	```javascript
	var objeto = {
	    valor: 0,
	    incrementar: function(incremento){
	       this.valor += incremento;
	    }
	};

	objeto.incrementar(6);
	```


- Alternado el valor de this:
	- ERROR!:
	```javascript
	var objeto = {
	    valor: 0,
	    incrementar: function(incremento){
	       function otraFuncion(unValor){
	           this.valor += unValor;
	       }
	       otraFuncion(incremento);
	    }
	};

	objeto.incrementar(6);
	```

	- CORRECTO:
	```javascript
	var objeto = {
	    valor: 0,
	    incrementar: function(incremento){
	       var esto = this; // "esto" puede ser "that"
	       function otraFuncion(unValor){
	           esto.valor += unValor;
	       }
	       otraFuncion(incremento);
	    }
	};

	objeto.incrementar(6);
	```


- Usando this en Constructor:
	```javascript
	var fabricaPersonas = function(){
	    this.nombre = 'Pepe';
	};

	fabricaPersonas.prototype.mostrarNombre = function(){
	    console.log(this.nombre);
	};

	var miPersona = new fabricaPersonas();
	miPersona.mostrarNombre();
	```


- Usando *.apply()* para modificar el contexto del *this*:
	```javascript
	var fabricaPersonas  = function(){
	    this.nombre = 'Pepe';
	};

	fabricaPersonas.prototype.mostrarNombre = function(){
	    console.log(this.nombre);
	};

	var otroObjeto = {
	    nombre: 'Oscar'
	};

	var miPersona = new fabricaPersonas();
	miPersona.mostrarNombre();
	miPersona.mostrarNombre.apply(otroObjeto);
	```


- Modificación de contexto con *.call()*:
	```javascript
	var objeto = {
	  multiplicador: 2,
	  sumatorio: function(num1, num2){
	     return (num1 + num2) * this.multiplicador;
	  }
	};

	var resultado = objeto.sumatorio(2,2);
	console.log(resultado);


	var cambio = {
	  multiplicador: 5
	};

	var resultado = objeto.sumatorio.call(cambio, 5, 5);
	console.log(resultado);
	```


- Modificación de contexto con *.apply()*:
	```javascript
	var objeto = {
	  multiplicador: 2,
	  sumatorio: function(num1, num2){
	     return (num1 + num2) * this.multiplicador;
	  }
	};

	var resultado = objeto.sumatorio(2,2);
	console.log(resultado);


	var cambio = {
	  multiplicador: 5
	};

	var resultado = objeto.sumatorio.apply(cambio, [5,5]);
	console.log(resultado);
	```


- Modificación de contexto con *.bind()*:
	```javascript
	var objeto = {
	  multiplicador: 2,
	  sumatorio: function(num1, num2){
	     return (num1 + num2) * this.multiplicador;
	  }
	};

	var resultado = objeto.sumatorio(2,2);
	console.log(resultado);

	var cambio = {
	  multiplicador: 5
	};

	var cambiandoFuncion = objeto.sumatorio.bind(cambio);
	var resultado = cambiandoFuncion(5, 5);
	console.log(resultado);

	```


**Trabajando con prototipos**

- .hasOwnProperty():
	```javascript
	var o = new Object();
	o.prop = 'exists';

	function changeO() {
	  delete o.prop;
	}

	o.hasOwnProperty('prop');
	changeO();
	o.hasOwnProperty('prop');
	```


- .create():
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


- .isPrototypeOf():
	```javascript
	console.log(coche.isPrototypeOf(clonCoche));
	```


- .valueOf():
	```javascript
	var str = "Hello World!";
	var res = str.valueOf();
	console.log(res);
	```


- .constructor():
	```javascript
	function arbol (nombre) {
	   this.nombre = nombre;
	}

	var miArbol = new arbol( "Pino" );
	console.log( "miArbol.constructor es " + miArbol.constructor );
	```


- .toLocalString():
	```javascript
	var date = new Date();
	console.log(date.toLocaleString('es-ES'));
	console.log(date.toLocaleString('en-US'));
	console.log(date.toLocaleString('ko-KR'));
	```


- .toString():
	```javascript
	function Perro(nombre, criadero, color, sexo) {
	   this.nombre=nombre;
	   this.criadero=criadero;
	   this.color=color;
	   this.sexo=sexo;
	}

	var elPerro = new Perro("Gabby","Laboratorio","chocolate","femenino");

	elPerro.toString();

	Perro.prototype.toString = function perroToString() {
	  var retorno = "Perro " + this.nombre + " es " + this.sexo + " " + this.color + " " + this.criadero;
	  return retorno;
	};

	elPerro.toString();
	```