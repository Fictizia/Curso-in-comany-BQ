# Dia 5

### JS avanzado (POO)

**POO**

- Entendiendo los objetos:
	```javascript
	/*
	[Objeto = Prototípo]{
	    [ Propiedad = Variable ]
	    [ Método = Función ]
	}
	*/
	```


- Constructor de Objetos:
	```javascript
	var coche = function (parametros) {
	    /* Codigo*/
	};
	```


- Propiedades del Objeto:
	```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad
	    this.color = color;
	    this.tipo = tipo;
	};
	```


- Data-typing:
	```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	    if (isNaN(this.antiguedad)) {
	        console.log("Error en el data-typing, antiguedad no es un número");
	    }
	};

	var miCoche = new coche ("Seat", "Panda", 20, "azul", "turismo");
	console.log("Tu coche es un "+miCoche.marca+" "+miCoche.modelo+" con "+miCoche.antiguedad+" años, clase "+miCoche.tipo+" y color "+miCoche.color);
	```


- Métodos (En el Constructor):
	```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	    if (isNaN(this.antiguedad)) {
	        console.log("Error en el data-typing, antiguedad no es un número");
	    }
	    this.detalles = function(){
	      console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
	    }
	};

	var miCoche = new coche ("Seat", "Panda", 20, "azul", "turismo");
	miCoche.detalles();
	```


- Métodos (Extensión del prototipo):
	```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	    if (isNaN(this.antiguedad)) {
	        console.log("Error en el data-typing, antigüedad no es un número");
	    }
	};

	coche.prototype.detalles = function(){
	  console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
	}

	var miCoche = new coche ("Seat", "Panda", 20, "azul", "turismo");
	miCoche.detalles();
	```


- Métodos (Vinculación Externa):
	```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	    if (isNaN(this.antiguedad)) {
	        console.log("Error en el data-typing, antigüedad no es un número");
	    }
	    this.detalles = dameDetalles;
	};

	function dameDetalles(){
	  console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
	}

	var miCoche = new coche ("Seat", "Panda", 20, "azul", "turismo");
	miCoche.detalles();
	```


- Herencia:
	```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	    if (isNaN(this.antiguedad)) {
	        console.log("Error en el data-typing, antigüedad no es un número");
	    }
	    this.detalles = dameDetalles;
	};

	var furgon = function (taraMinima, cargaUtil, volumenCarga) {
	    this.taraMinima = taraMinima;
	    this.cargaUtil = cargaUtil;
	    this.volumenCarga = volumenCarga;
	    if (isNaN(this.taraMinima) || isNaN(this.cargaUtil) || isNaN(this.volumenCarga)) {
	        console.log("Error en los datos. Por favor usar solo valores numéricos.");
	    }
	    this.detallesTecnicos = detallesTecnicos;
	};


	function dameDetalles(){
	  console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
	}

	function detallesTecnicos(){
	  console.warn("Tu coche tiene una Tara mínima de "+this.taraMinima+". Carga útil de "+this.cargaUtil+" y un volumen de carga de "+this.volumenCarga+"m3");
	}

	var miPickup = new coche ("Land Rover", "Santana Aníbal", 35, "Marrón tierra", "4x4");
	miPickup.prototype = new furgon (1200, 768, 4.5);


	miPickup.detalles();
	miPickup.prototype.detallesTecnicos();
	```

- Herencia (simplificada):
	```javascript
	var perro  = function () {
	    this.patas = 4;
	    this.ojos = 2;
	};

	var pastorAleman = function () {
	    this.colorLengua = "negra";
	    this.colorOjos = "marrón";
	    this.capacidadTrabajo = true;
	    this.especialidad = "Pastoreo";
	};

	pastorAleman.prototype = new perro();

	var miPerro = new pastorAleman();
	console.log("Número patas: "+miPerro.patas+"\n Número ojos: "+miPerro.ojos+"\n Color Lengua: "+miPerro.colorLengua+"\n Color ojos: "+miPerro.colorOjos+"\n Capacidad de trabajo: "+miPerro.capacidadTrabajo+"\n Especialidad: "+miPerro.especialidad);
	```


- Eliminando restricciones en los argumentos:
	```javascript
	var cocheEmpresa = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = "" || tipo;
	    var ITVPasada = true;
	    var ITVfrecuencia = "Cada año";
	    var seguroEnRegla = true;
	    var companySeguros = "SegurExpress";
	    var tipoSeguro = "a terceros";
	    if (this.tipo == ""){
	        this.tipo = "berlina";
	    }


	    function dameDetalles(){
	      console.log("Tu coche es un "+marca+" "+modelo+" con "+antiguedad+" años, clase "+tipo+" y color "+color);
	    }

	    function datosPrivados() {
	        if (ITVPasada && seguroEnRegla)
	            console.info("INFO: Todo en Regla, tienes que pasar la ITV "+ITVfrecuencia+". Tienes un seguro "+tipoSeguro+" con "+companySeguros);
	        else{
	            console.error("ALERTA! El coche no puede usarse. El seguro o la ITV no esta en regla.");
	        }
	    }

	    datosPrivados();
	    dameDetalles();
	};

	var miCoche = new cocheEmpresa ("Audi", "S8", 2, "negro", "Berlina");
	```


- Creando un ID:
	```javascript
	var contador = 0;

	var cocheEmpresa = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = "" || tipo;
	    this.id = contador++;
	    var ITVPasada = true;
	    var ITVfrecuencia = "Cada año";
	    var seguroEnRegla = true;
	    var companySeguros = "SegurExpress";
	    var tipoSeguro = "a terceros";
	    if (this.tipo == ""){
	        this.tipo = "berlina";
	    }

	    function dameDetalles(){
	      console.log("Tu coche es un "+marca+" "+modelo+" con "+antiguedad+" años, clase "+tipo+" y color "+color);
	    }

	    function datosPrivados() {
	        if (ITVPasada && seguroEnRegla)
	            console.info("INFO: Todo en Regla, tienes que pasar la ITV "+ITVfrecuencia+". Tienes un seguro "+tipoSeguro+" con "+companySeguros);
	        else{
	            console.error("ALERTA! El coche no puede usarse. El seguro o la ITV no esta en regla.");
	        }
	    }

	    function identificador(){
	        console.warn("Recuerda! Tu coche esta identificado como coche numero "+contador);
	    }

	    datosPrivados();
	    dameDetalles();
	    identificador();
	};

	var miCoche = new cocheEmpresa ("Audi", "S8", 2, "negro", "Berlina");
	var otroCoche = new cocheEmpresa ("Audi", "A8", 5, "gris", "Berlina");
	var miCoche2 = new cocheEmpresa ("Seat", "Ibiza", 9, "rojo", "Utilitario");
	```


- Extensión de objetos nativos (usando prototipos):
	```javascript
	Array.prototype.coincidencias = function(palabra) {
	    var coincidencias = 0;
	    for (var i=0; i<this.length; i++) {
	        if (this[i] == palabra) {
	            coincidencias++;
	        }
	    }
	    console.warn("Se encontraron "+coincidencias+" coincidencia(s) de la palabra");
	};


	var amigos = ["Charlie", "Marco", "Luis", "Jose", "Miguel", "Jose", "Luis", "Oscar"];
	amigos.coincidencias("Jose");
	```

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
	
	
**Ejercicios**

4 - Añadamos al sistema la posibilidad de saber las condiciones del agua y del ecosistema:
- total peces por tipo
- total hortalizas por tipo
- Propiedades del agua: 
	- Nitratos(NO3 mg/l)
	- Nitritos (NO2 mg/l)
	- Dureza Sales (GH)
	- Carbonatos (KH)
	- Ph (Ph)
	- Cloro (CL2 mg/l)

Nota: [For... in](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Sentencias/for...in) te resultará de gran utilidad.

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

	    this.agregarAgua = function(litros, nitratos, nitritos, durezaSales, carbonatos, ph, cloro){
	        this.calidadAgua = this.calidadAgua || {};
	        // Nitratos
	        this.calidadAgua["nitratos"] = this.calidadAgua["nitratos"] || {};
	        this.calidadAgua["nitratos"]["valor"] = nitratos || 10;
	        this.calidadAgua["nitratos"]["medida"] = "mg/l";
	        this.calidadAgua["nitratos"]["simbolo"] = "NO3";
	        // Nitritos
	        this.calidadAgua["nitritos"] = this.calidadAgua["nitritos"] || {};
	        this.calidadAgua["nitritos"]["valor"] = nitritos || 0.5;
	        this.calidadAgua["nitritos"]["medida"] = "mg/l";
	        this.calidadAgua["nitritos"]["simbolo"] = "NO2";
	        // Dureza de Sales
	        this.calidadAgua["dureza de sales"] = this.calidadAgua["dureza de sales"] || {};
	        this.calidadAgua["dureza de sales"]["valor"] = durezaSales || ">7ºd";
	        this.calidadAgua["dureza de sales"]["medida"] = "N/A";
	        this.calidadAgua["dureza de sales"]["simbolo"] = "GH";
	        // Carbonatos
	        this.calidadAgua["carbonatos"] = this.calidadAgua["carbonatos"] || {};
	        this.calidadAgua["carbonatos"]["valor"] = carbonatos || "6ºd";
	        this.calidadAgua["carbonatos"]["medida"] = "N/A";
	        this.calidadAgua["carbonatos"]["simbolo"] = "KH";
	        // PH
	        this.calidadAgua["ph"] = this.calidadAgua["ph"] || {};
	        this.calidadAgua["ph"]["valor"] = ph || 7.2;
	        this.calidadAgua["ph"]["medida"] = "N/A";
	        this.calidadAgua["ph"]["simbolo"] = "PH";
	        // Cloro (CL2 mg/l)
	        this.calidadAgua["cloro"] = this.calidadAgua["cloro"] || {};
	        this.calidadAgua["cloro"]["valor"] = cloro || 0.2;
	        this.calidadAgua["cloro"]["medida"] = "mg/l";
	        this.calidadAgua["cloro"]["simbolo"] = "CL2";
	        // Manejo de caudal
	        this.nivelAgua += litros;
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

	    this.calcularFrios = function(){
	        var numero = 0;
	        for (var key in this.peces){
	            if(this.peces[key].clase == "aguas fria"){
	                numero++;
	            }
	        }
	        this.peces["total aguas fria"] = numero;
	    };    

	    this.calcularInvasores = function(){
	        var numero = 0;
	        for (var key in this.peces){
	            if(this.peces[key].clase == "invasora"){
	                numero++;
	            }
	        }
	        this.peces["total invasora"] = numero;
	    };

	    this.estadoGeneral = function(){

	        this.calcularInvasores();    
	        this.calcularFrios();

	        var resumenGeneral = "================================\n";
	        resumenGeneral += "Estado del Agua ("+this.nombre+")\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Agua disponible: "+this.nivelAgua+"/"+nivelAguaMaximo+"l\n";
	        resumenGeneral += "Nitratos("+this.calidadAgua["nitratos"]["simbolo"]+"): "+this.calidadAgua["nitratos"]["valor"]+this.calidadAgua["nitratos"]["medida"]+"\n";
	        resumenGeneral += "Nitritos("+this.calidadAgua["nitritos"]["simbolo"]+"): "+this.calidadAgua["nitritos"]["valor"]+this.calidadAgua["nitritos"]["medida"]+"\n";
	        resumenGeneral += "Dureza de sales("+this.calidadAgua["dureza de sales"]["simbolo"]+"): "+this.calidadAgua["dureza de sales"]["valor"]+"\n";
	        resumenGeneral += "Carbonatos("+this.calidadAgua["carbonatos"]["simbolo"]+"): "+this.calidadAgua["carbonatos"]["valor"]+"\n";
	        resumenGeneral += "Ph("+this.calidadAgua["ph"]["simbolo"]+"): "+this.calidadAgua["ph"]["valor"]+"\n";
	        resumenGeneral += "Cloro("+this.calidadAgua["cloro"]["simbolo"]+"): "+this.calidadAgua["cloro"]["valor"]+this.calidadAgua["cloro"]["medida"]+"\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Estado de los Peces\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Total de Agua Fria: "+this.peces["total aguas fria"]+"\n";
	        resumenGeneral += "Total de Invasores: "+this.peces["total invasora"]+"\n";
	        resumenGeneral += "================================\n";

	        console.log(resumenGeneral);
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

	    this.agregarAgua = function(litros, nitratos, nitritos, durezaSales, carbonatos, ph, cloro){
	        this.calidadAgua = this.calidadAgua || {};
	        // Nitratos
	        this.calidadAgua["nitratos"] = this.calidadAgua["nitratos"] || {};
	        this.calidadAgua["nitratos"]["valor"] = nitratos || 10;
	        this.calidadAgua["nitratos"]["medida"] = "mg/l";
	        this.calidadAgua["nitratos"]["simbolo"] = "NO3";
	        // Nitritos
	        this.calidadAgua["nitritos"] = this.calidadAgua["nitritos"] || {};
	        this.calidadAgua["nitritos"]["valor"] = nitritos || 0.5;
	        this.calidadAgua["nitritos"]["medida"] = "mg/l";
	        this.calidadAgua["nitritos"]["simbolo"] = "NO2";
	        // Dureza de Sales
	        this.calidadAgua["dureza de sales"] = this.calidadAgua["dureza de sales"] || {};
	        this.calidadAgua["dureza de sales"]["valor"] = durezaSales || ">7ºd";
	        this.calidadAgua["dureza de sales"]["medida"] = "N/A";
	        this.calidadAgua["dureza de sales"]["simbolo"] = "GH";
	        // Carbonatos
	        this.calidadAgua["carbonatos"] = this.calidadAgua["carbonatos"] || {};
	        this.calidadAgua["carbonatos"]["valor"] = carbonatos || "6ºd";
	        this.calidadAgua["carbonatos"]["medida"] = "N/A";
	        this.calidadAgua["carbonatos"]["simbolo"] = "KH";
	        // PH
	        this.calidadAgua["ph"] = this.calidadAgua["ph"] || {};
	        this.calidadAgua["ph"]["valor"] = ph || 7.2;
	        this.calidadAgua["ph"]["medida"] = "N/A";
	        this.calidadAgua["ph"]["simbolo"] = "PH";
	        // Cloro (CL2 mg/l)
	        this.calidadAgua["cloro"] = this.calidadAgua["cloro"] || {};
	        this.calidadAgua["cloro"]["valor"] = cloro || 0.2;
	        this.calidadAgua["cloro"]["medida"] = "mg/l";
	        this.calidadAgua["cloro"]["simbolo"] = "CL2";
	        // Manejo de caudal
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

	    this.calcularHortalizas = function(){
	        var numero = 0;
	        for (var key in this.plantas){
	            if(this.plantas[key].clase == "hortaliza"){
	                numero++;
	            }
	        }
	        this.plantas["total hortalizas"] = numero;
	    };

	    this.estadoGeneral = function(){

	        this.calcularHortalizas();

	        var resumenGeneral = "================================\n";
	        resumenGeneral += "Estado del Agua ("+this.nombre+")\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Agua disponible: "+this.nivelAgua+"/"+nivelAguaMaximo+"l\n";
	        resumenGeneral += "Nitratos("+this.calidadAgua["nitratos"]["simbolo"]+"): "+this.calidadAgua["nitratos"]["valor"]+this.calidadAgua["nitratos"]["medida"]+"\n";
	        resumenGeneral += "Nitritos("+this.calidadAgua["nitritos"]["simbolo"]+"): "+this.calidadAgua["nitritos"]["valor"]+this.calidadAgua["nitritos"]["medida"]+"\n";
	        resumenGeneral += "Dureza de sales("+this.calidadAgua["dureza de sales"]["simbolo"]+"): "+this.calidadAgua["dureza de sales"]["valor"]+"\n";
	        resumenGeneral += "Carbonatos("+this.calidadAgua["carbonatos"]["simbolo"]+"): "+this.calidadAgua["carbonatos"]["valor"]+"\n";
	        resumenGeneral += "Ph("+this.calidadAgua["ph"]["simbolo"]+"): "+this.calidadAgua["ph"]["valor"]+"\n";
	        resumenGeneral += "Cloro("+this.calidadAgua["cloro"]["simbolo"]+"): "+this.calidadAgua["cloro"]["valor"]+this.calidadAgua["cloro"]["medida"]+"\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Estado de las Plantas\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Total Hortalizas: "+this.plantas["total hortalizas"]+"\n";

	        console.log(resumenGeneral);
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
	acuApp.cama1.agregarAgua(100);
	acuApp.tanque1.agregarAgua(987, 25, 0.5, ">14ºd", "3ºd", 8.0, 0.4);
	acuApp.tanque1.estadoGeneral();
	acuApp.cama1.estadoGeneral();
```

	
### Firebase

![FirebaseLogo](http://decks.mbleigh.com/images/firebase_logo.png)

- [Firebase Pricing](https://www.firebase.com/pricing.html)
- [Firebase Features](https://www.firebase.com/features.html)
- [Firebase Docs](https://www.firebase.com/docs/)
- [Firebase - Backbone](https://www.firebase.com/docs/web/libraries/backbone/quickstart.html)
- [Firebase - Angular](https://www.firebase.com/docs/web/libraries/angular/quickstart.html)
- [Firebase - Nodejs/js](https://www.firebase.com/docs/web/quickstart.html)

**Ejemplos**

- [Firebase - Open Data Sets](https://www.firebase.com/docs/open-data/)
- [Firebase - Cryptocurrencies](https://www.firebase.com/docs/open-data/cryptocurrencies.html)
- [Firebase - Parking](https://www.firebase.com/docs/open-data/parking.html)
- [Firebase - Bus](https://www.firebase.com/docs/open-data/transit.html)
- [Firebase - Weather](https://www.firebase.com/docs/open-data/weather.html)


**Primeros pasos**

- Crear una cuenta:
  - [SignUp](https://www.firebase.com/signup/)
  
- Gestionar dependéncias en cliente:
```javascript
  <script src="https://cdn.firebase.com/js/client/2.2.9/firebase.js"></script>
```

- Gestionar dependéncias en Nodejs:
```
  npm install firebase -save
```


**Limitaciones**

- [Limitaciones técnicas](https://www.firebase.com/docs/web/guide/understanding-data.html#section-limitations)
- [Conversión de Arrays](https://www.firebase.com/docs/web/guide/understanding-data.html#section-arrays-in-firebase)


**Guardando Datos**

- [Guardando datos en Firebase](https://www.firebase.com/docs/web/guide/saving-data.html#section-ways-to-save)
- set() Almacena / remplaza los datos
- update() Actualzia los datos
- push() Alamacena los datos con un ID único.
- transaction() Para datos complejos y cocurridos.




- set():

```javascript
  var ref = new Firebase("https://<<---URL--->>.firebaseio.com/fb-ejemplos/escritura");
  var usersRef = ref.child("users");
  usersRef.set({
    alanisawesome: {
      date_of_birth: "June 23, 1912",
      full_name: "Alan Turing"
    },
    gracehop: {
      date_of_birth: "December 9, 1906",
      full_name: "Grace Hopper"
    }
  });
```

```javascript
  var ref = new Firebase("https://<<---URL--->>.firebaseio.com/fb-ejemplos/escritura");
  usersRef.child("alanisawesome").set({
    date_of_birth: "June 23, 1912",
    full_name: "Alan Turing"
  });
  usersRef.child("gracehop").set({
    date_of_birth: "December 9, 1906",
    full_name: "Grace Hopper"
  });
```


- update():

```javascript
  var hopperRef = usersRef.child("gracehop");
  hopperRef.update({
    "nickname": "Amazing Grace"
  });
```

- push():

```javascript
// Callbacks y IDs
  var dataRef = ref.child("IDs");
  dataRef.push("Guardando datos...", function(error) {
    if (error) {
      alert("No se han podido guardar los datos." + error);
    } else {
      alert("Datos guardados con exito.");
    }
  });
```


**Eventos**

- Evento (value):

```javascript
  var ref = new Firebase("https://docs-examples.firebaseio.com/web/saving-data/fireblog/posts");
  
  ref.on("value", function(snapshot) {
    console.log(snapshot.val());
  }, function (errorObject) {
    console.log("The read failed: " + errorObject.code);
  });
```


- Evento (child_changed):

```javascript
  var ref = new Firebase("https://<<--URL-->>.firebaseio.com/fb-ejemplos/escritura/users");
  
  ref.on("child_changed", function(snapshot) {
    var usersData = snapshot.val();
    console.log("Nueva fecha nacimiento: " + usersData.date_of_birth);
  });
```


- Evento (child_removed):

```javascript
  var ref = new Firebase("https://<<--URL-->>.firebaseio.com/fb-ejemplos/escritura/users");
  
  ref.on("child_removed", function(snapshot) {
    var usersData = snapshot.val();
    console.log("Usuario eliminado: " + usersData.full_name);
  });
```


- once() *una vez*:

```javascript
var ref = new Firebase("https://<<--URL-->>.firebaseio.com/fb-ejemplos/escritura/users");

ref.once("child_changed", function(snapshot) {
  var usersData = snapshot.val();
  console.log("Nueva fecha nacimiento: " + usersData.date_of_birth);
});
```


- Quitar evento (value):

```javascript
  ref.off("value");
```

- Quitar todos los eventos:

```javascript
  ref.off();
```


**Queries**

- [Firebase - Queries Part I](https://www.firebase.com/blog/2013-10-01-queries-part-one.html)
- [Firebase - Queries Part II](https://www.firebase.com/blog/2014-01-02-queries-part-two.html)
- [Firebase - Denormalizing is normal](https://www.firebase.com/blog/2013-04-12-denormalizing-is-normal.html)
- [Firebase Docs - Ordenando Datos](https://www.firebase.com/docs/web/guide/retrieving-data.html#section-ordered-data)
- orderByChild() Ordenar por hijo
- orderByKey() Ordenar por Llave
- orderByValue() Ordenar por valor
- orderByPriority() Ordenar por prioridad


- orderByChild():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByChild("height").on("child_added", function(snapshot) {
    console.log(snapshot.key() + " was " + snapshot.val().height + " meters tall");
  });
```

- orderByKey():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByKey().on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```

- orderByValue():

```javascript
  var scoresRef = new Firebase("https://dinosaur-facts.firebaseio.com/scores");
  scoresRef.orderByValue().on("value", function(snapshot) {
    snapshot.forEach(function(data) {
      console.log("The " + data.key() + " dinosaur's score is " + data.val());
    });
  });
```

**Queries Avanzadas**

- limitToFirst() desde el primero...
- limitToLast() desde el final...
- startAt() empiezan por...
- endAt() terminan por...
- equalTo() igual a...


- limitToFirst():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByChild("height").limitToFirst(2).on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```


- limitToLast():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByChild("weight").limitToLast(2).on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```


**Queries Avanzadas (concatenando)**

- .orderByValue() y .limitToLast():

```javascript
  var scoresRef = new Firebase("https://dinosaur-facts.firebaseio.com/scores");
  scoresRef.orderByValue().limitToLast(3).on("value", function(snapshot) {
    snapshot.forEach(function(data) {
      console.log("The " + data.key() + " dinosaur's score is " + data.val());
    });
  });
```


- .orderByChild() y .startAt():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByChild("height").startAt(3).on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```


- .orderByKey() y .endAt():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByKey().endAt("pterodactyl").on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```


- .startAt() y .endAt() *usando tilde*:

```javascript
var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
ref.orderByKey().startAt("b").endAt("b~").on("child_added", function(snapshot) {
  console.log(snapshot.key());
});
```

- .equalTo():

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.orderByChild("height").equalTo(25).on("child_added", function(snapshot) {
    console.log(snapshot.key());
  });
```


- Ejemplo: *Busquemos un dinosaurio que sea mas pequeño que un Stegosaurus*

```javascript
  var ref = new Firebase("https://dinosaur-facts.firebaseio.com/dinosaurs");
  ref.child("stegosaurus").child("height").on("value", function(stegosaurusHeightSnapshot) {
    var favoriteDinoHeight = stegosaurusHeightSnapshot.val();
  
    var queryRef = ref.orderByChild("height").endAt(favoriteDinoHeight).limitToLast(2)
    queryRef.on("value", function(querySnapshot) {
        if (querySnapshot.numChildren() == 2) {
          // Data is ordered by increasing height, so we want the first entry
          querySnapshot.forEach(function(dinoSnapshot) {
            console.log("The dinosaur just shorter than the stegasaurus is " + dinoSnapshot.key());
  
            // Returning true means that we will only loop through the forEach() one time
            return true;
          });
        } else {
          console.log("The stegosaurus is the shortest dino");
        }
    });
  });
```


**Trabajar Offline**

- [Documentación](https://www.firebase.com/docs/web/guide/saving-data.html#section-writes-offline)


- Realizando acciones al desconectarse:

```javascript
  var presenceRef = new Firebase('https://experimentos.firebaseio.com/info/connectednow');
  presenceRef.onDisconnect().set("I disconnected!");
  
```


**Seguridad y Autorización**

- [Ajustes de seguridad](https://www.firebase.com/docs/security/guide/securing-data.html)



**Autorización**

- [User Auth](https://www.firebase.com/docs/web/guide/user-auth.html)
- [Ejemplo en jsfiddle](http://jsfiddle.net/firebase/a221m6pb/embedded/result,js,css/)


**Deploy**

- [Deploy en Cloud](https://www.firebase.com/docs/web/guide/deploying.html)


**Ejercicios**

Crearemos un formulario de registro para un evento. Nuestro objetivo será ofrecer un formulario web que guarde los datos en Firebase. 

Objetivos:
- Es importante que no se inscriban multiples usuarios con una misma cuenta de email.
- Queremos también incluir la lista de las personas que ya se han inscrito en la misma pagina que el formulario.

![Party_joke_commitStrip](http://www.commitstrip.com/wp-content/uploads/2015/02/Strip-Saint-valentin-650-finalenglish.jpg)


- [Solución](../otros/formularioFirebase)	
	