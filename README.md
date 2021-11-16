# Motor_de_arte_NFT
El motor de arte generativo es una herramienta que se utiliza para crear varias instancias diferentes de obras de arte basadas en las capas proporcionadas.

Cree arte generativo mediante el uso de canvas api y node js. Antes de utilizar el motor de generación, asegúrese de tener instalado node.js.

## Instalación 🛠️

Si está clonando el proyecto, ejecútelo primero; de lo contrario, puede descargar el código fuente en la página de lanzamiento y omitir este paso.

```sh
git clone https://github.com/larioxx/Motor_de_arte_NFT.git
```
Vaya a la raíz de su carpeta y ejecute este comando si tiene instalado Yarn.

```sh
yarn install
```

Alternativamente, puede ejecutar este comando si tiene un nodo instalado.

```sh
npm install
```
## Uso ℹ️

Cree sus diferentes capas como carpetas en el directorio 'capas' y agregue todos los archivos de capa en estos directorios. Puede nombrar los archivos de cualquier forma siempre que tenga un peso de rareza adjunto en el nombre del archivo, así: `ejemplo #70.png`. Opcionalmente, puede cambiar el delimitador `#` a cualquier cosa que le gustaría usar en la variable `rarityDelimiter` en el archivo `src/config.js`.

Una vez que tenga todas sus capas, vaya a `src/config.js` y actualice la matriz de objetos `layerConfigurations` objetos `layerOrder` para que sea el nombre de su carpeta de capas en el orden de la capa posterior a la capa frontal.

_Ejemplo:_ Si estuviera creando un diseño de retrato, es posible que tenga un fondo, luego una cabeza, una boca, ojos, gafas y luego sombreros, por lo que su `layerOrder` se vería así:

```js
const layerConfigurations = [
  {
    growEditionSizeTo: 100,
    layersOrder: [
      { name: "Cabeza" },
      { name: "Boca" },
      { name: "Ojos" },
      { name: "Gafas" },
      { name: "Cabeza" },
    ],
  },
];
```

El `name` de cada objeto de capa representa el nombre de la carpeta (en`/capas/`) en la que residen las imágenes.

Opcionalmente, ahora puede agregar múltiples "layerConfigurations" a su colección. Cada configuración puede ser única y tener diferentes órdenes de capas, usar las mismas capas o introducir nuevas. Esto le da al artista flexibilidad a la hora de ajustar sus colecciones a sus necesidades.

_Ejemplo:_ Si estuviera creando un diseño de retrato, es posible que tenga un fondo, luego una cabeza, una boca, ojos, gafas y luego sombreros y desee crear una nueva raza o simplemente reordenar las capas o incluso introducir nuevas capas, entonces eres `layerConfigurations` y` layerOrder` se vería así:

```js
const layerConfigurations = [
  {
    // Creates up to 50 artworks
    growEditionSizeTo: 50,
    layersOrder: [
      { name: "Fondo" },
      { name: "Cabeza" },
      { name: "Boca" },
      { name: "Ojos" },
      { name: "Gafas" },
      { name: "Sombrero" },
    ],
  },
  {
    // Crea 100 obras de arte adicionales
    growEditionSizeTo: 150,
    layersOrder: [
      { name: "Fondo" },
      { name: "Cabeza" },
      { name: "Boca" },
      { name: "Ojos" },
      { name: "Gafas" },
      { name: "Sombrero" },
      { name: "Especial" },
    ],
  },
];
```

Actualiza el tamaño de tu `format`, es decir, el tamaño de la imagen generada, y el `growEditionSizeTo` en cada objeto `layerConfigurations`, que es la cantidad de variación generada.

Puede mezclar el orden de `layerConfigurations` sobre cómo se guardan las imágenes estableciendo la variable `shuffleLayerConfigurations` en el archivo `config.js` en "true". Es "false" por defecto y guardará todas las imágenes en orden numérico.

Si desea tener registros para depurar y ver qué sucede cuando genera imágenes, puede establecer la variable `debugLogs` en el archivo `config.js` en "true". Es "false" de forma predeterminada, por lo que solo verá registros generales.

Si quieres jugar con diferentes modos de fusión, puedes agregar un campo `blend: MODE.colorBurn` al objeto layerOrder `options`.

Si necesita que las capas tengan una opacidad diferente, puede agregar el campo `opacity: 0.7` al objeto layerOrder `options` también.

Si desea tener una capa _ignorada_ en la comprobación de unicidad del ADN, puede establecer `bypassDNA: true` en el objeto `options`. Esto tiene el efecto de asegurarse de que el resto de los rasgos sean únicos sin considerar las Capas de "Fondo" como rasgos, por ejemplo. Las capas _están_ incluidas en la imagen final.

Para usar un nombre de atributo de metadatos diferente, puede agregar el `displayName: "Ojo Increible"` al objeto `options`. Todas las opciones son opcionales y se pueden agregar en la misma capa si lo desea.

Aquí hay un ejemplo de cómo puede jugar con ambos campos de filtro:

```js
const layerConfigurations = [
  {
    growEditionSizeTo: 5,
    layersOrder: [
      { name: "Fondo" , {
        options: {
          bypassDNA: false;
        }
      }},
      { name: "Globo Ocular" },
      {
        name: "Color Ojo",
        options: {
          blend: MODE.destinationIn,
          opacity: 0.2,
          displayName: "Ojo Increíble",
        },
      },
      { name: "Iris" },
      { name: "Brillo" },
      { name: "Parpado Inferior", options: { blend: MODE.overlay, opacity: 0.7 } },
      { name: "Parpado Superior" },
    ],
  },
];
```

Aquí hay una lista de los diferentes modos de fusión que puede usar opcionalmente.

```js
const MODE = {
  sourceOver: "source-over",
  sourceIn: "source-in",
  sourceOut: "source-out",
  sourceAtop: "source-out",
  destinationOver: "destination-over",
  destinationIn: "destination-in",
  destinationOut: "destination-out",
  destinationAtop: "destination-atop",
  lighter: "lighter",
  copy: "copy",
  xor: "xor",
  multiply: "multiply",
  screen: "screen",
  overlay: "overlay",
  darken: "darken",
  lighten: "lighten",
  colorDodge: "color-dodge",
  colorBurn: "color-burn",
  hardLight: "hard-light",
  softLight: "soft-light",
  difference: "difference",
  exclusion: "exclusion",
  hue: "hue",
  saturation: "saturation",
  color: "color",
  luminosity: "luminosity",
};
```

Cuando esté listo, ejecute el siguiente comando y su arte resultante estará en el directorio `build/images` y el json en el directorio `build/json`:

```sh
npm run build
```

o

```sh
node index.js
```

El programa generará todas las imágenes en el directorio `build/images` junto con los archivos de metadatos en el directorio `build/json`. Cada colección tendrá un archivo `_metadata.json` que consta de todos los metadatos de la colección dentro del directorio `build/json`. La carpeta `build/json` también contendrá todos los archivos .json individuales que representan cada archivo de imagen. El archivo .json único de una imagen se verá así:

```json
{
  "dna": "d956cdf4e460508b5ff90c21974124f68d6edc34",
  "name": "#1",
  "description": "Esta es la descripción de tu proyecto NFT",
  "image": "https://larioxx/nft/1.png",
  "edition": 1,
  "date": 1731990799975,
  "attributes": [
    { "trait_type": "Fondo", "value": "Negro" },
    { "trait_type": "Globo Ocular", "value": "Rojo" },
    { "trait_type": "Color Ojo", "value": "Amarillo" },
    { "trait_type": "Iris", "value": "Pequeño" },
    { "trait_type": "Brillo", "value": "Sombras" },
    { "trait_type": "Parpado Inferior", "value": "Bajo" },
    { "trait_type": "Parpado SUperior", "value": "Medio" }
  ],
  "compiler": "Generador de Arte"
}
```

También puede agregar metadatos adicionales a cada archivo de metadatos agregando sus elementos adicionales, pares (key:value) a la variable de objeto `extraMetadata` en el archivo `config.js`.

```js
const extraMetadata = {
  creator: "Larioxx",
};
```
Si no necesita metadatos adicionales, simplemente deje el objeto vacío. Está vacío por defecto.

```js
const extraMetadata = {};
```

Eso es todo, lo has conseguido. Felicidades!

## Utilidades

### Actualizando baseUri para IPFS y descripción

Es posible que desee actualizar la baseUri y la descripción después de haber ejecutado su colección. Para actualizar la baseUri y la descripción, simplemente ejecute:

```sh
npm run update_info
```

### Genera una previsualización de tus imagenes

Cree un collage de imágenes de vista previa de su colección, ejecute:

```sh
npm run preview
```

### Genera imágenes pixeladas de la colección

Para convertir imágenes en imágenes pixeladas, necesitaría una lista de imágenes que desea convertir. Así que primero ejecute el generador.

Luego, simplemente ejecute este comando:

```sh
npm run pixelate
```

Todas sus imágenes se enviarán al directorio `/build/pixel_images`.
Si desea cambiar la proporción de la pixelación, puede actualizar la propiedad de proporción en el objeto `pixelFormat` en el archivo `src/config.js`. Cuanto menor sea el número de la izquierda, más pixelada estará la imagen.

```js
const pixelFormat = {
  ratio: 5 / 128,
};
```

### Genera un GIF de la colección

Para exportar gifs basados ​​en las capas creadas, solo necesita establecer la exportación en el objeto `gif` en el archivo `src/config.js` en `true`. También puede jugar con el "repeat", la "quality" y el "delay" del gif exportado.

Establecer el `repeat: -1` producirá un render de una sola vez y` repeat: 0` se repetirá para siempre.

```js
const gif = {
  export: true,
  repeat: 0,
  quality: 100,
  delay: 500,
};
```
### Impresión de datos "raros" (función experimental)

Para ver los porcentajes de cada atributo en su colección, ejecute:

```sh
npm run rarity
```

La salida se verá así:

```sh
Trait type: Bottom lid
{ trait: 'Altas', chance: '20', occurrence: '15% de 100%' }
{ trait: 'Bajas', chance: '40', occurrence: '40% de 100%' }
{ trait: 'Medias', chance: '40', occurrence: '45% de 100%' }

Trait type: Iris
{ trait: 'Largo', chance: '20', occurrence: '15% de 100%' }
{ trait: 'Medio', chance: '20', occurrence: '15% de 100%' }
{ trait: 'Pequeño', chance: '60', occurrence: '70% de 100%' }
```

Espero que crees algunas obras de arte increíbles con este código

