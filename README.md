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
