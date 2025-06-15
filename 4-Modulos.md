# Qué son los Módulos ?

Node.js organiza el código en piezas reutilizables llamadas módulos. Estos permiten dividir la funcionalidad en diferentes archivos y aprovechar herramientas externas o integradas.

Node JS utiliza el sistema de módulos llamado CommonJS aunque también se puede utilizar el estándar ESModules. Ambos proporcionan una forma estándar de definir, importar y exportar módulos.  

Cada archivo de JavaScript en Node.js se considera un módulo por defecto, lo que significa que el código dentro de ese archivo está contenido en ese ámbito y no afectará a otros módulos a menos que se exporten específicamente ciertos elementos.  

### Módulos Internos

Son todos los archivos de nuestro proyecto donde disponibilizamos o exportamos código que puede ser importado como módulo desde otro archivo.  

### Módulos Nativos  

Node.js proporciona una amplia gama de módulos internos (core modules) que ofrecen funcionalidades listas para usar, como `http` para la creación de servidores web, `fs` para la manipulación de archivos, `path` para la manipulación de rutas de archivo, entre otros.  

### Módulos Externos  

Además de los módulos nativos, Node JS cuenta con un vasto ecosistema de módulos externos disponibles en el repositorio npm (Node Package Manager) o el gestor de paquetes de nuestra preferencia.  

## Importando, exportando y creando Módulos 

Actualmente, en JavaScript existen dos estándares principales para importar y exportar código, cada uno con características y casos de uso particulares:  

### 1. CommonJS (CJS)

Es el estándar más antiguo y ampliamente utilizado, con soporte nativo tanto en JavaScript como en Node.js. Ha sido el formato predeterminado para la gestión de módulos en Node.js durante muchos años.

Un ejemplo de como importar código con CJS: 

<pre>
  
</pre>
