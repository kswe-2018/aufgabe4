# Node.js

Installation von Node.js >= 8.9.x:

https://nodejs.org/en/download/ 

# Visual Studio Code

Installation Visual Studio Code:

https://code.visualstudio.com/

# Projektvorbereitung

Initialisierung:

* Verzeichnis erstellen, in VS Code öffnen
* Integriertes Terminal/Konsole öffnen (in Windows ist das die Powershell)
* `npm init -y`
* Webpack-Basis: `npm install webpack webpack-cli --save-dev`
* Webpack-Erweiterungen: `npm install html-loader node-sass sass-loader css-loader style-loader webpack-dev-server --save-dev`

* Leaflet installieren: `npm install leaflet --save`

## Projektstruktur:

```
  webpack-leaflet
  |- package.json
  |- index.html
  |- webpack.config.js
  |- /src
    |- index.js
```

Inhalt `index.html`:

```
<!doctype html>
<html>
  <head>
    <title>Getting Started</title>
  </head>
  <body>
    <div id="map"></div>
    <script src="dist/bundle.js"></script>
  </body>
</html>
```

Inhalt `src/style.scss`:

```
@import "~leaflet/dist/leaflet.css";

html, body, .full-width-height {
    margin: 0;
    padding: 0;
    width:100%;
    height:100%;
}

.map-placeholder {
    width:100%;
    height:100%;
}
```

## webpack.config.js

* Enthält Definition von Loadern (modules)

```
const path = require('path');

module.exports = {
    entry: './src/index.js',
    output: {
        filename: 'bundle.js',
        publicPath: '/dist/',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
        rules: [
            {
                test: /\.css$/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            },
            {
                test: /\.(png|svg|jpg|gif)$/,
                use: [
                    'file-loader'
                ]
            },
            {
                test: /\.scss$/,
                loader: 'style-loader!css-loader!sass-loader'
            },
            {
                test: /\.html$/,
                loader: 'html-loader'
            }
        ]
    }
};

```

## Dev Server

* webpack-dev-server

`npm install webpack-dev-server --save-dev`

* Einfügen eines Start-Skripts in der `package.json`:

```
{
  ...
  "scripts": {
    "serve": "webpack-dev-server"
  },
  ...
}
```

# Ausführen von Javscript

Inhalt `src/index.js`
```
import './style.scss';
import L from 'leaflet';

function component() {
    console.log('creating map');
    var mapElem = document.getElementById('map')
    var map = L.map(mapElem);
}

component();
```
