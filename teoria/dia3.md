### Reintroducción a JS

**Off topic**

- 20% de descuento para [dotcss](http://www.dotcss.io/). Paris, 5 Diciembre. Conferencia más grande sobre CSS en Europa.

![ITHumor](http://www.commitstrip.com/wp-content/uploads/2015/10/Strip-Retour-de-conf%C3%A9rence-650-finalenglish1.jpg)

**If... else**

- Estructura:
    ```javascript
    /* IF ...ELSE
    if (-algo verdadero-) {
        -ejecutaremos este código-
    } else {
        -Si lo anterior no era verdadero, se ejecutara este código-
    };
    */
    ```

- Documentación:
    - [If... else en w3schools](http://www.w3schools.com/js/js_if_else.asp)
    - [If... else en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)

- Ejemplo:
    ```javascript
    if (true) {
        console.log("true, por eso me ejecuto");
    } else {
        console.log("false, por eso me ejecuto");
    }
    ```


**Else if...**

```javascript
function testCondiccion (condicion){
    if (condicion == 1) {
        console.log("1, por eso me ejecuto");
    } else if (condicion == 2){
        console.log("2, por eso me ejecuto");
    } else {
        console.log("no es 1 o 2, por eso me ejecuto");
    }
}
```


**AND(&&)**

Elemento 1 | Elemento 2 | Resultado
------------ | ------------- | -------------
true | true | true
true | false | false
false | false | false
false | true | false


**OR(||)**

Elemento 1 | Elemento 2 | Resultado
------------ | ------------- | -------------
true | true | true
true | false | true
false | false | false
false | true | true


```javascript
var ex1 = true && true; // true
var ex2 = (2 == 2) && (3 >= 6); // false
var ex3 = (2>3) || (17 <= 40); // true
var ex4 = false || false; // false

function condicionalAvanzado ( paraComparar ) {
    if (paraComparar) {
        console.log("Verdadero!");
    } else {
        console.log("falso!");
    };
};
```


**Interacción Básica con el Usuario**

- alert():
    ```javascript
    alert("¡Bienvenido a esta web!");
    ```

- confirm():
    ```javascript
    confirm("¿Esta seguro que desea abandonar esta web?");
    ```


- Ejemplo:
    ```javascript
    var respuesta = confirm("presiona un botón!");
    if (respuesta === true) {
        console.log("Has aceptado!");
    } else {
        console.log("Has cancelado");
    }
    ```

- prompt():
    ```javascript
    prompt("¿Como te llamas?");
    ```

- Registremos los datos en una variable:
    ```javascript
    var nombre = prompt("¿Como te llamas?");
    ```


**Arrays**

- Creando un array:
    ```javascript
    var arreglo = [];
    arreglo = [1, "platano", "piscina", "manzana", true];
    ```

- Usando el Índice:
    ```javascript
    arreglo[1];
    ```

- Cambiar un valor del Índice:
    ```javascript
    arreglo[0] = "fresa";
    arreglo[4] = "pera";
    arreglo[2] = "limón";
    ```

- Índice total:
    ```javascript
    arreglo.length;
    ```

- .push() *Añadir elemento al índice*:
    ```javascript
    arreglo.push("nuevo");
    ```

- .pop() *Eliminar el último elemento del índice*:
    ```javascript
    arreglo.pop();
    ```

- .shift() *Eliminar el primer elemento*:
    ```javascript
    arreglo.shift();
    ```

- delete *sobrescribe a undefined*
    ```javascript
    delete arreglo[0];
    ```

- Elementos vacios:
    ```javascript
    arreglo[0] = undefined;
    ```

- .splice() *Borrar*:
    ```javascript
    var manzana = arreglo.splice(3, 1);
    ```

- .map():
    ```javascript
    var arreglo = ["plátano", "fresa", "lima", "manzana"];
    var resultado = arreglo.map(function (elemento){return elemento + " modificado!"});
    console.log(resultado);
    ```



**Arreglos avanzados**
```javascript
var arreglo1 = ["plátano", "fresa", "lima", "manzana"];
var arreglo2 = ["entrante", "primero", "segundo", "postre"];

var juntandoArreglos = [arreglo1, arreglo2];

function testArreglos () {
    console.log(juntandoArreglos[0][0]);
    console.log(juntandoArreglos[1][3]);
};
```


**Ejercicios**

8 - **#simplifiquemos!** Quiero solo un bucle para todo.

```javascript
    var trenesOperativos = 8;
    var totalTrenes = 12;

    function estadoDetalle () {
    	for(var numeroTren = 1; numeroTren <= totalTrenes; numeroTren++) {
    		if (numeroTren <= trenesOperativos) {
    			console.log("El tren número "+numeroTren+" esta funcionando");
    		}else {
    			console.log("El tren número "+numeroTren+" esta parado");
    		};		
    	};
    };
```

9 - **#compliquemos!** Servicio nocturno en el tren 10.
*Nota: Frente al ejercicio anterior, en este caso queremos que siempre que hablemos del
tren 10 se especifique que es nocturno. Independientemente de si esta parado o funcionando.*

```javascript
    var trenesOperativos = 8;
    var totalTrenes = 12;

    function estadoDetalle () {
    	for(var numeroTren = 1; numeroTren <= totalTrenes; numeroTren++) {
    		if ((numeroTren <= trenesOperativos) && (numeroTren != 10)) {
    			console.log("El tren numero "+numeroTren+" esta funcionando");
    		} else if (numeroTren == 10){
    			console.info("IMPORTANTE: El tren número "+numeroTren+" es nocturno");
    		} else {
    			console.log("El tren numero "+numeroTren+" esta parado");
    		};		
    	};
    };
```


10 - Refactoricemos - ¿Y si todos los trenes están en las vías funcionando o por el contrario si ninguno de los trenes esta funcionando?.

```javascript
    var trenesOperativos = 8;
    var totalTrenes = 12;

    function estadoDetalle () {
    	if (trenesOperativos > 0) {
    		if(trenesOperativos == totalTrenes){
    			console.log("Todos los trenes estan funcionando");
    		} else {
    			for(var numeroTren = 1; numeroTren <= totalTrenes; numeroTren++) {
    				if ((numeroTren <= trenesOperativos)  && (numeroTren != 10)) {
    					console.log("El tren numero "+numeroTren+" esta funcionando");
    				} else if (numeroTren == 10){
    					console.log("IMPORTANTE: El tren numero "+numeroTren+" es nocturno");
    				} else {
    					console.log("El tren numero "+numeroTren+" esta parado");
    				};		
    			};
    		};
    	} else {
    		console.log("IMPORTANTE: Ningún tren esta funcionando");
    	};
    };
```

11 - El servicio nocturno se queda un poco corto y necesitamos añadir un nuevo tren de refuerzo.
El 12 será destinado a cubrir esta necesidad, exactamente igual que el 10 anteriormente.

```javascript
    var trenesOperativos = 8;
    var totalTrenes = 12;

    function estadoDetalle () {
    	if (trenesOperativos > 0) {
    		if(trenesOperativos == totalTrenes){
    			console.log("Todos los trenes están funcionando");
    		} else {
    			for(var numeroTren = 1; numeroTren <= totalTrenes; numeroTren++) {
    				if ((numeroTren <= trenesOperativos) && (numeroTren != 10) && (numeroTren != 12)) {
    					console.log("El tren numero "+numeroTren+" esta funcionando");
    				} else if (numeroTren == 10 || numeroTren == 12){
    					console.log("IMPORTANTE: El tren numero "+numeroTren+" es nocturno");
    				} else {
    					console.log("El tren numero "+numeroTren+" esta parado");
    				};		
    			};
    		};
    	} else {
    		console.log("IMPORTANTE: Ningún tren esta funcionando");
    	};
    };
```


12 - El departamento de Marketing ha decidido lanzar un nuevo servicio los sábados.
 El "tren fiestero" será un tren adaptado a un público más intrépido y funcionará solo en los sábados.
 Este tren será el número 3.

*NOTA: EL TREN 3 SOLO FUNCIONA LOS SÁBADOS. Es necesario incluir el día de la semana en tu código*

```javascript
    var trenesOperativos = 8;
    var totalTrenes = 12;
    var diaSemana = "Sabado";
    function estadoDetalle () {
    	if (trenesOperativos > 0) {
    		if(trenesOperativos == totalTrenes){
    			console.log("Todos los trenes están funcionando");
    		} else {
    			for(var numeroTren = 1; numeroTren <= totalTrenes; numeroTren++) {
    				if (numeroTren <= trenesOperativos  && numeroTren != 3 && numeroTren != 10 && numeroTren != 12) {
    					console.log("El tren numero "+numeroTren+" esta funcionando");
    				} else if (numeroTren == 10 || numeroTren == 12){
    					console.info("IMPORTANTE: El tren numero "+numeroTren+" es nocturno");
    				} else if (numeroTren == 3 && diaSemana == "Sabado"){
    					console.info("El tren fiestero("+numeroTren+") esta funcionando.")
    				} else if (numeroTren == 3 && diaSemana != "Sabado"){
    					console.info("El tren fiestero("+numeroTren+") funcionará el sabado.")
    				} else {
    					console.log("El tren numero "+numeroTren+" esta parado");
    				};		
    			};
    		};
    	} else {
    		console.log("IMPORTANTE: Ningún tren esta funcionando");
    	};
    };
```



**Funciones**

- Propiedad *name*:
    ```javascript
	function miFuncion (){
		// vacia
	};

	console.log(miFuncion.name);
    ```


- Declaración y ejecución:
    ```javascript
	function dameTrue (){
		return true
	};

	function dameFalse () {
		return false
	};

	dameTrue();
	dameFalse();
    ```

- Invocación e introducción a *this*:
	- como función (*this* contexto *window*)
		```javascript
		function ambitoGlobal () {
			return this;
		}
		
		ambitoGlobal()
		```
	- como método en un objeto (*this* contexto objeto al que pertenece el método)
		```javascript
		var objeto = {};
		
		objeto.miMetodo = function () {
			return this;
		}
		
		objeto.miMetodo();
		```		
	- como constructor de un objeto (*this* contexto objeto creado)
	- .apply() y .call() (modificación explícita de *this*)

- Argumentos:
	- El exceso de argumentos no es un problema
	- La falta de argumento crea un valor indefinido
    - El Objeto Arguments no es un Array, solo es similar.
    ```javascript    
	
	function pruebaArguemntos () {
	console.log(arguments);
	console.info(arguments[0]);
	console.info(arguments[1]);
	}
	
	pruebaArguemntos (1, "vale", true);
	
	```


- [Objeto Arguments](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Funciones/arguments)


- Sumar cuadrados.

```javascript
	function sumaCuadrados (a, b) {
		return (a*a) + (b*b);
	};
```



**Funciones (Scope)**

- Declaración y ejecución:
    ```javascript
	var numero = 450;
	var otroNumero = 23;

	function sumaCuadrados (a, b) {
		var numero = a;
		var otroNumero = b;
		var calculo = (numero*numero) + (otroNumero*otroNumero);
		console.log("\"numero\" es \""+numero+"\", local");
		console.log("\"otroNumero\" es \""+otroNumero+"\", local");
	};

	function verificarGlobales() {
		console.log("\"numero\" es \""+numero+"\", global");
		console.log("\"otroNumero\" es \""+otroNumero+"\", global");
	};
    ```