# Leaflet - mapas para dispositivos móviles
En esta lección, se explica como configurar un mapa Leaflet para que se visualice adecuadamente en dispositivos móviles (ej. teléfonos celulares, tabletas). Esta configuración se realiza principalmente en el código HTML y CSS.

El contenido de esta lección está basado en el tutorial de Leaflet:  
[Leaflet on mobile](https://leafletjs.com/examples/mobile/)

## Cambios en el código HTML y CSS
Con el propósito de que el elemento ```div``` que contiene el mapa utilice toda la pantalla del dispositivo, puede utilizarse el siguiente código CSS:

```css
body {
  padding: 0;
  margin: 0;
}

html, body, #mapid {
  height: 100vw;
  width: 100vw;
}
```

Además, es necesario indicarle al navegador de Internet que no altere la escala de la página y que despliegue el tamaño actual de sus elementos, mediante el siguiente código HTML:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
```

## Geolocalización
El método [locate()](https://leafletjs.com/reference-1.7.1.html#map-locate) acerca el mapa a la ubicación detectada por el dispositivo que ejecuta el código.

```javascript
mapa.locate({setView: true, maxZoom: 16});
```

Para mostrar el punto geolocalizado, se agregar un *listener* al evento ```locationfound```.

```javascript
function onLocationFound(e) {
  var radius = e.accuracy / 2;

  L.marker(e.latlng).addTo(mapa)
    .bindPopup("Usted está en un radio de " + radius + " m de aquí").openPopup();

  L.circle(e.latlng, radius).addTo(mapa);
}

mapa.on('locationfound', onLocationFound);  
```

Por último, se manejan los posibles errores generados por el proceso de geolocalización.

```javascript
function onLocationError(e) {
    alert(e.message);
}

map.on('locationerror', onLocationError);
```

Puede ver un ejemplo de un mapa Leaflet configurado para dispositivos móviles en [https://tpb729-desarrollosigweb-2021.github.io/ejemplo-mapa-leaflet-movil/](https://tpb729-desarrollosigweb-2021.github.io/ejemplo-mapa-leaflet-movil/).
