# Guía de Comandos Docker Compose

## Gestión de Contenedores

- **Crear y ejecutar contenedores:**  
  `docker compose up`

- **Ver ayuda de las opciones de Docker Compose:**  
  `docker compose up --help`

- **Construir imágenes sin utilizar la caché:**  
  `docker compose build --no-cache`

- **Detener, eliminar contenedores y redes:**  
  `docker compose down`

- **Construir, crear, ejecutar y enviar a segundo plano el contenedor:**  
  `docker compose up --build -d`

## Logs y Estado de Contenedores

- **Ver los últimos logs del contenedor:**  
  `docker compose logs`

- **Ver logs en tiempo real con su timestamp:**  
  `docker compose logs -f -t`

- **Ver los contenedores que se están ejecutando:**  
  `docker compose ps`


[Volver al índice](../README.md)  # Enlace para volver al índice
