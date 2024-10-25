# Guía de Despliegue en Digital Ocean

## Instalación y Configuración de Docker en el Droplet

- **Verificar si Docker está instalado:**  
  `sudo docker --version`

- **Actualizar dependencias del sistema:**  
  `sudo apt update`

- **Actualizar los paquetes ya instalados:**  
  `sudo apt upgrade`

- **Instalar dependencias necesarias:**  
  `sudo apt install apt-transport-https ca-certificates curl software-properties-common`

- **Descargar e instalar la clave GPG del repositorio oficial de Docker:**  
  `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`

- **Agregar el repositorio oficial de Docker a las fuentes de software:**  
  `echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`

- **Actualizar la lista de dependencias disponibles:**  
  `sudo apt update`

- **Instalar Docker Community Edition y componentes asociados:**  
  `sudo apt install docker-ce docker-ce-cli containerd.io`

- **Modificar la configuración del usuario para ejecutar Docker sin `sudo`:**  
  `sudo usermod -aG docker $USER`

## Instalación de Docker Compose

- **Instalar Docker Compose:**  
  `sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`

- **Hacer ejecutable Docker Compose:**  
  `sudo chmod +x /usr/local/bin/docker-compose`

- **Verificar la instalación de Docker Compose:**  
  `docker-compose --version`

## Configuración de Docker en el Sistema

- **Iniciar Docker en el sistema:**  
  `sudo systemctl start docker`

- **Habilitar Docker para que se inicie automáticamente al reiniciar:**  
  `sudo systemctl enable docker`

## Generación de Claves SSH

- **Generar un par de claves SSH para acceder al servidor:**  
  `ssh-keygen -t ed25519 -C "email@gmail.com"`

- **Mostrar el contenido de la clave pública (para agregarla en el repositorio):**  
  `cat ~/.ssh/id_ed25519.pub`

## Clonación del Repositorio y Despliegue

- **Clonar el repositorio en el servidor:**  
  `git clone git@github.com:user/repository.git`

- **Ejecutar Docker Compose en modo productivo, construir los contenedores y ejecutar en segundo plano:**  
  `docker compose -f docker-compose.prod.yml up --build -d`

- **Reiniciar un contenedor específico (si es necesario):**  
  `docker-compose restart containerName`


[Volver al índice](../README.md)  # Enlace para volver al índice

---

<p align="center">
  <samp>Hecho con código, café ☕ y determinación 💻</samp><br>
  <samp>Desarrollado por <a href="https://github.com/FerFranky">[Fernando Olmos]</a> 🚀</samp><br>
  <samp><i>// Siempre en constante evolución // 🔧</i></samp><br>
  <samp><i>if(works) { don't_touch_it(); }</i></samp>
</p>

---