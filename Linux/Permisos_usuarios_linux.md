# Comandos básicos de Permisos de Usuarios y Grupos en Linux

Este tutorial cubre los comandos básicos de Linux y la estructura del sistema de archivos, así como la gestión de paquetes, procesos, usuarios, grupos y permisos. Ideal para principiantes que buscan familiarizarse con la terminal y el funcionamiento de un sistema Linux.


## Gestión de Usuarios y Grupos

### Usuarios
- Agregar usuario: `sudo useradd -m <nombre_usuario>`
- Eliminar usuario: `sudo userdel <nombre_usuario>`
- Cambiar de usuario: `su <nombre_usuario>`

### Grupos
- Crear grupo: `sudo groupadd <nombre_grupo>`
- Agregar usuario a un grupo: `sudo usermod -G <nombre_grupo> <nombre_usuario>`
- Eliminar grupo: `sudo groupdel <nombre_grupo>`

---

## Gestión de Permisos

- **Cambiar permisos de un archivo:** 
`chmod u+x <nombre_del_archivo>` (permisos para el usuario)

- **Quitar permisos:**
`chmod o-wrx <nombre_del_archivo>` (quita permisos de otros)

- **Ver permisos de un archivo:**
`ls -l <nombre_del_archivo>`

- **Crear un archivo ejecutable de Linux:**  
  `echo "echo hola mundo" > archivo.sh`

- **Ejecutar un archivo:**  
  `./archivo.sh`

- **Agregar permisos de ejecución al usuario:**  
  `chmod u+x archivo.sh`

- **Revisar permisos del archivo:**  
  `ls -l archivo.sh`

- **Agregar permisos de ejecución al grupo:**  
  `chmod g+x archivo.sh`

- **Agregar permisos de ejecución a otros usuarios:**  
  `chmod o+x archivo.sh`

- **Ejemplo para quitar permisos de escritura, lectura y ejecución a otros usuarios:**  
  `chmod o-wrx archivo.sh`

- **Agregar permisos a usuario, grupos y otros:**  
  `chmod o+x,g-wr,u-w archivo.sh`

- **Reemplazar o igualar permisos de un archivo:**  
  `chmod u=xrw archivo.sh`

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