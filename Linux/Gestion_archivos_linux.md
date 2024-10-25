# Comandos básicos de Gestión de Archivos en Linux

Este tutorial cubre los comandos básicos de Linux y la estructura del sistema de archivos, así como la gestión de paquetes, procesos, usuarios, grupos y permisos. Ideal para principiantes que buscan familiarizarse con la terminal y el funcionamiento de un sistema Linux.

## Sistema de Archivos en Linux

El sistema de archivos de Linux está estructurado en directorios con funciones específicas:

- **/bin**: Aplicaciones y comandos del sistema.
- **/boot**: Archivos relacionados con el arranque del sistema.
- **/dev**: Dispositivos conectados al sistema.
- **/etc**: Archivos de configuración de aplicaciones.
- **/home**: Archivos del usuario.
- **/lib**: Librerías y dependencias del sistema.
- **/media y /mnt**: Para montar dispositivos de almacenamiento.
- **/proc**: Información sobre los procesos en ejecución.
- **/root**: Directorio home del superusuario.
- **/sbin**: Comandos que solo puede ejecutar el superusuario.
- **/var**: Archivos que cambian con frecuencia, como logs.

---

## Gestión de Archivos y Directorios

- Crear un directorio: `mkdir <nombre_del_directorio>`
- Mover o renombrar archivos: `mv <ruta_antigua> <ruta_nueva>`
- Crear archivos: `touch <nombre_del_archivo>`
- Borrar archivos: `rm <nombre_del_archivo>`
- Borrar directorios de manera recursiva: `rm -r <nombre_del_directorio>`
- Ver el contenido de un archivo: `cat <nombre_del_archivo>`

---

## Editar Archivos con Nano

- Instalar nano: `sudo apt install nano`
- Crear o editar un archivo: `nano <nombre_del_archivo>`
- Guardar cambios: `Ctrl + O`
- Salir del editor: `Ctrl + X`
- Leer archivos largos parte por parte: `more <nombre_del_archivo>` o `less <nombre_del_archivo>`

---

## Comandos de Búsqueda

- Buscar texto en un archivo: `grep <texto_a_buscar> <archivo>`
- Buscar directorios: `find /etc`
- Buscar solo archivos: `find /etc -type f`
- Encadenar comandos: `comando1 && comando2 || comando3`

---

## Gestión de Variables de Entorno

- Listar variables de entorno: `env`
- Crear una variable temporal: `export NOMBRE="valor"`
- Agregar una variable al archivo `.bashrc` para que sea permanente: `echo "export NOMBRE='valor'" >> ~/.bashrc`

---

## Envío y Concatenación de Archivos

- Redirigir contenido de un archivo a otro: `cat <archivo1> > <archivo2>`
- Concatenar archivos: `cat <archivo1> <archivo2> > <nuevo_archivo>`
- Guardar errores en un archivo: `comando 2>> <archivo_errores>`

---

Este tutorial cubre los aspectos fundamentales de la terminal de Linux, la gestión de paquetes, archivos, procesos, usuarios y permisos. Puedes consultar más documentación oficial en sitios como [Linux Documentation Project](http://www.tldp.org/) para profundizar.

[Volver al índice](../README.md)  # Enlace para volver al índice

---

<p align="center">
  <samp>Hecho con código, café ☕ y determinación 💻</samp><br>
  <samp>Desarrollado por <a href="https://github.com/FerFranky">[Fernando Olmos]</a> 🚀</samp><br>
  <samp><i>// Siempre en constante evolución // 🔧</i></samp><br>
  <samp><i>if(works) { don't_touch_it(); }</i></samp>
</p>

---