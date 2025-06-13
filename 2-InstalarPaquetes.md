# Instalación de Paquetes y Gestión de Dependencias

Como habiamos dicho anteriormente, un paquete es una herramienta o librería de código que se puede "conectar" o "descargar" dentro de un proyecto.  
Para realizar la instalación de paquetes, debemos usar el comando `npm install` seguido del nombre del paquete que deseamos instalar.  

Cuando se ejecuta:  

<pre>
  npm install
</pre>  

NPM descarga los paquetes desde su registro y los guarda físicamente en una carpeta llamada `node_modules`, junto con cualquier dependencia secundaria que esos paquetes necesiten.
