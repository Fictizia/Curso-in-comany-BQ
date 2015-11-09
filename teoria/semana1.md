# Semana 1

### C9.io

**Creamos una cuenta y un workespace con referencia a nuestro repositorio de GitHub**
- [c9.io](https://c9.io/)

**Configurando GitHub**

- [Setup Git and basic commands](http://git-scm.com/book/es/v1/Empezando-Configurando-Git-por-primera-vez)

* Setup `git: git config remote.origin.push HEAD`.
 * `git config --global user.name "John Doe"`.
 * `git config --global user.email johndoe@example.com`.
* Git commands: `git status, git add, git rm, git pull, git commit -m "Commit message", git push`.

### Git y Github

Podéis encontrar todo el material de apoyo en este enlace

**Introducción**

[Como trabajar con Git](http://nvie.com/img/git-model@2x.png)
![Como trabajar con Git](http://nvie.com/img/git-model@2x.png)

[Diversos Entornos](http://www.rittmanmead.com/wp-content/uploads/2013/01/NewImage1.png)
![Diversos Entornos](http://www.rittmanmead.com/wp-content/uploads/2013/01/NewImage1.png)


**Instalación**

Instalamos [Git - Source Code Management](http://git-scm.com/)

Comprobamos la instalación

```
git --version
```


**Bienvenidos a la maquina del tiempo**
- Arquitectura de Árbol(working area, staging Area, Repository)
- Auditoria de código (quien? cuando? y que?)
- Git trabaja en binario (imagenes, docs, etc...)
- Git no guarda una copia de cada version, solo los cambios.
- Distribución (Repositorios y Clones)
- Opensource y funciona offline
- Consola vs. GUI



**Trabajando en Local**

Configuración (entornos):

[Repositorios locales y remotos](http://media.tumblr.com/tumblr_lbnpoxYtNm1qaku05.png)
![Repositorios locales y remotos](http://media.tumblr.com/tumblr_lbnpoxYtNm1qaku05.png)

- System (todos los usuarios)
    - git config --system
    - etc/gitconfig, /usr/local/git/etc/gitconfig

- Global (mi usuario)
    - git config --global
    - .gitconfig (usuario/root)

- Project (proyecto)
    - git config
    - /proyect/.git/config


**Comandos básicos**

versión
```
git --version
```

Grabando Nombre
```
git config --global user.name "nombre"
```

Comprobando el nombre
```
git config --global user.name
```

Grabando Email
```
git config --global user.email "email"
```

Habilitando colores
```
git config --global color.ui true
```

Ver usuarios en el equipo
```
git config --global --list
```


**GIT Working flow (local) - Básico**

- help (ayuda)

    - Ayuda general
    ```
    git config --global --list
    ```

    - Ayuda especifica
    ```
    git help push
    ```

    - Salir de la ayuda
    ```
    q (quit)
    ```

- init (arranque)
    - Buscamos la carpeta (ls, dir...)
    - Arrancando Git
    ```
    git init
    ```

- status
    - Verificar estado
    ```
    git status
    ```

- add
    - Añadiendo todo
    ```
    git add -A
    ```

    - Añadiendo todo *(como add -A, pero omite los archivos fuera de track)*
    ```
    git add .
    ```

    - Añadiendo un archivo especifico
    ```
    git add loquesea
    ```

- commit
    - Comentando el commit
    ```
    git commit -m "Mi primer commit"
    ```

- log
    - Verificando el estado de los commits
    ```
    git log
    ```

- reset (Reseteamos el proyecto hasta un punto dado (SIN RETORNO!))
    - No afecta al working area ni al Stagging Area, solo al repositorio
    ```
    git reset --soft NUMEROCOMMIT
    ```

    - No afecta al working area
    ```
    git reset --mixed NUMEROCOMMIT
    ```

    - Afecta a todos los niveles incluido el working area
    ```
    git reset --hard NUMEROCOMMIT
    ```

    - En caso de necesitar recuperación.
      Haz un reset --hard hacia delante, con el número del útimo commit.
      ```
      git reset --hard ULTIMOCOMMIT
      ```

    - Devolver un archivo de staging a working area
    ```
    git reset HEAD nombrearchivo
    ```    


**GIT Working flow (local) - Viajar en el tiempo**

- log
    - Hacemos una copia de seguridad de nuestros commits.
    ```
    git log > miscommits.txt
    ```

- checkout

    - Abrimos la maquina de tiempo
    ```
    git checkout NUMEROCOMMIT
    ```

    - Volvemos a Master
    ```
    git checkout master
    ```


**GIT Working flow (local) - Ramas (Branches)**

Ramas (Universos Paralelos)
*Línea master -> linea estable o principal.*
*Lineas secundarias -> lineas de desarrollo, bugs, experimentos, etc...*

- branch

    - Crear una rama
    ```
    git branch NOMBRERAMA
    ```

    - Ver ramas
    ```
    git branch
    ```    

    - Cambiar de rama
    ```
    git checkout NOMBRERAMA
    ```  

    - Ver cambios en formato ramas
    ```
    git log --oneline --graph --all
    ```  

    - Borrar una rama
    ```
    git branch -d NOMBRERAMA
    ```


**GIT Working flow (local) - Fusiones (básico)**

- Nos situamos en la rama que absorberá (principal)
    ```
    git checkout RAMAPRINCIAL
    ```

- Hacemos el *merge*
    ```
    git merge RAMASECUNDARIA
    ```

- Añadir comentario (o)

- Guardar y salir (:x)

- Ramas fusionadas
    ```
    git branch
    ```

- Borramos rama
    ```
    git branch -d NOMBRERAMA
    ```


**GIT Working flow (local) - Fusiones (gestión conflictos)**

  - Fast-forward (automatizado). No hay conflicto alguno.

    - Nos situamos en la rama que absorberá (principal)
    ```
    git checkout RAMAPRINCIAL
    ```

    - Hacemos el MERGE
    ```
    git merge RAMASECUNDARIA
    ```

    - Añadir comentario (o)

    - Guardar y salir (:x)


  - Manual Merge (Conflicto, dos personas tocaron los mismos archivos)

    - Nos situamos en la rama que absorberá (principal)
    ```
    git checkout RAMAPRINCIAL
    ```

    - Hacemos el MERGE
    ```
    git merge RAMASECUNDARIA
    ```

    - En consola
    ```
    Auto-merging CARPETA/ARCHIVO
    CONFLICT (content): Merge conflict in CARPETA/ARCHIVO
    Automatic merge failed; fix conflicts and then commit the result.
    ```

    - En el editor
    ```
    <<<<<<< HEAD
    hello world....!!!!!!!
    =======
    hello world 2 ..!!!
    >>>>>>> conflictiva
    ```

    - Resuelver y guardar
    ```
    hello world 2 ..!!!
    ```

    - Comprobamos el estado
    ```
    git status
    ```

    - commit para la resolución conflicto
    ```
    git commit -am "con este commit se arregla el conflicto"
    ```

    - Resultado
    ```
    *   81a6c1d con este commit se arregla el conflicto
    |\  
    | * 64b5518 que pasa
    * | 29a6348 ahora conflcito..no
    |/  
    * afe16ae Todo arriba..
    * 7c9cc50 Mi primer Commit
    ```

    - Borramos la rama (opcional)
    ```
    git branch -d NOMBRERAMA
    ```


**GITHUB Working flow (básico)**
  - clone
    - Clonar un proyecto ( [Bootstrap](https://github.com/twbs/bootstrap) )
    ```
    git clone https://github.com/twbs/bootstrap.git
    ```

  - log
    - Mirar los commits
    ```
    git log
    ```    


**GITHUB Working flow (Proyecto desde cero)**

  - Creamos los ficheros

  - init
    - monitorizamos los ficheros
    ```
    git init
    ```

  - commit
    - Añadimos los ficheros en un commit
    ```
    git commit -am "Mi primer proyecto"
    ```

  - remote
    - Enlazamos con Github
    ```
    git remote add origin <--HTTPoSSH-->
    ```

    - Comprobamos los detalles
    ```
    git remote -v
    ```

  - push
    - Mandamos los cambios
    ```
    git push origin master
    ```

**GITHUB Working flow (Proyecto en equipo)**
El proceso es igual, pero es necesario mantenerse sincronizado.

  - fetch
    - Actualizar *origin/master* (rama espejo en local)
    ```
    git fetch origin
    ```

  - merge
    - Fusionar *master* con *origin/master*
    ```
    git merge origin/master
    ```

  - commit
    - Preparamos un *commit* para subir un cambio a Github
    ```
    git commit -am "Nuevo cambio"
    ```

  - push
    - Subimos los cambios
    ```
    git push origin master
    ```


**GITHUB Working flow (Proyectos de terceros)**
*Usamos 2 repositorios (ORIGINAL EXTERNO (upstream/master) -> CLON ORIGINAL (origin/master) -> CLON LOCAL)*

  - remote
    - Conectamos al fork (origin)
    ```
    git remote add origin <--- HTTP --->
    ```

    - Verificamos la conexión
    ```
    git remote -v
    ```

    - Conectamos al remoto *(Upstream)*
    ```
    git remote add upstream HTTTPREPO-UPS
    ```

    - Verificamos que tenemos dos enlaces *(origin y upstream)*
    ```
    git remote -v
    ```

  - fetch
    - Comprobamos cambios en *origin*
    ```
    git fetch origin
    ```

    - Comprobamos cambios con *upstream*
    ```
    git fetch upstream
    ```

  - merge
    - Fusionamos *upstream* con local para actualizarnos
    ```
    git merge upstream/master
    ```

  - push
    - Subimos cambios a *origin*
    ```
    git push origin master
    ```

  - Subimos cambios al *upstream (pull-request)*



**GITHUB Working flow (GitHub Pages Manual)**
GitHub Pages nos permite hacer una web estática para nuestro usuario o proyectos

  - clone
    - Clonamos el repositorio
    ```
    git rclone <-- URL.git -->
    ```

  - checkout --orphan
    - Creamos una rama huérfana
    ```
    git checkout --orphan gh-pages
    ```

  - rm
    - Borramos todos los archivos del directorio
    ```
    git rm --rf .
    ```

  - add
    - Creamos nuestro index.html y lo añadimos
    ```
    echo "Bienvenido a gh-pages" > index.html
    git add index.html
    ```

  - commit
    - Preparamos un commit para subir el index a Github
    ```
    git commit -am "Nuevo cambio"
    ```

  - push
    - Subimos el cambio
    ```
    git push origin gh-pages
    ```


**GITHUB Avanzado (Trucos)**


  - branch
    - Renombrar rama
    ```
    git branch -m NOMBRERAMA NOMBRERAMANUEVO
    ```

    - Mostrando todas las ramas (incluido espejos)
    ```
    git branch -a
    ```

  - add + commit
    - am
    ```
    git commit -am "Texto"
    ```

  - config
    - Usando un alias
    ```
    git config --global alias.NOMBREALIAS 'COMANDO'
    git config --global alias.buenlog 'log --oneline --graph --all'
    git buenlog
    ```

  - pull
    - fecht + merge
    ```
    git pull
    ```

  - diff
    - Ver lo que has modificado pero aún no has preparado
    ```
    git diff
    ```

    - Ver los cambios que has preparado y que irán en tu próxima confirmación
    ```
    git diff --cached
    ```

**Resumen**
![Trabajar con Git/Github](http://www.geekgumbo.com/wp-content/uploads/2011/08/nvie-git-workflow-commands.png)
[tamaño original](http://www.geekgumbo.com/wp-content/uploads/2011/08/nvie-git-workflow-commands.png)


### Reintroducción a JS

**Modo Estricto**
> El modo estricto hace varios cambios en la semántica normal de JavaScript. Primero, modo estricto elimina algunos errores silenciosos de JavaScript cambiando a que lance los errores. Segundo, modo estricto corrige errores que hacen que sea difícil para los motores de JavaScript para realizar optimizaciones: código de modo estricto a veces se puede hacer para correr más rápido que el código idéntico que no es estricto. Tercero, el modo estricto prohíbe sintaxis que es probable que sea definida en futuras versiones de ECMAScript.
> - [Mozilla](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Modo_estricto)


En resumen:
- Detectaremos más errores
- Mejora la interpretación, lo que aumenta la velocidad de ejecucción.
- Previene que usemos sintaxis de futuras versiones de ECMAScript.

Aplicándolo a todo nuestro código

```javascript
// ./script.js
(function() {
  "use strict";

  // Nuestro código

})();
```

Aplicándolo solo en parte del código
```javascript
// ./script.js
function estricta(){
  'use strict';
  function anidada() {
      return "Yo también!";
  }
  return "Hola! Soy una función en modo estricto!  " + anidada();
}

function noEstricta() {
    return "yo no soy una función estricta.";
}
```

Algunos ejemplos:

- Error: Usar variables u objetos sin declararlos antes.

```javascript
    function estricto(){
        'use strict';
        pi = 3.14;
        console.log(pi);
    }
```

- Error: Borrar variables, objetos o funciones. 

```javascript
    function estricto(){
        'use strict';
        pi = 3.14;
        delete pi
    }
```

- Error: Duplicar parámetros

```javascript
    function estricto(){
        'use strict';
        function x (p1, p1){
            // código
        }
    }
```

- Error: Al usar carácteres escapados
 
```javascript
    function estricto(){
        'use strict';
        var x = \010; 
    }
```

Error: Al usar *writable:false*

```javascript
    function estricto(){
        'use strict';
        var obj = {};
        Object.defineProperty(obj, "x", {value:0, writable:false});
        obj.x = 3.14;
    }
```

Error: Al usar *with* 

```javascript
    function estricto(){
        'use strict';
        with (Math){x = cos(2)};
    }
```

Error: Al usar *eval()* por seguridad

```javascript
    function estricto(){
        'use strict';
        eval ("var x = 2");
        console.log(x);
    }
```



Otras palabras reservadas en modo estricto:
- implements
- interface
- let
- package
- private
- protected
- public
- static
- yield


**Variables**

- No se pueden usar espacios
```javascript
var con espacios = 1;
```

- No usar un número delante
```javascript
var 1numero = 1;
```

- Válidos, pero no recomendado
```javascript
var con_guiones_bajos = 1;
var dame$ = 1;
```

- Válidos, es mejor usar [camelCase](https://es.wikipedia.org/wiki/CamelCase)
```javascript
var otraOpcion = 1;
var opcionCon123123 = 1;
```


**Tipos de variables**

Operador *typeof* y su [especificación](http://www.ecma-international.org/ecma-262/5.1/#sec-11.4.3)

- [x] Undefined
```javascript
typeof undefined
typeof noDefinido
typeof tampocoCreado
```

- [x] Object
```javascript
typeof null
typeof [15, 4]
typeof new Date()
typeof {a:1}
```

- [x] Boolean
```javascript
typeof false
typeof true
typeof Boolean(false)
```

- [x] Number
```javascript
typeof 3
typeof 3.14
typeof NaN
typeof Infinity
```

- [x] String
```javascript
typeof "hola"
```

- [x] Function
```javascript
typeof function(){}
typeof class C {}
```

- [x] Symbol (ECMA6)

> Ahora tenemos los símbolos, nuevo tipo de datos que sirve como identificador único para atributos de objetos
> [EcmaScript 6: Símbolos](http://miguelsr.js.org/2015/08/20/es6-symbols.html) de [Miguel Sánchez](http://miguelsr.js.org/about/)

```javascript
typeof Symbol()
typeof Symbol('simbolo')
```


**Matemáticas Básicas**
```javascript
var suma = 5 + 4;
var resta = 10 - 6;
var multiplicacion = 3 * 3;
var division = 6 / 2;
var modulo = 43 % 10;

function calcular (operacion) {
    console.log(operacion);
};
```

**Matemáticas Básicas (Agrupando operaciones)**
```javascript
var expresion1 = (3 + 7) * 10;
var expresion2 = (-56 * 6) - 74 * -25;
var expresion3 = (3 * 3) + 10 - 12 / 2;
var expresion4 = 44 + (83 % (33 + 100));
var expresion5 = -145 + (500 / 10 - 5) + 10 * 10 ;

function calcular (operacion) {
    console.log(operacion);
};
```


**While**

- Estructura:
    ```javascript
    /*  --while--
    while (-algo verdadero-) {
        -ejecutamos este dódigo-
    };
    */
    ```

- Documentación:
    - [While en w3schools](http://www.w3schools.com/js/js_loop_while.asp)
    - [While en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while)

- Bucle infinito:
    Este es un error muy común.

    ```javascript
    while (true) {
        console.log("Este texto se imprime hasta el infinito...");
    };
    ```

- Bucle que no se ejecutará:
    ```javascript
    while (false) {
        console.log("Este texto jamas se imprimirá...");
    };
    ```

- Ejemplo:
    ```javascript
    var control = 1;
    while (control <= 10) {
        console.log(control);
        control++;
    };
    ```


**For**

- Estructura:
    ```javascript
    /*  --for--
    for (-inicializando-; -algo verdadero-; -ejecutar al terminar cada bucle-) {
        -ejecutamos este código-
    };
    */
    ```

- Documentación:
    - [For en w3schools](http://www.w3schools.com/js/js_loop_for.asp)
    - [For en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)
    - [Dominando el rendimiento](https://web.archive.org/web/20141205235948/https://blogs.oracle.com/greimer/entry/best_way_to_code_a)


- Ejemplo:
    ```javascript
    for (var i = 0; i < 10; i++) {
        console.log(i);
    }
    ```


**Do... While**

- Estructura:
    ```javascript
    /* --Do...while--
    do{
       -Ejecutamos este código-
    } while (-Algo verdadero-);
    */
    ```

- Documentación:
    - [Do... While en w3schools](http://www.w3schools.com/js/js_loop_while.asp)
    - [Do... While en MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/do...while)

- Ejemplo:
    ```javascript
    var i = 0;
    do {
       i++;
       console.log(i);
   } while (i < 10);
    ```

- Al menos se ejecutará una vez, aunque la premisa no sea verdadera.

    ```javascript
    do{
       console.warn("me ejecuto")
    } while (false);
    ```


**Ejercicios**
> Vamos a crear un sistema de control para el metro. Nuestro objetivo será desarrollar una aplicación para gestionarlo todo. Con este ejercicio nos centraremos en aplicar conceptos básicos de JavaScript

![Foto de trenes](http://estaticos04.elmundo.es/elmundo/imagenes/2010/06/29/1277838432_0.jpg)

1 - Quiero saber del total de trenes cuantos hay operativos.
    El formato de la respuesta es *"x de x funcionando hoy"*.

```javascript
    var trenesOperativos = 8;
    var totalTrenes = 12;
    var estadoOperacional = " trenes funcionando hoy."

    function estadoVia () {
    	console.log(trenesOperativos+ " de "+totalTrenes+estadoOperacional);
    };
```

- Respuesta esperada (consola):

```
    8 de 12 trenes funcionando hoy.
```


2 - Imprimimos por consola el estado de cada tren en movimiento de manera individualizada (sin bucles).

```javascript
    console.log("El tren numero "+1+" esta funcionando");
    console.log("El tren numero "+2+" esta funcionando");
    console.log("El tren numero "+3+" esta funcionando");
    console.log("El tren numero "+4+" esta funcionando");
    console.log("El tren numero "+5+" esta funcionando");
    console.log("El tren numero "+6+" esta funcionando");
    console.log("El tren numero "+7+" esta funcionando");
    console.log("El tren numero "+8+" esta funcionando");
```

- Respuesta esperada (consola):

```
    El tren numero 1 esta funcionando
    El tren numero 2 esta funcionando
    El tren numero 3 esta funcionando
    El tren numero 4 esta funcionando
    El tren numero 5 esta funcionando
    El tren numero 6 esta funcionando
    El tren numero 7 esta funcionando
    El tren numero 8 esta funcionando
```


3 - Refactoriza... usando *while*.

```javascript
    var trenesOperativos = 8;
    var numeroTren = 1; // Primer tren funcionando

    function estadoDetalle () {
    	while (numeroTren <= trenesOperativos) {
    		console.log("El tren número "+numeroTren+" esta funcionando");
    		numeroTren++;
    	};
    };
```


4 - Refactoriza.. usando *Do... While*.

```javascript
   var trenesOperativos = 8;

    function estadoDetalle () {
        var numeroTren = 1
        do {
            console.log("El tren numero "+numeroTren+" esta funcionando");
            numeroTren++
        } while (numeroTren <= trenesOperativos);
    };
```


5 - Refactoriza.. usando *for*.

```javascript
        var trenesOperativos = 8;

    function estadoDetalle () {
    	for (var numeroTren = 1; numeroTren <= trenesOperativos; numeroTren++) {
    		console.log("El tren numero "+numeroTren+" esta funcionando");
    	};
    };
```


**Trabajando con números**

- NaN:
    ```javascript
    console.log(0/0);
    ```

- Infinity:
    ```javascript
    console.log(100/0);
    ```

- .toFixed() limitar decimales:
    ```javascript
    var numero = 1.3453456467;
    console.log(numero.toFixed(3));
    ```


**Comparadores**

```javascript
var mayorQue = 100 > 10;
var menorQue = 10 < 100;
var mayorIgual = 100 >= 10;
var menorIgual = 10 <= 100;
var igual = 10 == 10;
var igualTotalmente = 10 === 10;
var noIgual = 100 != 10;

function comparar (dato) {
    console.log(dato);
};
```


**Cadenas**

```javascript
var yoVeo = "Yo soy de las personas que ven";
var vasoLleno = "vaso medio lleno";
var vasoVacio = "vaso medio vacío";
```

- Concatenando (Uniendo Cadenas):
    ```javascript
    var frasePositiva = yoVeo + " el " + vasoLleno;
    var fraseNegativa = yoVeo + " el " + vasoVacio;

    function imprimir ( texto) {
        console.log( texto );
    };
    ```

- Imprimir con estilo por consola:
    ```javascript
    function imprimirBonito (texto) {
        console.log (guiones);
        console.log (texto);
        console.log (iguales);
    };

    var guiones = "---------------------"
    var iguales = "====================="
    ```

- Caracteres especiales:
    ```javascript
    /*
    \t -> Tabulador
    \' -> Comillas Simples
    \" -> Comillas Dobles
    \\ -> \
    \n -> Salto de línea
    */

    function caracteresDemo () {
    console.log("Hasta aquí... todo correcto. Ahora vamos a \"tabular\":\tves? Ya estamos más lejos.\n\'Otra linea ;-)\'")
    };
    ```


**Consola**

- Niveles:
Nota: la mayoría de consolas nos permitiran el filtrado por tipo.
    - .log:
    ```javascript
        console.log("Hola en formato clásico");
    ```
    
    - .info:
    ```javascript
        console.info("Hola en formato informativo");
    ```
    
    - .warn:
    ```javascript
        console.warn("Hola en formato alerta");
    ```

    - .error:
    ```javascript
        console.error("Hola en formato error");
    ```
    
    - .debug:
    ```javascript
        console.debug("Hola en formato debug");
    ```

- Formateadores:
    - *%o* para estrcuturas del DOM
    ```javascript
        var parrafos = document.getElementsByTagName("p");
        console.log("DOM: %o", parrafos);
    ```
    
    - *%O* para objectos JS
    ```javascript    
        var objeto = {"nombre":"Yo","Apellido":"Mismo"};
        console.log("DOM: %O", objeto);
    ```

- Agrupación:

```javascript
    console.group("bucleFor");
    for(var i=100; i>0; i--){
        console.info("Iteración numero %i", i)
    }
    console.groupEnd();
```


**Manejo de cadenas**

- .lenght:
    ```javascript
    var amigo = "un amigo";
    var amigos = "un amigo, dos amigos, tres amigos...";

    function comparadorCadenas (cadena1, cadena2){
        console.log((cadena1.length>cadena2.length)+", "+cadena1+" no es mayor que "+cadena2);
    };
    ```

- .concat():
    ```javascript
    var amigo = "un amigo";
    var amigos = amigo.concat(", dos amigos, tres amigos...");
    ```

- .toLowerCase():
    ```javascript
    var amigo = "UN Amigo";
    var amigos = amigo.toLowerCase().concat(", dos amigos, tres amigos...");
    ```

- .charAt():
    ```javascript
    var amigo = "un amigo";
    var amigos = "un amigo, dos amigos, tres amigos...";
    function dimeCaracter ( variable, numero){
        console.log(variable.charAt(numero));
    };
    ```

- .indexOf():
    ```javascript
    var amigo = "un amigo";
    var amigos = "un amigo, dos amigos, tres amigos...";

    function localizaCaracter ( variable, caracter){
        console.log(variable.indexOf(caracter));
    };
    ```

- .substring(inicio, final):
    ```javascript
    var amigo = "un amigo";
    var amigos = "un amigo, dos amigos, tres amigos...";

    var dosAmigos = amigos.substring(10, 20);
    var tresAmigos = amigos.substring(22);
    ```


**Jugando con variables**

```javascript
var empezoComo3 = 3;
era3();

empezoComo3 = 35;
era3();

empezoComo3 = empezoComo3 + 30;
era3();

empezoComo3 += 4;
era3();

empezoComo3++;
era3();

empezoComo3 -= 12;
era3();

empezoComo3--;
era3();

empezoComo3 *= 10;
era3();

empezoComo3 /= 11;
era3();

empezoComo3 += "texto";
era3();

empezoComo3 += 20;
era3();

empezoComo3++;
era3();


function era3 () {
    console.log("empezoComo3 debería ser 3, ahora su valor es " + empezoComo3);
};
```


**Ejercicios**

6 - Del total de trenes... ¿cuantos tengo parados?

```javascript
    var trenesOperativos = 8;
    var totalTrenes = 12;

    function trenesParados(){
    	for(var numeroTren = trenesOperativos + 1; numeroTren <= totalTrenes; numeroTren++){
    		console.log("El tren numero "+numeroTren+" esta parado");
    	};
    };
```

- Respuesta esperada (consola):

```
    El tren numero 9 esta parado
    El tren numero 10 esta parado
    El tren numero 11 esta parado
    El tren numero 12 esta parado
```


7 - Refactoricemos y juntemos los dos bucles dentro de una misma función. Así se imprime por consola tanto los trenes que estan funcionanado como los que estan parados

```javascript
    var trenesOperativos = 8;
    var totalTrenes = 12;

    function estadoDetalle () {
    	var numeroTren = 1;
    	while (numeroTren <= trenesOperativos) {
    		console.log("El tren numero "+numeroTren+" esta funcionando");
    		numeroTren++;
    	};
    	for(var trenParado = trenesOperativos + 1; trenParado <= totalTrenes; trenParado++) {
    		console.log("El tren numero "+trenParado+" esta parado");
    	};
    };
```

- Respuesta esperada (consola):

```
    El tren numero 1 esta funcionando
    El tren numero 2 esta funcionando
    El tren numero 3 esta funcionando
    El tren numero 4 esta funcionando
    El tren numero 5 esta funcionando
    El tren numero 6 esta funcionando
    El tren numero 7 esta funcionando
    El tren numero 8 esta funcionando
    El tren numero 9 esta parado
    El tren numero 10 esta parado
    El tren numero 11 esta parado
    El tren numero 12 esta parado
```

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

**Atacando la lógica**

- Divide y venceras (determina la estructura de afuera hacia dentro)
    ![Divide et impera](http://orig12.deviantart.net/467f/f/2009/257/9/9/divide_y_venceras___cesar_by_horusart.jpg)

- Los comentarios son tu aliado. 

- [Introduction to Pseudocode de Damian Gordon](http://www.slideshare.net/DamianGordon1/pseudocode-10373156?qid=2ccda58e-4c14-4685-ba31-2b3ae9196e4a&v=qf1&b=&from_search=1)
    ![ejemplo_pseudocodigo](http://rockbotic.com/wp-content/uploads/2014/01/pseudocodigo-para-dormir.jpg)

- [Blocky](https://blockly-demo.appspot.com/static/demos/code/index.html?lang=es)
    - Exportación en PHP, JS, Python, etc...
    - Verificación de la lógica
    - [Opensource](https://github.com/google/blockly)


**Funciones (Avanzadas)**

- Anónimas (expresiones):
    ```javascript
	var sumaCuadrados = function (a, b) {
		return (a*a) + (b*b);
	};
    
    console.log("El .name de sumaCuadrados es "+sumaCuadrados.name)
    ```

- Funciones como dato:
    ```javascript
	function saludo () {
		console.log("hola!");
	};

	function lanzar (funcion){
		funcion();
	};
    ```

- Funciones anónimas autoejecutables:
    ```javascript
	(function() {
		console.log("hola Amigo/a")

	}) (); //ex:Jquery
    ```


- Funciones anónimas con parámetros:
    ```javascript
	( function(quien){
	   console.log("hola " + quien);
	})("Amigo/a");
    ```


- Función que devuelve una función anónima:
	- Asignando una variable:
    ```javascript
	function saludo(quien){
	        return function(){
	                alert("hola " + quien);
	        }
	}
	var saluda = saludo("Amigo/a");
	saluda();
    ```

	- Sin asignar una variable:
    ```javascript
	function saludo(quien){
	        return function(){
	                alert("hola " + quien);
	        }
	}
	saludo("Amigo/a")();
    ```


**Funciones (Anidación)**

- Anidación:
    ```javascript
	function saludar(quien){
	        function alertasaludo(){
	                console.log("hola " +  quien);
	        }
	        return alertasaludo;
	}
	var saluda = saludar("Amigo/a");
	saluda();
    ```

- Anidación:
    ```javascript
	function saludar(quien){
	        function alertasaludo(){
	                console.log("hola " +  quien);
	        }
	        return alertasaludo;
	}
	saludar("Amigo/a")();
    ```
    
**Funciones (recursión)**

- Calcular el [factorial](https://www.wikiwand.com/es/Factorial).
	
    ```javascript
		function factorial(n){
		   if(n <= 1)
		      return 1
		   else
		      return n * factorial(n-1)
		}
		
		factorial(0); // n! = 1
		factorial(1); // n! = 1
		factorial(2); // n! = 2
		factorial(3); // n! = 6 (3*2*1)
		factorial(4); // n! = 24 (4*3*2*1)
		factorial(5); // n! = 120 (5*4*3*2*1)
		factorial(6); // n! = 720 (...)
		// ...
    ```


- Saber si hoy es un día par o impar.

```javascript
	var miDiaEs = function() {
	    if (new Date().getDate() % 2 == 0) {
	        console.info("hoy es un día par");
	    } else {
	        console.info("hoy es un día impar");
	    }
	}
	miDiaEs();
```



**Funciones (Closures)**

> Los closures son funciones que manejan variables independientes. En otras palabras, la función definida en el closure "recuerda" el entorno en el que se ha creado.

> No es aconsejable crear innecesariamente funciones dentro de otras funciones si no se necesitan los closures para una tarea particular ya que afectará negativamente el rendimiento del script tanto en consumo de memoria como en velocidad de procesamiento.
> [Closures MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Closures)

- Fábrica de función:
    ```javascript
	function sumador(x) {
	  return function(y) {
	    return x + y;
	  };
	}

	var sum1 = sumador(10); //Closure
	var sum2 = sumador(30);	//Closure

	console.log(sum1(2)); // Devuelve 12
	console.log(sum2(2)); // Devuelve 32
	console.log(sumador(20)(2)); //Devuelve 22
    ```

- Otro ejemplo, ahora temporizado:
    ```javascript
	function saludar(segundos){
		var hola = "Hola, Hola!";

		setTimeout(function(){
			console.info(hola);
		},segundos*1000);
	}

	saludar(2);
    ```

- Otro ejemplo... más útil:
    ```javascript
      var varGlobal = "Soy un dato Global";
      var burbuja;

      function nivel1() {
        var varInterna = "Soy un dato interno. -> nivel1";

        function nivel2() {
          console.log("Estoy dentro de la funcion -> nivel2")
          console.log("Estoy dentro de la funcion -> nivel2 y puedo acceder al nivel1: "+varInterna)
        }

        burbuja = nivel2;

      }

      nivel1();

      burbuja();
      console.log("Burbuja recuerda su contexto original")
    ```


**Switch**

- Estructura:
    ```javascript
    /* Switch
	switch(expresión) {
	    case n:
	        //Código
	        break;
	    case n:
	        //Código
	        break;
	    default:
	        //Código
	}
    */
    ```

- Documentación:
    - [Switch en w3schools](http://www.w3schools.com/js/js_switch.asp)
    - [Switch en MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Sentencias/switch)

- Casos únicos:
    ```javascript
	var nombre = "";
	switch (nombre) {
	  case "Pepe":
	    console.log("Hola Pepe");
	    break;
	  case "Luis":
	    console.log("Hola Luis");
	    break;
	  case "Antonio":
	    console.log("Hola Antonio");
	    break;
	  default:
	    console.log('Ninguno de los nombres que pensamos... es '+nombre);
	}
    ```

- Multiples coincidencias:
    ```javascript
	var nombre = "";
	switch (nombre)
	{
	   case "Pepe":
	   case "Luis":
	   case "Antonio":
	       alert('Hola '+nombre);
	       break;

	   default:
	       console.log('Ninguno de los nombres que pensamos... es '+nombre);
	}
    ```


**Ejercicios**

13 - Hagamos una lista de pasajeros (min. 6)

```javascript
   	var pasajero1 = "Alicia Gutierrez";
	var pasajero2 = "Alfonso Gomez";
	var pasajero3 = "Luis Navarro";
	var pasajero4 = "Oscar Garcia";
	var pasajero5 = "Andres Fernandez";
	var pasajero6 = "Lucia Mellado";
```


14 - Hagamos una lista de pasajeros efectiva usando Arrays

```javascript
	var pasajeros = ["Alicia Gutierrez", "Alfonso Gomez", "Luis Navarro", "Oscar Garcia", "Andres Fernandez", "Lucia Mellado"];
```


15 - Imprimamos cada pasajero de la lista y su número de asiento (basado en el orden del índice).
*Nota: El primer asiento del tren es el 1 y no el 0.*

```javascript
	var pasajeros = ["Alicia Gutierrez", "Alfonso Gomez", "Luis Navarro", "Oscar Garcia", "Andres Fernandez", "Lucia Mellado"];

	function listaPasajeros(){
		for (var i = 0; i < pasajeros.length; i++) {
			console.log("El pasajero "+pasajeros[i]+" tiene reservado el asiento "+(i+1));
		};
	};
```


16 - Necesitamos una función para agregar y otra para borrar pasajeros de la lista.
*Nota: Pensemos que a la larga pueden existir más listas.*

```javascript
	var pasajeros = ["Alicia Gutierrez", "Alfonso Gomez", "Luis Navarro", "Oscar Garcia", "Andres Fernandez", "Lucia Mellado"];

	function agregarPasajero(nombre, lista) {
		lista.push(nombre);
		return lista
	};

	function quitarPasajero(nombre, lista) {
		if (lista.length == 0) {
			console.log("La lista \""+lista+"\" esta vacía.");
		} else {
			for (var i = 0; i < lista.length; i++) {
				if(lista[i] == nombre){
					lista.splice(i, 1);
					return lista;
				} else if (i == lista.length -1){
					console.log("El pasajero \""+nombre+"\" no encontrado!")
				};
			};
		};
	};
	
	/* Testeamos Funcionalidad
		quitarPasajero("Luis Navarro", pasajeros)
		agregarPasajero("Yo Mismo", pasajeros)
		quitarPasajero("Yo Mismo", pasajeros)
		
	*/
```


17 - La compañía de trenes ha decidido que los viajeros podrán reservar el asiento asignado, pero quiere evitar que los pasajeros cambien de asiento constantemente cuando se anula un o varios billetes.
*Nota: Al borrar en el ejercicio anterior las posiciones de los pasajeros cambiaban y los billetes quedaban desactualizados.*

```javascript
	var pasajeros = ["Alicia Gutierrez", "Alfonso Gomez", "Luis Navarro", "Oscar Garcia", "Andres Fernandez", "Lucia Mellado"];

	function agregarPasajero(nombre, lista) {
		if(lista.length == 0){
			lista.push(nombre);
			console.log("El pasajero "+nombre+" añadido con éxito, asiento asignado 0");
		}else {
			for (var i = 0; i < lista.length; i++) {
				if (lista[i] == undefined) {
					lista[i] = nombre;
					console.log("El pasajero "+nombre+" añadido con éxito, asiento asignado "+(i+1));
					return true
				} else if (i == lista.length -1){
					lista.push(nombre);
					console.log("El pasajero "+nombre+" añadido con éxito, asiento asignado "+(i+1));
					console.log("INFO: En esta lista no quedan asientos pendientes de asignación.")
					return true
				};
			};
		};
	};


	function quitarPasajero(nombre, lista) {
		if (lista.length == 0) {
			console.log("La lista \""+lista+"\" esta vacía.");
			return false
		} else {
			for (var i = 0; i < lista.length; i++) {
				if(lista[i] == nombre){
					lista[i] = undefined;
					console.log("El pasajero \""+nombre+"\" eliminado con éxito!")
					return true;
				} else if (i == lista.length -1){
					console.log("El pasajero \""+nombre+"\" no encontrado!");
					return false
				};
			};
		};
	};
	
		
	/* Testeamos Funcionalidad
	
		quitarPasajero("Luis Navarro", pasajeros)
		agregarPasajero("Yo Mismo", pasajeros)
		quitarPasajero("Yo Mismo", pasajeros)
		
	*/
	
```


18 - Una de las vías principales esta en obras. Así que nuestra compañía decidió usar antiguas vías para hacer transbordos directos entre las estaciones afectadas.

Nuestra Misión es añadir el tiempo estimado en los billetes para las estaciones afectadas Tetuán,
Moncloa y Hortaleza. Es necesario incluir un texto informativo y el nombre del usuario también en el billete.

*Nota: Intenta utilizar lo parendido en clase (funciones avanzadas)*

Info: 	
	- Tetuán (12)
   	- Moncloa (19)
   	- Hortaleza (21)

```javascript
	var nuevasRutas = [ ["Tetuán", 12], ["Moncloa", 19], ["Hortaleza", 21] ];

	function constructorDeTickets (estacion, tiempo) {
		return function (nombre) {
			console.log("Sr/a. "+nombre+".\n Muchas gracias por adquirir este ticket gratuito en el "+estacion+" express.\n El tiempo estimado de llegada es de "+tiempo+" minutos.\n Estamos trabajando en la mejora de nuestra vía principal, disculpe las molestias!");
		};
	}

	var tetuanExpress = constructorDeTickets ("Tetuán", 12);
	var moncloaExpress = constructorDeTickets (nuevasRutas[1][0], nuevasRutas[1][1]);
	var hortalezaExpress = constructorDeTickets (nuevasRutas[2][0], nuevasRutas[2][1]);

	tetuanExpress ("Pepe");
	moncloaExpress ("Luis");
	hortalezaExpress ("Hector");

```


**Funciones (Callbacks)**

> En programación de computadoras, una devolución de llamada o retrollamada (en inglés: callback) es una función "A" que se usa como argumento de otra función "B". Cuando se llama a "B", ésta ejecuta "A". Para conseguirlo, usualmente lo que se pasa a "B" es el puntero a "A".
> [Callbacks en Wikiwand](https://www.wikiwand.com/es/Callback_(inform%C3%A1tica))

- Ejemplo condensado:
    ```javascript
	var quieroCallback = function(parametro, callback){
	    if ((callback) && (typeof callback === 'function')){
	        callback(parametro);
	    }
	    else
	        console.log(parametro, callback);
	}
	 
	quieroCallback('a', 'b');
	 
	quieroCallback('a', function(val){
	    console.log(val);
	});
    ```


- Ejemplo con Jquery:
    ```javascript
    $('#elemento').fadeIn('slow', function() {
    	// código del callback
	});
    ```


- Otro ejemplo:
    ```javascript
    function comerSandwich(elemento1, elemento2, callback) {
	    console.info('ñam ñam... empiezo con el sándwich.\n\nMe gusta porque tiene tiene ' + elemento1 + ', ' + elemento2);
	    callback();
	}

	comerSandwich('jamón', 'queso', function() {
	    console.info('Ya terminé...');
	});
    ```


- Ejemplo con Callback opcional:
    ```javascript
    function comerSandwich(elemento1, elemento2, callback) {
	    console.info('ñam ñam... empiezo con el sándwich.\n\nMe gusta porque tiene tiene ' + elemento1 + ', ' + elemento2);
	    
	    if (callback) {
	        callback();
	    }

	}

	comerSandwich('jamón', 'queso');
    ```


- Sanitizar el Callback:
    ```javascript
    function comerSandwich(elemento1, elemento2, callback) {
	    console.info('ñam ñam... empiezo con el sándwich.\n\nMe gusta porque tiene tiene ' + elemento1 + ', ' + elemento2);
	    
	    if (callback && typeof(callback) === "function") {
	        callback();
	    }

	}

	comerSandwich('jamón', 'queso');
    ```


- Asincronia:
    ```javascript
    function comerSandwich(elemento1, elemento2, callback) {
	    console.info('ñam ñam... empiezo con el sándwich.\n\nMe gusta porque tiene tiene ' + elemento1 + ', ' + elemento2);
	  
		setTimeout(alarma, 5000);
		function alarma(){
			console.log("ring! ring!.. pasaron los 5 segundos!");
		};

	  
	    if (callback && typeof(callback) === "function") {
	        callback();
	    }
	}

	comerSandwich('jamón', 'queso', function() { 
	    console.log('Ya terminé...');
	});
    ```


- Más información: 
	- [Callback Functions in JavaScript de Louis Lazaris](http://www.impressivewebs.com/callback-functions-javascript/)
	- [Creando y utilizando callbacks de Pablo Novas en fernetjs](https://fernetjs.com/2011/12/creando-y-utilizando-callbacks/)



**Ejercicios**

19 - Necesitamos saber cuantos pasajeros están utilizando cada una de estas rutas temporales, para ellos la empresa decide añadir un numero de billete para cada pasajero.  El número de billete tiene que seguir una estructura fija.

*Nota: El formato del número de billete deseado:
- (Inicial de la estación)(número de viajero) -> H1 (Hortaleza 1), T120 (Tetuan 120), M110 (Moncloa 110), etc...*

```javascript
	var nuevasRutas = [ ["Tetuán", 12], ["Moncloa", 19], ["Hortaleza", 21] ];

	function constructorDeTickets (estacion, tiempo) {
		var numeroPasajero = 0;
		return function (nombre) {
			numeroPasajero++;
			console.log("Sr/a. "+nombre+".\n Muchas gracias por adquirir este ticket gratuito en el "+estacion+" express.\n Billete Número:\t"+(estacion.charAt(0)+numeroPasajero)+"\n El tiempo estimado de llegada es de "+tiempo+" minutos.\n  Estamos trabajando en la mejora de nuestra vía principal, disculpe las molestias!");
		};
	}

	var tetuanExpress = constructorDeTickets ("Tetuán", 12);
	var moncloaExpress = constructorDeTickets (nuevasRutas[1][0], nuevasRutas[1][1]);
	var hortalezaExpress = constructorDeTickets (nuevasRutas[2][0], nuevasRutas[2][1]);
	
	
	tetuanExpress ("Pepe");
	moncloaExpress ("Luis");
	hortalezaExpress ("Hector");

```


20 - Gracias al ejercicio anterior, hemos podido saber a groso modo cuantos pasajeros van en cada línea.

La empresa considera que con estos datos, usará trenes con menos vagones que le permitirán transportar a los pasajeros en menos tiempo.

Pero existe el riesgo de dejar pasajeros esperando mucho tiempo.

Así que haremos una nueva función que avise al revisor cuando no quede sitio en el próximo tren.

El revisor del tren debe repartir tickets restaurante a los pasajeros para que puedan tomar una consumición gratis en la cafetería de la estación, si no tienen sitio en el próximo tren.

*Nota: La linea es única y el mismo tren cubre todo el trayecto.*

```javascript
	function capacidad (ultimoPasajero, numeroMaximo) {

		function sinSitios () {
			console.log("IMPORTANTE: No queda sitio, por favor... saca los tickets restaurante!")
			console.log ("Capacidad:\t"+ultimoPasajero+"/"+numeroMaximo);
		};
		function quedaSitio () {
			console.log ("Capacidad:\t"+ultimoPasajero+"/"+numeroMaximo);
		};

		if (ultimoPasajero >= numeroMaximo){
			sinSitios();
		} else {
			quedaSitio();
		};

	};
	
	capacidad(10, 50);
	capacidad(50, 50);
	capacidad(55, 50);
```


**Objetos Literales**

- Propiedades:
    ```javascript
	var miObjeto = {
	    cadena: 'esto es una cadena',
	    numero: 2,
	    booleano: false
	};
	```


- Métodos:
    ```javascript
	var miObjeto = {
	    saludar: function(){
			console.log("hola!");
		}
	};
	```
	
- Trabajando con espacios y caracteres especiales:
    ```javascript
	var miObjeto = {
		nombre: "objeto",
	    "año": 2015,
	    "estado del sistema": "correcto"
	};
	
	console.log(miObjeto["año"]);
	miObjeto["estado del sistema"] = "fuera de servicio";
	console.log(miObjeto["estado del sistema"]);
	```

- Acortar objetos:

    ```javascript
	var objetoAbreviado = objeto.muy.muy.largo.que.tiene.muchos["metodos y propiedades"];
	
	objetoAbreviado.propiedad1;
	objetoAbreviado.metodo1();

	```


**Ejercicios Repaso - Cajero Automático**
![cajero automatico](http://rack.1.mshcdn.com/media/ZgkyMDE0LzAyLzI2L2YwL0JpdGNvaW5fQVRNLmJjN2IxLmpwZwpwCXRodW1iCTEyMDB4NjI3IwplCWpwZw/bdee5162/0fe/Bitcoin_ATM.jpg)

1 - Definimos el objeto

```javascript
	var cajeroAutomatico = {};
```

2 - Añadimos detalles básicos(clientes y propiedades)

```javascript
	var clientesBD = ["Alicia Gutierrez", "Alfonso Gomez", "Luis Navarro", "Oscar Garcia", "Andres Fernandez", "Lucia Mellado"];

	var cajeroAutomatico = {
	    empresaPropietaria: "SuperExpress",
	    modelo: "Al-201",
	    año: 2010,
	    serie: "01 Beta",
	    tipo: "Prototipo",
	    unidadMedida: "metros",
	    alto: 1,
	    ancho: 0.5,
	    largo: 0.5,
	    unidadPeso: "Kg",
	    peso: 600,
	    materiales: ["acero", "plástico", "cables", "circuitos"],
	    clientesAutorizados: clientesBD,
	    moneda: "Euros",
	    dineroDisponible: 65000
	};
```


3 - Añadimos detalles adicionales (volumen)

```javascript
	cajeroAutomatico.volumen = cajeroAutomatico.alto * cajeroAutomatico.ancho * cajeroAutomatico.largo;
	cajeroAutomatico.volumenMedida = cajeroAutomatico.unidadMedida.charAt(0) +3;

	console.log("El volumen del cajero automático es de "+cajeroAutomatico.volumen+cajeroAutomatico.volumenMedida);
```


4 - Añadimos funciones para quitar y añadir clientes

```javascript
	function agregarCliente (nombre, lista) {
	lista.push(nombre);
	return lista;
	}

	function quitarCliente(nombre, lista) {
		if (lista.length === 0) {
			console.log("La lista esta vacía.");
		} else {
			for (var i = 0; i < lista.length; i++) {
				if(lista[i] == nombre){
					lista.splice(i, 1);
					console.log("El Cliente \""+nombre+"\" eliminado con éxito!");
					return lista;
				} else if (i == lista.length -1){
					console.log("El cliente \""+nombre+"\" no encontrado!");
				}
			}
		}
	}
	
	/* Testeamos Funcionalidad

	agregarCliente ("yo mismo", clientesBD)
	quitarCliente ("yo mismo", clientesBD)
	quitarCliente ("yo mismo", clientesBD)

	
	*/
	
```


5 - Añadimos una propiedad para contabilizar las operaciones realizadas

```javascript
	cajeroAutomatico["operaciones realizadas"] = 0;
	console.info("Por el momento las operaciones realizadas son "+cajeroAutomatico["operaciones realizadas"]);
```


6 - Creamos una función para eliminar una propiedad si no contiene cierta cantidad de datos.
*Nota: borrandoDatosVacios (objeto, propiedad, valorMinimo)*

```javascript
	function borrandoDatosVacios (objeto, propiedad, valorMinimo) {
	    if (objeto[propiedad] <= valorMinimo) {
	        delete objeto[propiedad]
	        return true
	    } else {
	        return false
	    }
	}
	
	/* Testeamos Funcionalidad

	borrandoDatosVacios(cajeroAutomatico, "operaciones realizadas", 0);
	
	*/
```


7 - Añadimos funciones de control de operaciones (contabilizar operaciones realizadas y fallidas) y funciones de administracción (agregar y quitar dinero)

```javascript
	var debugMode = true;

	function esNumero(n) {
	  return !isNaN(parseFloat(n)) && isFinite(n);
	}

	function operacionRealizada () {
	    if (isNaN(cajeroAutomatico["operaciones realizadas"]) || cajeroAutomatico["operaciones realizadas"] === undefined) {
	        cajeroAutomatico["operaciones realizadas"] = 1;
	        if(debugMode){
	            console.info("Primera operación realizada con éxito!");
	        }
	    } else {
	        cajeroAutomatico["operaciones realizadas"]++;
	        if(debugMode){
	            console.info("La operación #"+cajeroAutomatico["operaciones realizadas"]+" realizada con éxito!");
	        }        
	    }  
	};

	function operacionFallida () {
	    if (isNaN(cajeroAutomatico["operaciones fallidas"]) || cajeroAutomatico["operaciones fallidas"] === undefined) {
	        cajeroAutomatico["operaciones fallidas"] = 1;
	        if(debugMode){
	            console.warn("ERROR: Primera operación fallida!");
	        }
	    } else {
	        cajeroAutomatico["operaciones fallidas"]++;
	        if(debugMode){
	            console.warn("ERROR: La operación #"+cajeroAutomatico["operaciones fallidas"]+" fallo!");
	        }        
	    }  
	};


	function agregarDinero (cantidad){
	    if (esNumero(cantidad)) {
	        cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible + cantidad;
	        operacionRealizada();
	        if(debugMode){
	            console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
	        }
	    } else {
	        operacionFallida();
	        if(debugMode){
	            console.warn(cantidad+" No es un numero valido!");
	        }
	    }

	}

	function quitarDinero (cantidad){
	    if (esNumero(cantidad)) {
	        cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible - cantidad;
	        operacionRealizada();
	        if(debugMode){
	            console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
	        }
	    } else {
	        operacionFallida();
	        if(debugMode){
	            console.warn(cantidad+" No es un numero valido!");
	        }
	    }
	}

	/* Testeamos Funcionalidad
	
	quitarDinero (1000)
	quitarDinero ("Mucho!!")
	agregarDinero (1000000)
	agregarDinero ("Poco!")
	
	*/
```


8 - Añadimos funciones para operaciones económicas y verificación de los clientes

```javascript
function retirarEfectivo (nombre, cantidad) {
    if (esCliente(nombre)){
        if (esNumero(cantidad)) {
            cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible - cantidad;
            operacionRealizada();
            if(debugMode){
                console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
            }
        } else {
            operacionFallida();
            if(debugMode){
                console.warn(cantidad+" No es un numero valido!");
            }
        }
    } else {
            operacionFallida();
            if(debugMode){
                console.warn(nombre+" No eres un cliente de "+cajeroAutomatico.empresaPropietaria+"!");
            }        
    }    

}

function ingresarEfectivo (nombre, cantidad) {
    if (esCliente(nombre)){
        if (esNumero(cantidad)) {
            cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible + cantidad;
            operacionRealizada();
            if(debugMode){
                console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
            }
        } else {
            operacionFallida();
            if(debugMode){
                console.warn(cantidad+" No es un numero valido!");
            }
        }
    } else {
            operacionFallida();
            if(debugMode){
                console.warn(nombre+" No eres un cliente de "+cajeroAutomatico.empresaPropietaria+"!");
            }        
    }    

}


function esCliente(nombre) {
	if (cajeroAutomatico.clientesAutorizados === 0) {
	    if (debugMode) {
		    console.warn("La lista esta vacía.");
	    }
	    return false;
	} else {
		for (var i = 0; i < cajeroAutomatico.clientesAutorizados.length; i++) {
			if(cajeroAutomatico.clientesAutorizados[i] == nombre){
				if (debugMode) {
		            console.info(nombre+" eres cliente de "+cajeroAutomatico.empresaPropietaria);
				}
				return true;
			} else if (i == cajeroAutomatico.clientesAutorizados.length -1){
				if (debugMode) {
		            console.warn(nombre+" no encontrado!");
				}
				return false;
			}
		}
	}
}

/* Testeamos Funcionalidad

	ingresarEfectivo ("Yo mismo", 1000);
	ingresarEfectivo ("Oscar Garcia", "Poco!");
	ingresarEfectivo ("Oscar Garcia", 10);
	retirarEfectivo("Yo mismo", 1000);
	retirarEfectivo ("Oscar Garcia", "Muchoo!");
	retirarEfectivo ("Oscar Garcia", 10000);
	
*/
```


9 - Creamos un log detallado y una cuenta total

```javascript
	'use strict';
	/* VARIABLES */
	var debugMode = true;

	var clientesBD = ["Alicia Gutierrez", "Alfonso Gomez", "Luis Navarro", "Oscar Garcia", "Andres Fernandez", "Lucia Mellado"];

	var cajeroAutomatico = {
	    empresaPropietaria: "SuperExpress",
	    modelo: "Al-201",
	    año: 2010,
	    serie: "01 Beta",
	    tipo: "Prototipo",
	    unidadMedida: "metros",
	    alto: 1,
	    ancho: 0.5,
	    largo: 0.5,
	    unidadPeso: "Kg",
	    peso: 600,
	    materiales: ["acero", "plástico", "cables", "circuitos"],
	    clientesAutorizados: clientesBD,
	    moneda: "Euros",
	    dineroDisponible: 65000
	};

	cajeroAutomatico.volumen = cajeroAutomatico.alto * cajeroAutomatico.ancho * cajeroAutomatico.largo;
	cajeroAutomatico.volumenMedida = cajeroAutomatico.unidadMedida.charAt(0) +3;

	/* FUNCIONES VERIFICACIÓN */

	/**
	 * Añade información sobre todo lo que ocurre en cajeroAutomatico.log.(logNUMERO).
	 * Actualiza cajeroAutomatico.logTotal con operaciones fallidas y operaciones realizadas.
	 * @param {string} tipo - "info" o "error".
	 * @param {string} origen - "usuario", "maquina" o "administrador".
	 * @param {string} codigo - código de error
	 * @param {string} detalles - Descripción del error.
	 */
	function dataLog (tipo, origen, codigo, detalles) {
	    cajeroAutomatico["operaciones fallidas"] = cajeroAutomatico["operaciones fallidas"] || 0;
	    cajeroAutomatico["operaciones realizadas"] = cajeroAutomatico["operaciones realizadas"] || 0;
	    cajeroAutomatico.logTotal = cajeroAutomatico.logTotal || 1;
	    cajeroAutomatico.log = cajeroAutomatico.log || [];
	    cajeroAutomatico.logTotal = cajeroAutomatico["operaciones fallidas"] + cajeroAutomatico["operaciones realizadas"];
	    cajeroAutomatico.log[cajeroAutomatico.logTotal] = [cajeroAutomatico.logTotal, tipo, origen, codigo, detalles ]

	}


	function esCliente(nombre) {
		if (cajeroAutomatico.clientesAutorizados === 0) {
		    if (debugMode) {
			    console.warn("La lista esta vacía.");
		    }
		    return false;
		} else {
			for (var i = 0; i < cajeroAutomatico.clientesAutorizados.length; i++) {
				if(cajeroAutomatico.clientesAutorizados[i] == nombre){
					if (debugMode) {
			            console.info(nombre+" eres cliente de "+cajeroAutomatico.empresaPropietaria);
					}
					return true;
				} else if (i == cajeroAutomatico.clientesAutorizados.length -1){
					if (debugMode) {
			            console.warn(nombre+" no encontrado!");
					}
					return false;
				}
			}
		}
	}

	function esNumero(n) {
	  return !isNaN(parseFloat(n)) && isFinite(n);
	}

	function operacionRealizada () {
	    if (isNaN(cajeroAutomatico["operaciones realizadas"]) || cajeroAutomatico["operaciones realizadas"] === undefined) {
	        cajeroAutomatico["operaciones realizadas"] = 1;
	        if(debugMode){
	            console.info("Primera operación realizada con éxito!");
	        }
	    } else {
	        cajeroAutomatico["operaciones realizadas"]++;
	        if(debugMode){
	            console.info("La operación #"+cajeroAutomatico["operaciones realizadas"]+" realizada con éxito!");
	        }        
	    }  
	}

	function operacionFallida () {
	    if (isNaN(cajeroAutomatico["operaciones fallidas"]) || cajeroAutomatico["operaciones fallidas"] === undefined) {
	        cajeroAutomatico["operaciones fallidas"] = 1;
	        if(debugMode){
	            console.warn("ERROR: Primera operación fallida!");
	        }
	    } else {
	        cajeroAutomatico["operaciones fallidas"]++;
	        if(debugMode){
	            console.warn("ERROR: La operación #"+cajeroAutomatico["operaciones fallidas"]+" fallo!");
	        }        
	    }  
	}

	function borrandoDatosVacios (objeto, propiedad, valorMinimo) {
	    if (objeto[propiedad] <= valorMinimo) {
	        delete objeto[propiedad];
	        return true;
	    } else {
	        return false;
	    }
	}


	/* FUNCIONES INTERACCIÓN */

	function retirarEfectivo (nombre, cantidad) {
	    if (esCliente(nombre)){
	        if (esNumero(cantidad)) {
	            cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible - cantidad;
	            operacionRealizada();
	            dataLog ("info", "usuario", 1, "Retirada de "+cantidad+cajeroAutomatico.moneda+" por "+nombre);
	            if(debugMode){
	                console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
	            }
	            return true;
	        } else {
	            operacionFallida();
	            dataLog ("error", "usuario", 2, "Retirada fallida por "+cantidad+" errónea. Usuario: "+nombre);
	            if(debugMode){
	                console.warn(cantidad+" No es un numero valido!");
	            }
	            return false;
	        }
	    } else {
	            operacionFallida();
	            dataLog ("error", "usuario", 3, nombre+" No es cliente");
	            if(debugMode){
	                console.warn(nombre+" No eres un cliente de "+cajeroAutomatico.empresaPropietaria+"!");
	            }
	            return false;
	    }    

	}

	function ingresarEfectivo (nombre, cantidad) {
	    if (esCliente(nombre)){
	        if (esNumero(cantidad)) {
	            cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible + cantidad;
	            operacionRealizada();
	            dataLog ("info", "usuario", 4, "Ingreso de "+cantidad+cajeroAutomatico.moneda+" por "+nombre);
	            if(debugMode){
	                console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
	            }
	            return true;
	        } else {
	            operacionFallida();
	            dataLog ("error", "usuario", 5, "Ingreso fallido por "+cantidad+" - errónea. Usuario: "+nombre);
	            if(debugMode){
	                console.warn(cantidad+" No es un numero valido!");
	            }
	            return false;
	        }
	    } else {
	            operacionFallida();
	            dataLog ("error", "usuario", 6, nombre+" No es cliente");
	            if(debugMode){
	                console.warn(nombre+" No eres un cliente de "+cajeroAutomatico.empresaPropietaria+"!");
	            }
	            return false;
	    }    

	}

	function agregarDinero (cantidad){
	    if (esNumero(cantidad)) {
	        cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible + cantidad;
	        operacionRealizada();
	        dataLog ("info", "administrador", 7, "Ingreso de "+cantidad+cajeroAutomatico.moneda);
	        if(debugMode){
	            console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
	        }
	        return true;
	    } else {
	        operacionFallida();
	        dataLog ("error", "administrador", 8, "Ingreso fallido por "+cantidad+" - errónea.");
	        if(debugMode){
	            console.warn(cantidad+" No es un numero valido!");
	        }
	        return false;
	    }

	}

	function quitarDinero (cantidad){
	    if (esNumero(cantidad)) {
	        cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible - cantidad;
	        operacionRealizada();
	        dataLog ("info", "administrador", 9, "Retirada de "+cantidad+cajeroAutomatico.moneda);
	        if(debugMode){
	            console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
	        }
	        return true;
	    } else {
	        operacionFallida();
	        dataLog ("error", "administrador", 10, "Retirada fallida por "+cantidad+" - errónea.");
	        if(debugMode){
	            console.warn(cantidad+" No es un numero valido!");
	        }
	        return false;
	    }
	}

	function agregarCliente (nombre, lista) {
	    lista.push(nombre);
	    operacionRealizada();
	    dataLog ("info", "administrador", 11, "Ingreso de "+nombre+" a la base de datos de clientes");
	    return true;
	}

	function quitarCliente(nombre, lista) {
		if (lista.length === 0) {
		    if (debugMode) {
			    console.log("La lista esta vacía.");
		    }
			operacionFallida();
			dataLog ("error", "maquina", 12, "Eliminacion de "+nombre+" fallida. Base de datos, vacía.");
			return false;
		} else {
			for (var i = 0; i < lista.length; i++) {
				if(lista[i] == nombre){
					lista.splice(i, 1);
					if(debugMode) {
					    console.log("El Cliente \""+nombre+"\" eliminado con éxito!");
					    console.log(lista);
					}
					operacionRealizada();
	                dataLog ("info", "administrador", 13, "Eliminado "+nombre+" de la base de datos de clientes");
					return true;
				} else if (i == lista.length -1){
				    if(debugMode) {
					    console.log("El cliente \""+nombre+"\" no encontrado!");
				    }
					operacionFallida();
			        dataLog ("error", "maquina", 14, "Eliminacion de "+nombre+" fallida. Cliente inexistente.");
				    return false;
				}
			}
		}
	}
	
	/* Testeamos Funcionalidad

	agregarCliente ("yo mismo", clientesBD)
	quitarCliente ("yo mismo", clientesBD)
	quitarCliente ("yo mismo", clientesBD)
	quitarDinero (1000)
	quitarDinero ("Mucho!!")
	agregarDinero (1000000)
	agregarDinero ("Poco!")
	ingresarEfectivo ("Yo mismo", 1000);
	ingresarEfectivo ("Alicia Gutierrez", "Poco!");
	ingresarEfectivo ("Alicia Gutierrez", 10);
	retirarEfectivo("Yo mismo", 1000)
	ingresarEfectivo ("Alicia Gutierrez", "Muchoo!");
	ingresarEfectivo ("Alicia Gutierrez", 10000);
	borrandoDatosVacios(cajeroAutomatico, "operaciones realizadas", 0);
	
	*/
	
```


10 - Refactorizamos y dejamos todo preparado para incluirlo en nuestro html, usando lo que hemos aprendido. 
	Evitando tambien que las funciones puedan ser accedidas desde la consola u otras librerias.

```javascript
	var myApp = myApp || {};

	myApp = (function (w){
		'use strict';
	/* VARIABLES */
	var debugMode = true;

	var clientesBD = ["Alicia Gutierrez", "Alfonso Gomez", "Luis Navarro", "Oscar Garcia", "Andres Fernandez", "Lucia Mellado"];

	var cajeroAutomatico = {
	    empresaPropietaria: "SuperExpress",
	    modelo: "Al-201",
	    "año": 2010,
	    serie: "01 Beta",
	    tipo: "Prototipo",
	    unidadMedida: "metros",
	    alto: 1,
	    ancho: 0.5,
	    largo: 0.5,
	    unidadPeso: "Kg",
	    peso: 600,
	    materiales: ["acero", "plástico", "cables", "circuitos"],
	    clientesAutorizados: clientesBD,
	    moneda: "Euros",
	    dineroDisponible: 65000
	};

	cajeroAutomatico.volumen = cajeroAutomatico.alto * cajeroAutomatico.ancho * cajeroAutomatico.largo;
	cajeroAutomatico.volumenMedida = cajeroAutomatico.unidadMedida.charAt(0) +3;

	/* FUNCIONES VERIFICACIÓN */

	/**
	 * Añade información sobre todo lo que ocurre en cajeroAutomatico.log.(logNUMERO).
	 * Actualiza cajeroAutomatico.logTotal con operaciones fallidas y operaciones realizadas.
	 * @param {string} tipo - "info" o "error".
	 * @param {string} origen - "usuario", "maquina" o "administrador".
	 * @param {string} codigo - código de error
	 * @param {string} detalles - Descripción del error.
	 */
	function dataLog (tipo, origen, codigo, detalles) {
	    cajeroAutomatico["operaciones fallidas"] = cajeroAutomatico["operaciones fallidas"] || 0;
	    cajeroAutomatico["operaciones realizadas"] = cajeroAutomatico["operaciones realizadas"] || 0;
	    cajeroAutomatico.logTotal = cajeroAutomatico.logTotal || 1;
	    cajeroAutomatico.log = cajeroAutomatico.log || [];
	    cajeroAutomatico.logTotal = cajeroAutomatico["operaciones fallidas"] + cajeroAutomatico["operaciones realizadas"];
	    cajeroAutomatico.log[cajeroAutomatico.logTotal] = [cajeroAutomatico.logTotal, tipo, origen, codigo, detalles ];

	}


	function esCliente(nombre) {
		if (cajeroAutomatico.clientesAutorizados === 0) {
		    if (debugMode) {
			    console.warn("La lista esta vacía.");
		    }
		    return false;
		} else {
			for (var i = 0; i < cajeroAutomatico.clientesAutorizados.length; i++) {
				if(cajeroAutomatico.clientesAutorizados[i] == nombre){
					if (debugMode) {
			            console.info(nombre+" eres cliente de "+cajeroAutomatico.empresaPropietaria);
					}
					return true;
				} else if (i == cajeroAutomatico.clientesAutorizados.length -1){
					if (debugMode) {
			            console.warn(nombre+" no encontrado!");
					}
					return false;
				}
			}
		}
	}

	function esNumero(n) {
	  return !isNaN(parseFloat(n)) && isFinite(n);
	}

	function operacionRealizada () {
	    if (isNaN(cajeroAutomatico["operaciones realizadas"]) || cajeroAutomatico["operaciones realizadas"] === undefined) {
	        cajeroAutomatico["operaciones realizadas"] = 1;
	        if(debugMode){
	            console.info("Primera operación realizada con éxito!");
	        }
	    } else {
	        cajeroAutomatico["operaciones realizadas"]++;
	        if(debugMode){
	            console.info("La operación #"+cajeroAutomatico["operaciones realizadas"]+" realizada con éxito!");
	        }        
	    }  
	}

	function operacionFallida () {
	    if (isNaN(cajeroAutomatico["operaciones fallidas"]) || cajeroAutomatico["operaciones fallidas"] === undefined) {
	        cajeroAutomatico["operaciones fallidas"] = 1;
	        if(debugMode){
	            console.warn("ERROR: Primera operación fallida!");
	        }
	    } else {
	        cajeroAutomatico["operaciones fallidas"]++;
	        if(debugMode){
	            console.warn("ERROR: La operación #"+cajeroAutomatico["operaciones fallidas"]+" fallo!");
	        }        
	    }  
	}

	function borrandoDatosVacios (objeto, propiedad, valorMinimo) {
	    if (objeto[propiedad] <= valorMinimo) {
	        delete objeto[propiedad];
	        return true;
	    } else {
	        return false;
	    }
	}


	/* FUNCIONES INTERACCIÓN */

	function retirarEfectivo (nombre, cantidad) {
	    if (esCliente(nombre)){
	        if (esNumero(cantidad)) {
	            cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible - cantidad;
	            operacionRealizada();
	            dataLog ("info", "usuario", 1, "Retirada de "+cantidad+cajeroAutomatico.moneda+" por "+nombre);
	            if(debugMode){
	                console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
	            }
	            return true;
	        } else {
	            operacionFallida();
	            dataLog ("error", "usuario", 2, "Retirada fallida por "+cantidad+" errónea. Usuario: "+nombre);
	            if(debugMode){
	                console.warn(cantidad+" No es un numero valido!");
	            }
	            return false;
	        }
	    } else {
	            operacionFallida();
	            dataLog ("error", "usuario", 3, nombre+" No es cliente");
	            if(debugMode){
	                console.warn(nombre+" No eres un cliente de "+cajeroAutomatico.empresaPropietaria+"!");
	            }
	            return false;
	    }    

	}

	function ingresarEfectivo (nombre, cantidad) {
	    if (esCliente(nombre)){
	        if (esNumero(cantidad)) {
	            cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible + cantidad;
	            operacionRealizada();
	            dataLog ("info", "usuario", 4, "Ingreso de "+cantidad+cajeroAutomatico.moneda+" por "+nombre);
	            if(debugMode){
	                console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
	            }
	            return true;
	        } else {
	            operacionFallida();
	            dataLog ("error", "usuario", 5, "Ingreso fallido por "+cantidad+" - errónea. Usuario: "+nombre);
	            if(debugMode){
	                console.warn(cantidad+" No es un numero valido!");
	            }
	            return false;
	        }
	    } else {
	            operacionFallida();
	            dataLog ("error", "usuario", 6, nombre+" No es cliente");
	            if(debugMode){
	                console.warn(nombre+" No eres un cliente de "+cajeroAutomatico.empresaPropietaria+"!");
	            }
	            return false;
	    }    

	}

	function agregarDinero (cantidad){
	    if (esNumero(cantidad)) {
	        cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible + cantidad;
	        operacionRealizada();
	        dataLog ("info", "administrador", 7, "Ingreso de "+cantidad+cajeroAutomatico.moneda);
	        if(debugMode){
	            console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
	        }
	        return true;
	    } else {
	        operacionFallida();
	        dataLog ("error", "administrador", 8, "Ingreso fallido por "+cantidad+" - errónea.");
	        if(debugMode){
	            console.warn(cantidad+" No es un numero valido!");
	        }
	        return false;
	    }

	}

	function quitarDinero (cantidad){
	    if (esNumero(cantidad)) {
	        cajeroAutomatico.dineroDisponible = cajeroAutomatico.dineroDisponible - cantidad;
	        operacionRealizada();
	        dataLog ("info", "administrador", 9, "Retirada de "+cantidad+cajeroAutomatico.moneda);
	        if(debugMode){
	            console.info("Dinero disponible en el cajero, "+cajeroAutomatico.dineroDisponible);
	        }
	        return true;
	    } else {
	        operacionFallida();
	        dataLog ("error", "administrador", 10, "Retirada fallida por "+cantidad+" - errónea.");
	        if(debugMode){
	            console.warn(cantidad+" No es un numero valido!");
	        }
	        return false;
	    }
	}

	function agregarCliente (nombre, lista) {
	lista.push(nombre);
	operacionRealizada();
	dataLog ("info", "administrador", 11, "Ingreso de "+nombre+" a la base de datos de clientes");
	return true;
	}

	function quitarCliente(nombre, lista) {
		if (lista.length === 0) {
		    if (debugMode) {
			    console.log("La lista esta vacía.");
		    }
			operacionFallida();
			dataLog ("error", "maquina", 12, "Eliminacion de "+nombre+" fallida. Base de datos, vacía.");
			return false;
		} else {
			for (var i = 0; i < lista.length; i++) {
				if(lista[i] == nombre){
					lista.splice(i, 1);
					if(debugMode) {
					    console.log("El Cliente \""+nombre+"\" eliminado con éxito!");
					    console.log(lista);
					}
					operacionRealizada();
	                dataLog ("info", "administrador", 13, "Eliminado "+nombre+" de la base de datos de clientes");
					return true;
				} else if (i == lista.length -1){
				    if(debugMode) {
					    console.log("El cliente \""+nombre+"\" no encontrado!");
				    }
					operacionFallida();
			        dataLog ("error", "maquina", 14, "Eliminacion de "+nombre+" fallida. Cliente inexistente.");
				    return false;
				}
			}
		}
	}
		return {
		    cajeroAutomatico: "Esto es todo lo que te muestro."
		};
	})(window);
```

11 (opcional) - Integrarlo con el html y bloquea el uso del de las funciones por consola

```javascript
	// Ejercicio Opcional
```


