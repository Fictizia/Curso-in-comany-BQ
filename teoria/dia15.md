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
