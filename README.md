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


