# Guía de Comandos Docker para Imágenes y Contenedores

## Construcción y Gestión de Imágenes

- **Construir una imagen a partir de un Dockerfile:**  
  `docker build -t hola-mundo .`

- **Listar las imágenes existentes:**  
  `docker image ls`  
  `docker images`

- **Buscar y ejecutar una imagen en particular:**  
  `docker run name_image`

## Gestión de Contenedores

- **Ver procesos de Docker en ejecución:**  
  `docker ps`

- **Ver contenedores detenidos:**  
  `docker ps -a`

- **Ver contenedores detenidos con su descripción completa:**  
  `docker ps -la`

- **Ingresar a la shell de un contenedor (crea una nueva instancia):**  
  `docker run -it name_image`

- **Iniciar e ingresar a una imagen ya existente (usando su ID de contenedor):**  
  `docker start -i dockerId`

- **Entrar a un contenedor que ya está corriendo:**  
  `docker exec -it -u userName dockerId bash`

## Creación y Ejecución de Contenedores

- **Construir un contenedor y asignarle un nombre:**  
  `docker build -t app-name .`

- **Ejecutar el contenedor previamente construido y abrir una terminal `sh`:**  
  `docker run -it app-name sh`

## Limpieza y Eliminación

- **Eliminar los contenedores que no estén en uso:**  
  `docker container prune`

- **Eliminar imágenes que no estén en uso:**  
  `docker image prune`

- **Borrar una imagen específica:**  
  `docker image rm name-or-id`

- **Eliminar una imagen por nombre y versión:**  
  `docker image rm name-or-id:version`

## Gestión de Versiones y Publicación

- **Crear una imagen a partir de otra con una nueva etiqueta:**  
  `docker image tag app-name:1 app-name:2`

- **Subir una imagen al repositorio Docker Hub:**  
  `docker push user/name:tagname`

## Redes de Docker

- **Revisar las redes instaladas en Docker:**  
  `docker network ls`

[Volver al índice](../README.md)  # Enlace para volver al índice

---

<p align="center">
  <samp>Hecho con código, café ☕ y determinación 💻</samp><br>
  <samp>Desarrollado por <a href="https://github.com/FerFranky">[Fernando Olmos]</a> 🚀</samp><br>
  <samp><i>// Siempre en constante evolución // 🔧</i></samp><br>
  <samp><i>if(works) { don't_touch_it(); }</i></samp>
</p>

---