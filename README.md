# NodeJS, Express y Jade (Pug). Ejemplos básicos.

## Iniciación a NodeJS

Los programas de ejemplo de NodeJS están en <a href="https://github.com/LuisJoseSanchez/nodejs-iniciacion">https://github.com/LuisJoseSanchez/nodejs-iniciacion</a>

## Instalación de Express

Para instalar <a href="http://expressjs.com/">Express</a> en un proyecto basta teclear lo siguiente:

```console
npm install express --save
```

## "Hola mundo" en Express

Crea el directorio del proyecto e instala Express.

```console
mkdir hola-mundo-express
cd hola-mundo-express
npm init
npm install express --save
```

Crea el fichero `index.js` con el siguiente contenido:

```javascript
// index.js
var express = require('express');
var app = express();

app.get('/', function (req, res) {
  res.send('¡Hola mundo!');
});

app.listen(8080);
```

Ejecuta la aplicación:

```console
node index.js
```


## "Hola mundo" con Jade

```console
mkdir hola-mundo-jade
cd hola-mundo-jade
npm init
npm install express --save
npm install jade --save
```

Crea el fichero `index.js` con el siguiente contenido:

```javascript
// index.js
var express = require('express');
var app = express();

app.set('view engine', 'jade');

app.get('/', function (req, res) {
  res.render('index');
});

app.listen(8080);
```

Crea la plantilla `index.jade` con el siguiente contenido:

```jade
<!DOCTYPE html>
html(lang="es")
head
  meta(charset="UTF-8")
  title Mi primera página con Jade
body
  h1 Mi primera página con Jade
  p ¡Hola mundo! Aquí estoy probando Jade.
```

Observa que no se utilizan etiquetas de cierre. Lo que determina cuáles son los bloques que engloban a otros es la indentación.


## Usando Javascript en la plantilla

```jade
<!DOCTYPE html>
html(lang="es")
head
  meta(charset="UTF-8")
  title Página con Jade
body
  h1 Página con Jade
  //- Este javascript se ejecuta en el servidor

  h2 Usando =
  - for (var i = 0; i < 10; i++) {
      = i
  - }

  h2 Usando p=
  - for (var i = 0; i < 10; i++) {
    p= i
  - }

  h2 Usando &num;
  - for (var i = 0; i < 10; i++) {
    span Número: #{i} 
  - }
```

## Cómo pasar datos a una plantilla

Fichero javascript con los datos:

```javascript
// index.js

var express = require('express');
var app = express();

app.set('view engine', 'jade');

app.get('/', function (req, res) {

var datos = {
  "nombre": "Aitor",
  "apellido": "Menta",
  "telefono": "555 123 456"
}

  res.render('index', datos);
});

app.listen(8080);
```

Plantilla en jade:

```jade
<!DOCTYPE html>
html(lang="es")
head
  meta(charset="UTF-8")
  title Página con Jade
body
  h2 Datos del empleado

  p.
    Nombre: #{nombre}#[br]
    Apellido: #{apellido}#[br]
    Teléfono: #{telefono}
```

## Enlaces en Jade

```jade
<!DOCTYPE html>
html(lang="es")
head
  meta(charset="UTF-8")
  title Página con Jade
body
  h2 Enlaces de interés

  ul
    li.
      Página de #[a(href="https://github.com/LuisJoseSanchez/github-alumnos-daw-1517") 2º DAW]
    li.
      #[a(href="https://naltatis.github.io/jade-syntax-docs/") Jade Syntax Documentation] by example
```

## Enrutamiento básico y paso de parámetros

Vamos a crear una aplicación con tres secciones: página de inicio, página de contacto y página de saludo.

A la página de inicio se accede indistintamente mediante las rutas `http://localhost:8080` y `http://localhost:8080/inicio`.

A la página de contacto se accede mediante la ruta `http://localhost:8080/contacto`.

La página de saludo nos mostrará un saludo personalizado según la URL. Por ejemplo, si accedemos a `http://localhost:8080/saluda/Luis`, la página mostrará el mensaje **Hola Luis, ¿qué tal estás?**.

Creamos el fichero `index.js`:

```javascript
// index.js
var express = require('express');
var app = express();

app.set('view engine', 'jade');

app.get('/', function (req, res) {
  res.render('index');
});

app.get('/inicio', function (req, res) {
  res.render('index');
});

app.get('/contacto', function (req, res) {
  res.render('contacto');
});

app.get('/saluda/:nombre', function (req, res) {
  datos = {
    "nombre": req.params.nombre
  };
  res.render('saluda', datos);
});

app.listen(8080);
```

Fichero `index.jade`:

```jade
<!DOCTYPE html>
html(lang="es")
head
  meta(charset="UTF-8")
  title Página con Jade
body
  h1 Página de inicio

  p.
    Lorem fistrum llevame al sircoo de la pradera a peich te voy a borrar el cerito va usté muy cargadoo diodenoo por la gloria de mi madre amatomaa. Fistro pupita sexuarl pecador papaar papaar qué dise usteer al ataquerl va usté muy cargadoo ese que llega quietooor diodeno. Torpedo te voy a borrar el cerito de la pradera no puedor qué dise usteer de la pradera va usté muy cargadoo. Pupita de la pradera ese que llega torpedo pecador se calle ustée se calle ustée a wan. Ese pedazo de te va a hasé pupitaa benemeritaar te va a hasé pupitaa llevame al sircoo torpedo diodeno te va a hasé pupitaa me cago en tus muelas benemeritaar. Ese hombree no puedor qué dise usteer fistro ese que llega me cago en tus muelas fistro quietooor ese hombree. Está la cosa muy malar está la cosa muy malar qué dise usteer pupita está la cosa muy malar. No puedor por la gloria de mi madre a gramenawer a gramenawer fistro por la gloria de mi madre ese hombree al ataquerl al ataquerl jarl.
```

Fichero `contacto.jade`:

```jade
<!DOCTYPE html>
html(lang="en")
head
  meta(charset="UTF-8")
  title Contacto
body
  h1 Contacto
  p Marie Curie, 10 - PTA Campanillas.
```

Fichero `saluda.jade`:

```jade
<!DOCTYPE html>
html(lang="en")
head
  meta(charset="UTF-8")
  title Saluda
body
  p Hola #{nombre}, ¿qué tal estás?
```
