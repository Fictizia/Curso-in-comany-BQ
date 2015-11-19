# Día 11

### Geolocalización (continuación)

**Ejercicios**:


1 - Utiliza Google Maps para posicionar al usuario.

```javascript
	 //	Tu solución aquí
```

2 - *RETO:* Partiendo de este [Gist](https://gist.github.com/strongwave/1297177), adapta el script a lo que aprendimos en estos días y compartelo usando Gist.
    - Nota: Recuerda que con Gist también puedes hacer *Forks*
    - Objetivos:
        - Reconstruir el script usando solo js, sin Jquery
        - Mejorar la representación visual de los datos
        - Utiliza las opciones avanzadas de Geolocation para mejorar la usabilidad

```javascript
	 //	Tu solución aquí
```
    
3 - Utiliza Ajax para posicionar al usuario y las estaciones de BiciMad en un mapa:

![Captura de localizaciones](https://github.com/UlisesGascon/bicimad-api/blob/master/ejemplos/img/gmaps_bicimad_station.png?raw=true)

- API:
    - [BiciMad Cercania](http://bicimad-api.herokuapp.com/api-v1/locations/nearest/?lat=40.418889&long=-3.691944&distance=1000000000)
    - [BiciMad Localizaciones](http://bicimad-api.herokuapp.com/api-v1/locations/)
    
```javascript
	 //	Tu solución aquí
```

4 - Utiliza esta [librería](https://github.com/UlisesGascon/Curso-in-comany-BQ/tree/master/otros/starwars) para posicionar al usuario, los cascos de StarWars con sus característicos iconos y la distancia estimada

![Captura](https://raw.githubusercontent.com/UlisesGascon/Face-the-force-con-html5/master/img/captura_helmets_distance.png)

- Nota: 
    - [Función para calcular la distancia entres dos puntos usando coordenadas](http://stackoverflow.com/questions/27928/calculate-distance-between-two-latitude-longitude-points-haversine-formula)
    - [Más sobre #FaceTheForce](http://www.starwars.es/face-the-force)
    - [Darth Vader podría estar mal localizado](http://www.20minutos.es/noticia/2605833/0/reparacion-casco/darth-vader/face-the-force/)

```javascript
	 //	Tu solución aquí
```

### Eventos

- Podemos escuchar eventos y enlazar funciones (*event handler*)
![img_pro_bu](http://i.stack.imgur.com/liJ5u.png)
- [Demo](http://jsfiddle.net/sc5Xa/2/)
- Propagación:
	- *Capturing* desde *document* hasta el elemento
	- *Target* impacta el elemento
	- *Bubbling* sube desde el elemento hasta *document*
	 

- Usando Eventos (Tradicional)
	- Solo una función por evento
	```html
		<button onclick="cambiarFondo()">Cambia el fondo</button>
	```
	
	```javascript
		function cambiarFondo() {
		
		// color = 'rgb(0-255,0-255,0-255'
		var color = 'rgb(' + Math.floor((Math.random() * 255))+ ',';
		color += Math.floor((Math.random() * 255)) + ',';
		color += Math.floor((Math.random() * 255)) + ')';
		
		document.body.style.backgroundColor= color;
		}
	```

- Usando Eventos (Callbacks)
	- Multiples funciones por evento
	- Necesidad de compatibilizar para IE8 
	```javascript
		// Callback - Manejador de Eventos
		function manejadorEventos(elEvento) {
		  	// Compatibilizar el evento
		  	var evento = elEvento || window.event;
		  	// Imprimir detalles
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
			// Desactivamos
			if (document.removeEventListener){ 
				document.removeEventListener('click', manejadorEventos, false);
				console.info("Listener quitado con exito");
			} else { // IE8
				document.detachEvent('onclick', manejadorEventos);
				console.info("Listener quitado con exito");
			}

		}
		
		// Añadimos Listener
		if (document.addEventListener){ 
			document.addEventListener('click', manejadorEventos, false);
			console.info("Listener añadido con exito");
		} else if (document.attachEvent){ // IE8
			document.attachEvent('onclick', manejadorEventos);
			console.info("Listener añadido con exito");
		} else {
			document.onclick = manejadorEventos;
			console.info("Listener añadido con exito");
		}
	```	

- Deteniendo el flujo
	- *.preventDefault()* evita el comportamiento por defecto (ex: Link -> nueva URL)
	- *.stopPropagation()* evita la propagación por el DOM


- Gestión vs. Delegación de eventos
	- Gestión (asociar un evento por elemento)
	```html
		<ul id="miNav">
			 <li><a href="#nosotros">¿Quienes Somos?</a></li>
			 <li><a href="#objetivos">Los objetivos</a></li>
			 <li><a href="#equipo">Nuestro Equipo</a></li>
			 <li><a href="#detalles">Más detalles</a></li>
			 <li><a href="#contacta">Contactanos</a></li>
		</ul>
	```
	```javascript
	   var miNav = document.getElementById("miNav");
	   var miNavLinks = miNav.getElementsByTagName("a");
	   for (var i = 0; i < miNavLinks.length; i++) {
	     miNavLinks[i].onclick = function(){
	        console.info(this.innerHTML);
	     }
	   }
	```
	- Delegación (asociar un único evento al padre de los elementos)
	```html
		<ul id="miNav">
			 <li><a href="#nosotros">¿Quienes Somos?</a></li>
			 <li><a href="#objetivos">Los objetivos</a></li>
			 <li><a href="#equipo">Nuestro Equipo</a></li>
			 <li><a href="#detalles">Más detalles</a></li>
			 <li><a href="#contacta">Contactanos</a></li>
		</ul>
	```
	```javascript
	   var miNav = document.getElementById("miNav");
	   miNav.onclick = function(evento){
	      var evento = evento || window.event;
	      var elemento = evento.target || evento.srcElement;
	      console.info(elemento.innerHTML);
	   }
	```

### Selectors

- Convencional:
    - getElementById():
    ```javascript
        // <tag id = x >
        document.getElementById("id");
    ```
    
    - getElementsByName():
    ```javascript
        // <tag name = x >
        document.getElementsByName("fname");
    ```
    
    - getElementsByTagName():
    ```javascript
        // <tag >
        document.getElementsByTagName("input");
    ```

- Selectores CSS3:

    - URL que empieza con "javascript:"
    ```javascript
        a[href^="javascript:"] {color:blue;}
    ```
    
    - URL que contiene "google.es"
    ```javascript
        a[href*="google.es"] {color:orange;}
    ```
    
    - URL que termina con ".pdf"
    ```javascript
        a[href$=".pdf"] {color:red;}
    ```


- Comprobando disponibilidad del API:
```javascript
// op.1 - Positivo

    if( document.querySelector && document.querySelectorAll ){
        console.info("querySelector() y querySelectorAll() estan soportados!!")
    }
// op.2 - Negativo

    if( typeof document.querySelector !== "function" && typeof document.querySelectorAll !== "function" ){
        console.warn("querySelector() y querySelectorAll() no estan soportados!!")
    }

```

- querySelector():
Devuelve el primer elemento que coincida con el selector 

```html
    <div id="miDiv">
        <span id="miId5" class="miClase" title="cinco"></span>
        <span id="miId4" class="miClase" title="cuatro"></span>
        <span id="miId3" class="miClase" title="tres"></span>
        <span id="miId2" class="miClase" title="dos"></span>
        <span id="miId1" class="miClase" title="uno"></span>
    </div> 
```

```javascript
    document.getElementById('miId1').title // uno
    document.querySelector('#miDiv .miClase').title // cinco
    document.querySelector('#miDiv #miId1.miClase').title // uno
    document.querySelector('#miDiv .inventado').title // ERROR -> undefined
    document.querySelector('#miDiv .miClase[title^=u]').title // uno
```

- querySelectorAll():
Devuelve todos los elementos que coincida con el selector en un array
```javascript
    document.querySelectorAll('#miDiv .miClase') // [<span id="miId5" ... ]
    document.querySelectorAll('p') // todos los parrafos
    document.querySelectorAll('div, img') // todos los divs e imágenes
    document.querySelectorAll('a > img') // todos las imágenes contenidas en enlaces
```


### LocalStorage

- Convencional:
    - Cookies:
    - Espacio limitado (4kb)
    - Por cada petición HTTP se envia y recibe todo el contenido
    - Caducidad 

- Tipos:
    - SessionStorage (Solo se almacenan los datos durante la sesión)
    - LocalStorage (Almacenamiento persistente)
    - GlobalStorage (Experimental - No usar)

- Uso y limitaciones:
    - 5-10Mb según navegador
    - Almacenamiento local
    - Sin caducidad
    - Funcionamiento clave/valor
    - Solo se permite el almacenamiento de cadenas de texto.


- Problemas Conocidos:
    - IE 8 y 9 almacena los datos basandose unicamente en el hostname, ignorando el protocolo (http/https) y el puerto.
    - En iOS 5 y 6 los datos se almacenan en una localización que puede ser borrada ocasionalmente por el SO.
    - Usando el modo "navegación privada" Safari, Safari para IOs y Navegadores Android no soportan sessionStorage o localStorage.
    - En IE al acceder a LocalStorage desde local, el objeto localStorage pasa a ser undefined.
    - Internet Explorer no soporta el almacenamiento de casi ninguna cadena de carácteres ASCII con una logitud menor a 20.
    - En IE el evento "storage" genera errores: 
        - IE10 : Se dispara el evento al usar iframes.
        - IE11 : Se confunden el valor antiguo con el nuevo valor (actualizado). 
    - IE10 en Windows 8 puede presentar el siguiente mensaje de error  "SCRIPT5: Access is denied" if "integrity" settings are not set correctly.
    - Chrome en Local no funciona correctamente

- Métodos de *LocalStorage*
    - setItem() Guardando datos
    ```javascript
        localStorage.setItem('clave', 'valor');
    ```
    
    - getItem() Recuperar un valor
    ```javascript
        console.info(localStorage.getItem('clave'));
    ```
    
    - length() Total de elementos
    ```javascript
        console.info(localStorage.length);
    ```
    
    - removeItem() Eliminar un elemento
    ```javascript
        localStorage.removeItem('clave');
    ```

- Comprobación
```javascript
    if (window.localStorage) {
        console.info("La función Html5 localStorage está soportada");
    } else {
        console.warn('Su navegador no soporta localStorage');
    }
    
    if (window.sessionStorage) {
        console.info('La función Html5 sessionStorage está soportada');
    } else {
        console.warn('Su navegador no soporta sessionStorage');
    } 
```
- Usando json en LocalStorage
```javascript
    var objeto = { 
        numero: 1, 
        booleano : true,
        array: ["dato", true, 2],
        cadena: "dato"
        };
    localStorage.setItem('clave', JSON.stringify(objeto));
    var objetoRecuperado = JSON.parse(localStorage.getItem('clave'));
    console.log(objetoRecuperado.booleano);    
```

- Eventos asociados
    - key: es la clave que se modifica
    - oldValue: es el valor anterior de la clave que se modifica
    - newValue: es el nuevo valor de la clave que se modifica
    - url: la página donde se modifica la clave
    - storageArea: el objeto donde se modifica la clave
    - [Usa dos Pestañas](http://stackoverflow.com/questions/3055013/html5-js-storage-event-handler)


- Ejercicios:
    - Sacar todas las claves guardadas
   ```javascript 
        for (var key in localStorage){
           console.log(key)
        }
    ```
    
    - Sacar todos los valores
    ```javascript
        for ( var i = 0; i < localStorage.length; i++ ) {
          console.log( localStorage.getItem( localStorage.key( i ) ) );
        }
    ```
    
    - Utiliza los eventos para monitorizar tu aplicación:
    ```javascript
    document.addEventListener('storage', function(event){
        console.info("Se registran cambios en "+event.key+". El valor pasó de ser "+event.oldValue+" a "+event.newValue+".\nRecuerda que estas en "+event.url+" y usando el almacenamiento "+event.storageArea);
    }); 
    ```

- **Ejercicios**    
    - Libreta de contactos (Básica)
    ```javascript
        // Tu solución
    ```
    
### ContentEditable

- Convencional:
    - Campos de texto
    - Formularios

- Comprobación:
```javascript 
    if (!document.body.contentEditable) {
        console.warn("No se puede utilizar contentEditable :-(");
    } else {
        console.info("Podemos utilizar contentEditable :-)");
    }    
```
- Usando *contentEditable* 
    - Atributo *contentEditable* (true, false, inherit)
    ```html 
        <!-- estilos: [contenteditable] y [contenteditable]:hover -->
        <!DOCTYPE html>
        <html>
          <body>
            <div contentEditable="true">
              Modificame... tanto como quieras!
            </div>
          </body>
        </html
    ```
    - designMode (editando todo el documento)
    ```javascript
        window.document.designMode = "on"; // off, por defecto
    ```
    
    - [execCommand](https://developer.mozilla.org/es/docs/Web/API/Document/execCommand)
        - [Demo](http://www-archive.mozilla.org/editor/midasdemo/)
        - [Código](https://developer.mozilla.org/en-US/docs/Rich-Text_Editing_in_Mozilla)
    
    - spellcheck (editando todo el documento)
    ```html
        <!DOCTYPE html>
        <html>
          <body>
            <div contentEditable="true" spellcheck="true">
              Modificame... tanto como quieras!
            </div>
          </body>
        </html
    ```


### Offline

- Uso y limitaciones:
    - Aplicación disponible independientemente del estado de la conexión
    - Se acelera la carga de los archivos
    - Disminuyen las consultas al servidor
    - En algunos navegadores es necesario que el usuario permita el almacenamiento

- Comprobación:
```javascript
    if (!window.applicationCache) {
        console.warn("No se puede utilizar applicationCache :-(");
    } else {
        console.info("Podemos utilizar applicationCache :-)");
    }
```

- Verificando la conexión:
```javascript
    if (window.navigator.onLine) {
        var detalles = "<h1>Estas Conectado a Internet!!</h1>";
        detalles += "<h3>Detalles del navegador:</h3>";
        detalles += "<p>CodeName: " + navigator.appCodeName + "</p>";
        detalles += "<p>Nombre: " + navigator.appName + "</p>";
        detalles += "<p>Versión: " + navigator.appVersion + "</p>";
        detalles += "<p>Cookies Habilitadas: " + navigator.cookieEnabled + "</p>";
        detalles += "<p>Lenguaje: " + navigator.language + "</p>";
        detalles += "<p>Plataforma: " + navigator.platform + "</p>";
        detalles += "<p>User-agent header: " + navigator.userAgent + "</p>";
        document.body.innerHTML = detalles;

    } else {
        document.body.innerHTML = "<h1>No estas Conectado!!</h1>"
        console.warn("No estamos conectados a Internet!");
    }
```
- Verificando la conexión usando eventos: 
```javascript
    window.addEventListener("offline", function(){
        console.warn("Estas desconectado!")
    });
    
    window.addEventListener("online", function(){
        console.info("Estas conectado!")
    });
```

- Usando Cache (manifest):
    - Uso:
        - Los archivos son visibles en la pestaña Resources/Application Cache
        - Extensión .appcache (asegurarnos del Content/Type)
        - El atributo manifest puede señalar a una URL pero deben tener el mismo origen que la aplicación web
        - Los sitios no pueden tener más de 5MB de datos almacenados en caché, pueden ser menos si el usuario lo cambia.
        - Si no se puede descargar el archivo de manifiesto o algún recurso especificado en él, fallará todo el proceso de actualización de la caché.
        - Añadir la versión del manifest como comentario.
        - JAMAS incluir el propio manifest dentro del manifest
        - Nuevo sistema de carga:
            - Si existe manifest, el navegador carga el documento y sus recursos asociados directamente desde local.
            - Se verifica si hubo actualizaciones al manifest.
            - Si se actualizo, el navegador descarga la nueva versión del archivo y de los recursos listados en él (segundo plano).
    - Estructura
        - CACHE, lo que se cacheará
        - NETWORK, lo que NO se cacheará
        - FALLBACK, que se visualizará si algo no esta disponible
    
    - Incluyendo el manifest
    ```html
        <html manifest="ejemplo.appcache"> 
          <!-- ... -->
        </html>
    ```
    
    - Ejemplo de Manifest
    ```
        CACHE MANIFEST
        # versión 1.0
        
        # SI CACHEAR
        CACHE:
        index.html
        offline.html
        css/style.css 
        js/script.js
        img1.jpg
        img2.jpg
        img3.jpg
        logo.png
        
        # Mostraremos offline.html cuando algo falle
        FALLBACK:
        offline.html
        
        # NO CACHEAR
        NETWORK:
        *
        # * es todo aquello que no este en CACHE
    ```
    
- Estados de Cache (manifest):
```javascript
    var appCache = window.applicationCache;

    switch (appCache.status) {
      case appCache.UNCACHED: // appCache.status == 0
        console.warn('Un objeto caché de la aplicación no se inicializó correctamente o falló.');
        break;
      case appCache.IDLE: // appCache.status == 1
        console.info('La caché no esta en uso.');
        break;
      case appCache.CHECKING: // appCache.status == 2
        console.info('El manifesto se ha obtenido y esta siendo revisado para actualizarse.');
        break;
      case appCache.DOWNLOADING: // appCache.status == 3
        console.info('Se estan descargando nuevos recursos debido a una actualización del manifesto.');
        break;
      case appCache.UPDATEREADY: // appCache.status == 4
        console.info('Hay una nueva versión del manifiesto.');
        break;
      case appCache.OBSOLETE: // appCache.status == 5
        console.info('El caché esta ahora obsoleto');
        break;
      default:
        console.warn('El Caché esta en estado desconocido');
        break;
    };
```    

- Eventos de Cache:
```javascript
function eventosCache(){

var appCache = window.applicationCache;
appCache.addEventListener('cached', chivato);
appCache.addEventListener('checking', chivato);
appCache.addEventListener('downloading', chivato);
appCache.addEventListener('error', chivato);
appCache.addEventListener('noupdate', chivato);
appCache.addEventListener('obsolete', chivato);
appCache.addEventListener('progress', chivato);
appCache.addEventListener('updateready', chivato);

    function chivato(e) {
        var conexion = (navigator.onLine) ? 'sí': 'no';
        var type = e.type;
        console.log('Conectado: ' + conexion+', Evento: ' + type +", \nMás Información: %O", e);
    }

} 
```

- Forzar la actualización (manualmente):

```javascript
var appCache = window.applicationCache;

appCache.update(); // Intentamos actualizar la versión del usuario con un nuevo manifest

if (appCache.status == window.applicationCache.UPDATEREADY) {
  appCache.swapCache();  // La ctualización es correcta y se cambiado a la nueva versión
}
```

**Ejercicio**
    
1 - Adaptamos una aplicación para que funcione offline
```javascript
    // Tu solución
```

### History

- Comprobación:
```javascript
    if (!window.history) {
        console.warn("No se puede utilizar history :-(");
    } else {
        console.info("Podemos utilizar history :-)");
    }
```

- Métodos de *History* 
    - length (total de entradas disponibles en el historial)
    ```javascript
        console.info(window.history.length);
    ```
    
    - go (hacia delante o hacia atras en función del numero) 
    ```javascript
        window.history.go(-1);// <- 1
        window.history.go(2); // 2 ->
        window.history.go(0); // refresh
        // sí te sales de rango, no pasa nada.
    ```

    - back (retrocede) 
    ```javascript
        window.history.back()
    ```

    - forward (avanza) 
    ```javascript
        window.history.forward()
    ```

- Métodos Avanzados de *History* 

    - pushState (añadir entradas al historial) 
    ```javascript
        // pushState(data, title , url)
        window.history.pushState({pag: 1}, "titulo 1", "?pag=1");
        console.log(history.state)
    ```

    - replaceState (remplazar entradas en el historial) 
    ```javascript
        // replaceState(data, title , url)
        window.history.replaceState({pag: 5}, "titulo 5", "?pag=5");
        console.log(history.state)
    ```


- Eventos de *History*
    - onpopstate (monitorizar cambios en el historial) 
    ```javascript
        window.onpopstate = function(event) {
          console.log("location: " + document.location + ", state: " + JSON.stringify(event.state));
        };
    ```

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
    var constructorCocheEmpresa = function (marca, modelo, antiguedad, color, tipo) {
        this.marca = marca;
        this.modelo = modelo;
        this.antiguedad = antiguedad;
        this.color = color;
        this.tipo = "" || tipo;
        var _ITVPasada = true;
        var _ITVfrecuencia = "Cada año";
        var _seguroEnRegla = true;
        var _companySeguros = "SegurExpress";
        var _tipoSeguro = "a terceros";
        if (this.tipo == ""){
            this.tipo = "berlina";
        }


        function _dameDetalles(){
          console.log("Tu coche es un "+marca+" "+modelo+" con "+antiguedad+" años, clase "+tipo+" y color "+color);
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
    var constructorCocheEmpresa = function (marca, modelo, antiguedad, color, tipo) {
        this.marca = marca;
        this.modelo = modelo;
        this.antiguedad = antiguedad;
        this.color = color;
        this.tipo = "" || tipo;
        var _ITVPasada = true;
        var _ITVfrecuencia = "Cada año";
        var _seguroEnRegla = true;
        var _companySeguros = "SegurExpress";
        var _tipoSeguro = "a terceros";
        if (this.tipo == ""){
            this.tipo = "berlina";
        }


        this.dameDetalles = function(){
          console.log("Tu coche es un "+marca+" "+modelo+" con "+antiguedad+" años, clase "+tipo+" y color "+color);
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
    var constructorCocheEmpresa = function (marca, modelo, antiguedad, color, tipo) {
        this.marca = marca;
        this.modelo = modelo;
        this.antiguedad = antiguedad;
        this.color = color;
        this.tipo = "" || tipo;
        var _ITVPasada = true;
        var _ITVfrecuencia = "Cada año";
        var _seguroEnRegla = true;
        var _companySeguros = "SegurExpress";
        var _tipoSeguro = "a terceros";
        if (this.tipo == ""){
            this.tipo = "berlina";
        }


        function _dameDetalles(){
          console.log("Tu coche es un "+marca+" "+modelo+" con "+antiguedad+" años, clase "+tipo+" y color "+color);
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
    
    - [Rendimiento comparado](http://jsperf.com/fibonacci-cache)
    
- Aplicaremos este mismo concepto a la función de [calculo factorial](http://www.wikiwand.com/es/Factorial) que vimos en clases anteriores.

Más Información:
- [Fixed-point combinators in JavaScript: Memoizing recursive functions](http://matt.might.net/articles/implementation-of-recursive-fixed-point-y-combinator-in-javascript-for-memoization/)


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
- [Más información](https://fernetjs.com/2012/05/patrones-module-y-namespace/s)
http://www.etnassoft.com/2011/04/11/el-patron-de-modulo-en-javascript-en-profundidad/
http://blog.aijoona.com/2011/03/17/patrones-de-diseno-y-javascript-module/


### Javascript Avanzado (Patrones de Diseño)

**Patrón Singleton**
- limitamos la instanciación de una clase a un objeto único

```javascript
    var miSingleton = (function () {
        var instancia;
     
        function crearInstancia() {
            var object = new Object("Instanciación");
            return object;
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
        if (isNaN(this.antiguedad)) {
            console.log("Error en el data-typing, antigüedad no es un número");
        }
        this.detalles = function (){
            console.log("Tu vehículo es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
        };
    };
    
    var furgon = function (opciones) {
        this.taraMinima = opciones.taraMinima;
        this.cargaUtil = opciones.cargaUtil;
        this.volumenCarga = opciones.volumenCarga;
        if (isNaN(this.taraMinima) || isNaN(this.cargaUtil) || isNaN(this.volumenCarga)) {
            console.log("Error en los datos. Por favor usar solo valores numéricos.");
        }
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
