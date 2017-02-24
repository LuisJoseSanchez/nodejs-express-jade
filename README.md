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
