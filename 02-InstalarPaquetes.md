# Instalación de Paquetes y Gestión de Dependencias

Como habiamos dicho anteriormente, un paquete es una herramienta o librería de código que se puede "conectar" o "descargar" dentro de un proyecto.  

Cuando se ejecuta:  

<pre>
  npm install
</pre>  

NPM lee el archivo `package.json` creado anteriormente y el archivo `package-lock.json` si es que ya existe, y hace lo siguiente:  

1. descarga todos los paquetes o dependencias listadas en `"dependencies"` y `"devDependencies"`  

2. Crea o actualiza una carpeta llamada `node_modules`, que es la carpeta donde NPM instala todas las dependencias de tu proyecto.  

3. Si existe el archivo `package-lock.json`, respeta las versiones exactas allí indicadas (es un "fotograma" exacto del entorno que otros ya usaron).

4. Si no existe el archivo `package-lock.json`, al crearse la carpeta `node_modules`, lo genera desde cero.



## Instalar Express y Nodemon   

Para realizar la instalación de dependencias, debemos usar el comando `npm install` seguido del nombre del paquete que deseamos instalar.  

Instalar Express.js

<pre>
  npm install express
</pre>

Este comando realiza la siguiente acción:

1. Agrega `express` en tu proyecto  

2. Lo anota en `package.json` en la parte de `"dependencies"`  

3. Lo guarda en la carpeta `node_modules/`  

## Instalar Dependencias de Desarrollo  

El ejemplo más común es la instalación de `nodemon`, que reinicia el servidor automáticamente al "escuchar" cambios en el proyecto:  

<pre>
  npm install --save-dev nodemon
</pre>

O también la manera abreviada de decir `--save-dev`:  

<pre>
  npm install -D nodemon
</pre>

Esto se guarda en `"devDependencies"` en `package.json`.  

## Eliminar un paquete  

<pre>
  npm uninstall express
</pre>

