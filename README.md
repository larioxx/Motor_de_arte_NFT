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
