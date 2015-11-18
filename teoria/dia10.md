# Día 10


### Dudas

- [código 418](http://www.nytimes.com/418) un cásico [April Fools' Day](https://es.wikipedia.org/wiki/D%C3%ADa_de_las_bromas_de_abril)
![google_418](https://i1.wp.com/fat.gfycat.com/EquatorialAjarBlackfootedferret.gif)

- [Más bromas del Internet Engineering Task Force (IETF)](https://es.wikipedia.org/wiki/RFC_del_1_de_abril)



### AJAX

4 - Desarrolla una versión mejorada de [MovieFire](https://github.com/arvindr21/movieFire) (JS puro) incluyendo llamadas AJAX a la base de datos de IMBD para enriquecer los datos, usando [OMDb API](http://omdbapi.com/). 

```javascript
	// Tu solución aquí
```


### HTML5 API

### Geolocalización

- [Espeficicación](http://dev.w3.org/geo/api/spec-source.html)
- [Compatibildiad](http://caniuse.com/#feat=geolocation)

- Precisión:
    - Wi-fi (MAC)
    - Ethernet (IP)
    - Triangulación (3G y 4G)    
    - GPS (máxima precisión, pero tardará más en cargar)

- Métodos de *geolocation*
    - getCurrentPosition():
    ```javascript
        // Posición Actual
        navigator.geolocation.getCurrentPosition();
    ```
    - watchPosition():
    ```javascript
        // Seguimiento como un GPS 
        navigator.geolocation.watchPosition();
    ```
    - clearWatch():
    ```javascript
        // Para el seguimiento
        navigator.geolocation.clearWatch();
    ```
    
- Propiedades de *geolocation*
    - Latitud (en base 10):
    ```javascript
        console.info(position.coords.latitude);
    ```
    - Longitud (en base 10):
    ```javascript
        console.info(position.coords.longitude);
    ```    
    - Precisión en posicionamiento:
    ```javascript
        console.info(position.coords.accuracy);
    ```    
    - Altitud (metros por encima del nivel del mar):
    ```javascript
        console.info(position.coords.altitude);
    ```    
    - Precisión de altitud:
    ```javascript
        console.info(position.coords.altitudeAccuracy);
    ```     
    - Rumbo (Grados respectos al norte):
    ```javascript
        console.info(position.coords.heading);
    ```     
    - Velocidad (m/s):
    ```javascript
        console.info(position.coords.speed);
    ``` 
    - Timestamp:
    ```javascript
        console.info(position.timestamp);
    ``` 


- Ajustes de *geolocation*

    - enableHighAccuracy:
        - Mejora los datos para conexiones no GPS, pero aumenta drásticamente el consumo de batería del dispositivo.
        - *False por defecto*
    
    - timeout:
        - Tiempo (ms) de espera antes de lanzar el error.
        - *0 por defecto*
    
    - maximumAge:
        - Tiempo (ms) para el almacenamiento en memoria cache de la posición actual
        - *0 por defecto*
    
    - Ejemplo:
    ```javascript
        var opciones = {
            enableHighAccuracy: true,
            maximumAge: 1000, // 1s
            timeout: 2000 // 2s
        }
    ```


- Trabajando con *geolocation*

    - Comprobando la compatibildiad de *geolocation*
    ```javascript
        if ("geolocation" in navigator) {
          console.info("Podemos usar Geolocation! :-) ");
        } else {
          console.warn("Geolocation no soportado :-( ");
        }
    ```
    
    - Probando la geolocalización:
    ```javascript
        if ("geolocation" in navigator) {
            navigator.geolocation.getCurrentPosition(function(position) {
                // Consola
                console.info("Latitud: " + position.coords.latitude + "\nLongitud: "+ position.coords.longitude);
                // HTML
                var datos = "<h1>Te pille!</h1>"
                datos += "Latitud: " + position.coords.latitude.toFixed(4) + "<br>"
                datos += "Longitud: "+ position.coords.longitude.toFixed(4)
                document.body.innerHTML = datos;
            });
        } else {
          console.warn("Geolocation no soportado :-( ");
        }
    ```
    - Mostrar la localización en una imagen estatica usando Gogole Maps:
    ```javascript
        if ("geolocation" in navigator) {
            navigator.geolocation.getCurrentPosition(function(position) {

                var latlon = position.coords.latitude + "," + position.coords.longitude;
            
                var img_url = "http://maps.googleapis.com/maps/api/staticmap?center="+latlon+"&zoom=14&size=400x300&sensor=false";
            
                document.body.innerHTML = "<img src='"+img_url+"'>";
            });
        } else {
          console.warn("Geolocation no soportado :-( ");
        }    
    ```
    
    - Gestionar los Errores y rechazos:
    ```javascript
    navigator.geolocation.getCurrentPosition(geo_success, geo_error);
    
    function geo_success(position) {
      console.info(position.coords.latitude+","+ position.coords.longitude);
    }
    
    function geo_error(error) {
        switch(error.code) {
            case error.PERMISSION_DENIED:
                document.body.innerHTML = "El usuario ha rechazado la petición.";
                console.warn(error);
                break;
            case error.POSITION_UNAVAILABLE:
                document.body.innerHTML = "La posición de usuario no es correcta.";
                console.warn(error);
                break;
            case error.TIMEOUT:
                document.body.innerHTML = "No hay respuesta en el tiempo limite previsto.";
                console.warn(error);
                break;
            case error.UNKNOWN_ERROR:
                document.body.innerHTML = "Error Desconocido";
                console.warn(error);
                break;
        }
    }
    ```   
    
    - Trabajando con ajustes personalizados:
    ```javascript
    navigator.geolocation.getCurrentPosition(geo_exito, geo_error, opciones);
    
    var opciones = {
        enableHighAccuracy: true,
        maximumAge: 1000, // 1s
        timeout: 2000 // 2s
    }
    
    function geo_exito(position) {
        console.info(position.coords.latitude+","+ position.coords.longitude);
    }
    
    function geo_error(error) {
        console.warn("Error! - "+error);
    }
    ```
    
    - Convirtiendo las coordenadas a hexadecimal:
    ```javascript
    
    /**
     * From Isabel Castillo
     * http://isabelcastillo.com/convert-latitude-longitude-decimal-degrees
     * Convert longitude/latitude decimal degrees to degrees and minutes
     * DDD to DMS, no seconds
     * @param lat, latitude degrees decimal
     * @param lng, longitude degrees decimal
     */
            
    function convertDMS( lat, lng ) {
     
            var convertLat = Math.abs(lat);
            var LatDeg = Math.floor(convertLat);
            var LatSec = (Math.floor((convertLat - LatDeg) * 60));
            var LatCardinal = ((lat > 0) ? "n" : "s");
             
            var convertLng = Math.abs(lng);
            var LngDeg = Math.floor(convertLng);
            var LngSec = (Math.floor((convertLng - LngDeg) * 60));
            var LngCardinal = ((lng > 0) ? "e" : "w");
             
            return LatDeg + LatCardinal + LatSec  + "<br />" + LngDeg + LngCardinal + LngSec;
    }
    ```
    
    - Sigue a un usuario:
    ```javascript
    
        navigator.geolocation.watchPosition(geo_exito, geo_error);

        function geo_exito(position) {
            console.info(position.coords.latitude +", "+ position.coords.longitude);
        }
        
        function geo_error(error) {
            console.warn("Error! - "+error);
        }

    ```

**Google Maps**
- Librería
```html 
<script type='text/javascript' src="http://maps.googleapis.com/maps/api/js?sensor=false&extension=.js&output=embed"></script>
```

- Centrar el mapa
```javascript
function initMap() {
  var map = new google.maps.Map(document.getElementById('map'), {
    zoom: 8,
    center: {lat: -3.8199647, lng: 40.4381307}
  });
}
```

- Markers ( [Demo](https://developers.google.com/maps/documentation/javascript/examples/marker-labels) )
```javascript
// In the following example, markers appear when the user clicks on the map.
// Each marker is labeled with a single alphabetical character.
var labels = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
var labelIndex = 0;

function initialize() {
  var bangalore = { lat: 12.97, lng: 77.59 };
  var map = new google.maps.Map(document.getElementById('map'), {
    zoom: 12,
    center: bangalore
  });

  // This event listener calls addMarker() when the map is clicked.
  google.maps.event.addListener(map, 'click', function(event) {
    addMarker(event.latLng, map);
  });

  // Add a marker at the center of the map.
  addMarker(bangalore, map);
}

// Adds a marker to the map.
function addMarker(location, map) {
  // Add the marker at the clicked location, and add the next-available label
  // from the array of alphabetical characters.
  var marker = new google.maps.Marker({
    position: location,
    label: labels[labelIndex++ % labels.length],
    map: map
  });
}

google.maps.event.addDomListener(window, 'load', initialize);
```

- Markers Personalizados ( [Demo](https://developers.google.com/maps/documentation/javascript/examples/icon-simple) )
```javascript
// This example adds a marker to indicate the position of Bondi Beach in Sydney,
// Australia.
function initMap() {
  var map = new google.maps.Map(document.getElementById('map'), {
    zoom: 4,
    center: {lat: -33, lng: 151}
  });

  var image = 'images/beachflag.png';
  var beachMarker = new google.maps.Marker({
    position: {lat: -33.890, lng: 151.274},
    map: map,
    icon: image
  });
}
```

- InfoWindows ( [Demo](https://developers.google.com/maps/documentation/javascript/examples/infowindow-simple) )
```javascript
// This example displays a marker at the center of Australia.
// When the user clicks the marker, an info window opens.

function initMap() {
  var uluru = {lat: -25.363, lng: 131.044};
  var map = new google.maps.Map(document.getElementById('map'), {
    zoom: 4,
    center: uluru
  });

  var contentString = '<div id="content">'+
      '<div id="siteNotice">'+
      '</div>'+
      '<h1 id="firstHeading" class="firstHeading">Uluru</h1>'+
      '<div id="bodyContent">'+
      '<p><b>Uluru</b>, also referred to as <b>Ayers Rock</b>, is a large ' +
      'sandstone rock formation in the southern part of the '+
      'Northern Territory, central Australia. It lies 335&#160;km (208&#160;mi) '+
      'south west of the nearest large town, Alice Springs; 450&#160;km '+
      '(280&#160;mi) by road. Kata Tjuta and Uluru are the two major '+
      'features of the Uluru - Kata Tjuta National Park. Uluru is '+
      'sacred to the Pitjantjatjara and Yankunytjatjara, the '+
      'Aboriginal people of the area. It has many springs, waterholes, '+
      'rock caves and ancient paintings. Uluru is listed as a World '+
      'Heritage Site.</p>'+
      '<p>Attribution: Uluru, <a href="https://en.wikipedia.org/w/index.php?title=Uluru&oldid=297882194">'+
      'https://en.wikipedia.org/w/index.php?title=Uluru</a> '+
      '(last visited June 22, 2009).</p>'+
      '</div>'+
      '</div>';

  var infowindow = new google.maps.InfoWindow({
    content: contentString
  });

  var marker = new google.maps.Marker({
    position: uluru,
    map: map,
    title: 'Uluru (Ayers Rock)'
  });
  marker.addListener('click', function() {
    infowindow.open(map, marker);
  });
}
```


- Notas sobre GMaps:
    - [Documentación](https://developers.google.com/maps/documentation/javascript/)
    - [Ejemplos](https://developers.google.com/maps/documentation/javascript/examples/)
    - [Soporte Stackoverflow](https://stackoverflow.com/questions/tagged/google-maps-api-3)


**Ejercicios**:


1 - Utiliza Google Maps para posicionar al usuario.

```javascript
	 //	Tu solución aquí
```

2 - Utiliza Google Maps para posicionar al usuario en movimiento.

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
    
- Adaptamos una aplicación para que funcione offline


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