# Galerie photo

- Explication du projet :white_check_mark:
- Technologies employées :white_check_mark:
- Maquette sommaire :white_check_mark:
- Réalisation du projet NodeJs :white_check_mark:
- Réalisation du projet NodeJs + VueJs

## Explication du projet
Ce projet a pour but de comprendre le développement web récent. Le projet sur lequel nous allons travailler sera réalisé de 2 manières, une première en NodeJs standard, la seconde sera en NodeJs avec VueJs. C'est-à-dire que l'on pourra donc faire un parallèle entre les 2 pour comprendre ce qu'un framework (VueJs) peut nous apporter dans le développement de notre application (car on appelle désormais ainsi les projets webs).
L'application constituera à créer une galerie d'images, tout simplement.
Tout d'abord, nous verrons comment partir d'une bonne base, pour se lancer dans le bain, ensuite nous verrons comment atteindre notre objectif.

## Technologies employées

| Technologie        | Description |
|:-------------:|:-------------:|
| **HTML**       | Base du projet, c'est ce qui est transmis au navigateur (le fond)  |
| **CSS**        | Permet de faire des modifications graphique (la forme)      |
| **Javascript** | Permet de rendre des éléments dynamiques, c'est-à-dire qu'après que le navigateur est affiché la page, Javascript permet d'en modifier certains éléments en agissant sur le HTML et sur le CSS      |
| **NodeJs**     | Framework permettant de créer des applications web pouvant évoluer rapidement      |
| **VueJs**      | Framework permettant de créer des éléments dynamiques (par exemple, le chargement d'une galerie photo qui aurait évoluée dans le temps)      |

## Maquette sommaire

![](http://puu.sh/Csk3S/d1defa2dae.png)
Ce sera la base de notre travail, nous verrons par la suite si d'autres éléments doivent être ajoutés.

## Prérequis

- [NodeJs](https://nodejs.org/en/)
- Un éditeur de texte comme [Atom](https://atom.io/) ou [Visual Studio Code](https://code.visualstudio.com/) (pour le confort)

## Réalisation du projet NodeJs

### Création du front
#### Créer un projet NodeJs

On va d'abord commencer par créer un projet NodeJs, on crée donc un dossier sur notre machine, et une fois dans ce dossier, on lance la commande
```
npm init
```
On peut laisser les valeurs par défaut, pas de soucis.
Cela a donc créé un fichier package.json qui correspond à la configuration du projet.

*package.json*
```json
{
  "name": "galerienode",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

Ensuite, comme on peut le voir le fichier *main*, le fichier qui est appelé au lancement de l'application est appelé *index.js*, mais il n'existe pas encore, il va donc falloir le créer. Pour cela, on va partir de l'exemple donné sur [le site de NodeJs](https://nodejs.org/en/about/) :

*index.js*
```javascript
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

Pour lancer l'application et vérifier que tout fonctionne, on va donc lancer la commande
```
node index.js
```

On est alors gratifié d'un *Server running at http://127.0.0.1:3000/* si tout va bien.
On peut donc aller vérifier que tout est OK, en allant sur l'[adresse](http://127.0.0.1:3000/) mentionnée.

Pour se simplifier la vie, on va créer une ligne dans le *package.json*, ce qui donnera :
```json
"scripts": {
  "dev": "node index.js",
  "test": "echo \"Error: no test specified\" && exit 1"
},
 ```

On lancera donc désormais le programme avec la commande
```
npm run dev (dev étant le nom du script)
```

#### Ajout d'un Linter
Un Linter permet de vérifier notre code Javascript, il va dénicher les erreurs et les oublis et ainsi nous permettre d'avancer plus vite.
Nous allons donc installer ESLint.
```
npm install --save-dev eslint eslint-plugin-import eslint-config-airbnb-base
```
Ici, on installe ESLint en tant que plugin avec une configuration préconcue, tant mieux pour nous !

Mais la configuration n'est pas reliée à ESLint, il va donc falloir créer le fichier de configuration générale :

*.eslintrc.js*
```
module.exports = {
  extends: [
    'airbnb-base',
  ],
  plugins: [
    'import',
  ],
  env: {
    node: true,
  },
};
```

Ensuite, on va retourner dans *package.json* et on va mettre à jour la section scripts :
```json
"scripts": {
    "dev": "node index.js",
    "lint": "eslint index.js",
    "lint-fix": "eslint --fix index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  ```
  *lint* permet de lancer ESLint sur notre fichier index.js.
  *lint-fix* permettra de réparer les erreurs qui apparaitront (les règles d'Unix sont appliquées, nous voulons celles de Windows, c'est à ça que cela sert).

  Donc pas d'inquiétude si, lors d'un lancement de *lint*, on obtient quelque chose comme
  ```
   1:32  error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
   2:30  error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
   3:1   error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
   4:30  error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
   5:19  error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
   6:1   error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
   7:49  error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
   8:24  error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
   9:47  error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
  10:28  error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
  11:4   error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
  12:1   error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
  13:3  warning  Unexpected console statement  no-console
  13:38  error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
  14:64  error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style
  15:4   error  Expected linebreaks to be 'LF' but found 'CRLF'  linebreak-style

✖ 16 problems (15 errors, 1 warnings)
   15 errors and 0 warnings potentially fixable with the `--fix` option.
```
Un coup de *lint-fix*, et les erreurs s'envolent !
Par contre, il reste un warning "Unexpected console statement".
Ce warning indique qu'à la ligne 13 à partir du 3ème caractère une instruction appelant la *console* est donnée.
Il s'agit d'un warning car lors du déploiement de l'application, ceci ne devra pas exister. En effet, une application déployée ne doit pas contenir de "tests" fait par les développeurs.
Pour l'instant, on va donc ajouter un petit quelque chose à notre fichier *index.js*

*index.js*
```javascript
/* eslint-disable no-console */
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```
Cette nouvelle première ligne permet de dire à ESLint de ne pas répertorier les problèmes liés à la règle "no-console", le tour est joué !

On voit donc que la façon d'écrire ce fichier est assez lourde, avec ces informations précises de code de statut, de header à renvoyer... On va se simplifier la vie.

#### Installation d'Express

On va installer *express*, un package qui permet de rendre tout ceci bien plus propre et facile à commprendre.
On fait donc
```
npm install express
```

Après ça, on va modifier notre point d'entrée :

*index.js*
```javascript
/* eslint-disable no-console */
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Hello World!'));
app.listen(3000, () => console.log('Example app listening on port 3000!'));
```

On lance... Et en allant sur l'[adresse de tout à l'heure](http://127.0.0.1:3000/), on peut voir que tout va bien !
On a donc un serveur web fonctionnel, maintenant il va falloir créer notre page web, la galerie de photo.

On va donc créer le fichier *index.html* et modifier *index.js* en conséquence :
*index.js*
```javascript
/* eslint-disable no-console */
const express = require('express');
const app = express();

app.get('/', (req, res) => res.sendFile(__dirname + '/index.html')); //permet d'envoyer le fichier index.html aux navigateurs
app.listen(3000, () => console.log('Example app listening on port 3000!'));
```

### Création de la page

*index.html*
```html
<html>

<head>
  <meta charset="utf-8">
  <title>Galerie</title>
</head>

<body>
  <p>Hello, world!</p>
</body>

</html>
```

On relance le serveur, on vérifie que le message est toujours le même... Et hop, c'est tout bon !

#### Utilisation de Swiper

[Swiper](http://idangero.us/swiper/demos/) est un package qui permet de créer une galerie photo assez jolie, assez facilement, on va donc en profiter :
```
npm install swiper
```

Du coup, maintenant, on va devoir intégrer à la page les fichiers *.css* et *.js* qui correspondent à Swiper, ce qui nous mène donc à aller modifier *index.js* :

*index.js*
```javascript
/* eslint-disable no-console */
const express = require('express');
const app = express();

app.use(express.static('node_modules\\swiper\\dist')); //permet d'envoyer les fichiers relatif à Swiper
app.get('/', (req, res) => res.sendFile(__dirname + '/index.html')); //permet d'envoyer le fichier index.html aux navigateurs
app.listen(3000, () => console.log('Example app listening on port 3000!'));
```

On va donc ensuite modifier *index.html* :

- On ajoute dans la balise head le lien qui mène au *.css* de Swiper

*index.html*
```html
<html>
<head>
  <meta charset="utf-8">
  <title>Galerie</title>
  <meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1">
  <!-- AJOUT -->
  <link rel="stylesheet" href="/css/swiper.min.css">
  <!-- AJOUT -->
</head>
<body>
</body>
</html>
```

- On ajoute ensuite dans le body, le lien qui mène au *.js* de Swiper

*index.html*
```html
<html>
<head>
  <meta charset="utf-8">
  <title>Galerie</title>
  <meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1">
  <link rel="stylesheet" href="/css/swiper.min.css">
</head>
<body>
  <!-- AJOUT -->
  <script src="/js/swiper.min.js"></script>
  <!-- AJOUT -->
</body>
</html>
```

- Ensuite, on ajoute la dynamique CSS propre à notre exemple, qui est trouvable sur le site de Swiper, elle permet de donner un affichage propre à notre diaporama

*index.html*
```html
<html>
<head>
  <meta charset="utf-8">
  <title>Galerie</title>
  <meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1">
  <link rel="stylesheet" href="/css/swiper.min.css">

  <!-- AJOUT -->
  <style>
    html, body {
      position: relative;
      height: 100%;
    }
    body {
      background: #000;
      font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
      font-size: 14px;
      color:#000;
      margin: 0;
      padding: 0;
    }
    .swiper-container {
      width: 100%;
      height: 300px;
      margin-left: auto;
      margin-right: auto;
    }
    .swiper-slide {
      background-size: cover;
      background-position: center;
    }
    .gallery-top {
      height: 80%;
      width: 100%;
    }
    .gallery-thumbs {
      height: 20%;
      box-sizing: border-box;
      padding: 10px 0;
    }
    .gallery-thumbs .swiper-slide {
      height: 100%;
      opacity: 0.4;
    }
    .gallery-thumbs .swiper-slide-thumb-active {
      opacity: 1;
    }

  </style>
  <!-- AJOUT -->
</head>
<body>
  <script src="/js/swiper.min.js"></script>
</body>
</html>
```
- Et le plus important... Le HTML qui correspond à notre galerie photo !

*index.html*
```html
<html>
<head>
  <meta charset="utf-8">
  <title>Galerie</title>
  <meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1">
  <link rel="stylesheet" href="/css/swiper.min.css">

  <style>
    html, body {
      position: relative;
      height: 100%;
    }
    body {
      background: #000;
      font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
      font-size: 14px;
      color:#000;
      margin: 0;
      padding: 0;
    }
    .swiper-container {
      width: 100%;
      height: 300px;
      margin-left: auto;
      margin-right: auto;
    }
    .swiper-slide {
      background-size: cover;
      background-position: center;
    }
    .gallery-top {
      height: 80%;
      width: 100%;
    }
    .gallery-thumbs {
      height: 20%;
      box-sizing: border-box;
      padding: 10px 0;
    }
    .gallery-thumbs .swiper-slide {
      height: 100%;
      opacity: 0.4;
    }
    .gallery-thumbs .swiper-slide-thumb-active {
      opacity: 1;
    }

  </style>
</head>
<body>
  <!-- AJOUT -->
  <div class="swiper-container gallery-top">
    <div class="swiper-wrapper">
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/1/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/2/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/3/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/4/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/5/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/6/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/7/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/8/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/9/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/10/)"></div>
    </div>
    <div class="swiper-button-next swiper-button-white"></div>
    <div class="swiper-button-prev swiper-button-white"></div>
  </div>
  <div class="swiper-container gallery-thumbs">
    <div class="swiper-wrapper">
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/1/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/2/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/3/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/4/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/5/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/6/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/7/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/8/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/9/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/10/)"></div>
    </div>
  </div>
  <!-- AJOUT -->

  <script src="/js/swiper.min.js"></script>
</body>
</html>
```

- Ca ne marche toujours pas ? C'est normal, j'ai menti. Jusqu'à présent, nous avons récupéré les fichiers *.css* et *.js* qui correspondent à Swiper, et nous avons créer le HTML qui doit afficher, mais nous n'avons pas utilisé Swiper ! Pour ce faire, notre fichier va donc devoir être comme ceux présent dans la démo de Swiper, c'est-à-dire initialiser l'objet Swiper.

*index.html*
```html
<html>
<head>
  <meta charset="utf-8">
  <title>Galerie</title>
  <meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1">
  <link rel="stylesheet" href="/css/swiper.min.css">

  <style>
    html, body {
      position: relative;
      height: 100%;
    }
    body {
      background: #000;
      font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
      font-size: 14px;
      color:#000;
      margin: 0;
      padding: 0;
    }
    .swiper-container {
      width: 100%;
      height: 300px;
      margin-left: auto;
      margin-right: auto;
    }
    .swiper-slide {
      background-size: cover;
      background-position: center;
    }
    .gallery-top {
      height: 80%;
      width: 100%;
    }
    .gallery-thumbs {
      height: 20%;
      box-sizing: border-box;
      padding: 10px 0;
    }
    .gallery-thumbs .swiper-slide {
      height: 100%;
      opacity: 0.4;
    }
    .gallery-thumbs .swiper-slide-thumb-active {
      opacity: 1;
    }

  </style>
</head>
<body>
  <!-- AJOUT -->
  <div class="swiper-container gallery-top">
    <div class="swiper-wrapper">
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/1/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/2/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/3/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/4/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/5/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/6/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/7/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/8/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/9/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/10/)"></div>
    </div>
    <div class="swiper-button-next swiper-button-white"></div>
    <div class="swiper-button-prev swiper-button-white"></div>
  </div>
  <div class="swiper-container gallery-thumbs">
    <div class="swiper-wrapper">
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/1/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/2/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/3/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/4/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/5/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/6/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/7/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/8/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/9/)"></div>
      <div class="swiper-slide" style="background-image:url(http://lorempixel.com/1200/1200/nature/10/)"></div>
    </div>
  </div>
  <!-- AJOUT -->

  <script src="/js/swiper.min.js"></script>

  <!-- AJOUT -->
  <script>
  //Ici se trouve la partie du bas, les miniatures
    var galleryThumbs = new Swiper('.gallery-thumbs', {
      spaceBetween: 10,
      slidesPerView: 4,
      loop: true,
      freeMode: true,
      loopedSlides: 5, //looped slides should be the same
      watchSlidesVisibility: true,
      watchSlidesProgress: true,
    });
    //Ici se trouve la partie du haut, l'image visualisée
    var galleryTop = new Swiper('.gallery-top', {
      spaceBetween: 10,
      loop:true,
      loopedSlides: 5, //looped slides should be the same
      navigation: {
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev',
      },
      thumbs: {
        swiper: galleryThumbs,
      },
    });
  </script>
  <!-- AJOUT -->
</body>
</html>
```

On a donc une galerie photo fonctionnelle, **presque** prête à l'emploi.
Si l'on veut ajouter nos photos, il faudra modifier *index.js* pour qu'il ressemble à quelque chose comme ceci :

*index.js*
```javascript
/* eslint-disable no-console */
const express = require('express');
const app = express();

app.use(express.static('node_modules\\swiper\\dist'));
app.use(express.static('public')); //ajout du dossier public
app.get('/', (req, res) => res.sendFile(__dirname + '/index.html'));
app.listen(3000, () => console.log('Example app listening on port 3000!'));
```

Il faudra donc créer un dossier *public* à la racine du projet et y mettre les photos que l'on veut employer.
Puis, il faudra modifier le fichier *index.html* de la sorte :

*index.html* (zoom sur la partie importante)
```html
<!-- Swiper -->
  <div class="swiper-container gallery-top">
    <div class="swiper-wrapper">
      <div class="swiper-slide" style="background-image:url('MON_IMAGE.EXTENSION')"></div>

    </div>
    <!-- Add Arrows -->
    <div class="swiper-button-next swiper-button-white"></div>
    <div class="swiper-button-prev swiper-button-white"></div>
  </div>
  <div class="swiper-container gallery-thumbs">
    <div class="swiper-wrapper">
      <div class="swiper-slide" style="background-image:url('MON_IMAGE.EXTENSION')"></div>
    </div>
  </div>
```

Et voilà ! On a une application de galerie photo qui fonctionne !
Bravo !
Mais... Devoir modifier à chaque fois la page peut-être agaçant, donc on va dynamiser ça, en proposant une liste d'images qui sera envoyée à la page lorsque celle-ci le demandera.

On va installer [Axios](https://github.com/axios/axios), package qui permet de se faciliter la vie en terme de récupération et envoi d'information.
Comme d'habitude :
```
npm install axios
```

Ensuite, on va modifier le fichier *index.js* de la même manière que pour Swiper MAIS on va en plus créer une ligne *get* qui sera celle appelée pour envoyer la liste de photos :

*index.js*
```javascript
/* eslint-disable no-console */
const express = require('express');
const app = express();

app.use(express.static('node_modules\\swiper\\dist'));
app.use(express.static('node_modules\\axios\\dist')); // On ajoute Axios
app.use(express.static('public'));
app.get('/', (req, res) => res.sendFile(__dirname + '/index.html'));
app.get('/images', (req, res) => res.send("Cette API /images fonctionne !"));
app.listen(3000, () => console.log('Example app listening on port 3000!'));
```

Puis on modifie *index.html* pour qu'il l'incorpore :

*index.html* (zoom sur la partie import des scripts)
```html
<!-- AJOUT -->
<script src="/axios.min.js"></script>
<script>
  axios.get("/images").then(function (response) {
    // handle success
    alert(response.data);
  })
</script>
<!-- AJOUT -->
<script src="/js/swiper.min.js"></script>

<!-- Initialize Swiper -->
<script>
  var galleryThumbs = new Swiper('.gallery-thumbs', {
    spaceBetween: 10,
    slidesPerView: 4,
    loop: true,
    freeMode: true,
    loopedSlides: 5, //looped slides should be the same
    watchSlidesVisibility: true,
    watchSlidesProgress: true,
  });
  var galleryTop = new Swiper('.gallery-top', {
    spaceBetween: 10,
    loop:true,
    loopedSlides: 5, //looped slides should be the same
    navigation: {
      nextEl: '.swiper-button-next',
      prevEl: '.swiper-button-prev',
    },
    thumbs: {
      swiper: galleryThumbs,
    },
  });
</script>
```

Maintenant que cela fonctionne et qu'un message s'affiche lorsqu'on lance la page, on peut avancer.
On va d'abord s'occuper de créer et d'envoyer la liste d'images, ensuite, on pensera à incorporer nos images à la page.

Donc, d'abord, on va modifier *index.js* pour qu'il nous renvoie la liste d'images, qui sera en format JSON :

```javascript
/* eslint-disable no-console */
const express = require('express');
const app = express();

const images = 	[{ url: 'http://lorempixel.com/1200/1200/nature/1/' },
				{ url: 'http://lorempixel.com/1200/1200/nature/2/' },
				{ url: 'http://lorempixel.com/1200/1200/nature/3/' },
				{ url: 'http://lorempixel.com/1200/1200/nature/4/' },
				{ url: 'http://lorempixel.com/1200/1200/nature/5/' },
				{ url: 'http://lorempixel.com/1200/1200/nature/6/' },
				{ url: 'http://lorempixel.com/1200/1200/nature/7/' },
				{ url: 'http://lorempixel.com/1200/1200/nature/8/' },
				{ url: 'http://lorempixel.com/1200/1200/nature/9/' },
				{ url: 'http://lorempixel.com/1200/1200/nature/10/' }]

app.use(express.static('node_modules\\swiper\\dist'));
app.use(express.static('node_modules\\axios\\dist'));
app.use(express.static('public'));
app.get('/', (req, res) => res.sendFile(__dirname + '/index.html'));
app.get('/images', (req, res) => res.json(images));
app.listen(3000, () => console.log('Example app listening on port 3000!'));
```

Il nous reste à récupérer les informations maintenant :

*index.html* (zoom sur Axios)
```html
<script src="/axios.min.js"></script>
<script>
  var images = "";
  axios.get("/images")
  .then(function (response) {
    // handle success
    for (var image of response.data) {
      images += image.url + "\n";
    }
    alert(images);
  })
  .catch(function (error) {
    // handle error
    alert(error.data);
  })
</script>
```

Jusqu'ici, on ne fait que récupérer les informations, on ne les exploite pas, donc on va d'abord s'occuper de les ajouter à la page.
