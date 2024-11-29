# Instalacion y comandos utiles.

## Instalar CLI de NestJs

El siguiente comando permite a traves de `npm` instalar de manera global la `CLI` de `NestJs`.

```bash
npm i -g @nestjs/cli
```

## Crear un nuevo proyecto con nest
Crea un nuevo proyecto de Nest a partir del path actual donde estemos ubicados.
```bash
nest new project-name 
```

## Ejecutar el proyecto
Entrando al directorio que creo el comando anterior ejecutar:

Con YARN:
```bash
yarn run start:dev
```
Con NPM:
```bash
npm run start:dev
```
## Crear un resource
Crea un recurso completo (Entities, Controller con su CRUD, DTO, Service).
```bash
nest g resource <nombre> 
```

## Libreria para transformar tipos de datos
```bash
yarn add class-transformer
```

## Libreria para validaciones 
```bash
yarn add class-validator
```

[Volver al índice](../README.md)  # Enlace para volver al índice

---

<p align="center">
  <samp>Hecho con código, café ☕ y determinación 💻</samp><br>
  <samp>Desarrollado por <a href="https://github.com/FerFranky">[Fernando Olmos]</a> 🚀</samp><br>
  <samp><i>// Siempre en constante evolución // 🔧</i></samp><br>
  <samp><i>if(works) { don't_touch_it(); }</i></samp>
</p>

---