# Agregar prefijo personalizado al API.

- Debemos ubicar el archivo `./src.main.ts`.
- Justo despues de definir la constante `app` que contiene el objeto de configuracion del aplicativo, debemos agregar la siguiente linea.
```typescript
app.setGlobalPrefix('api')
```
- La linea anterior reescribe el path de la siguiente manera:
```http
{domain}{newGlobalPrefix}(endpointUri)
```
- Dicho de esta manera en el ejemplo establecimos el prefijo `api` bien se puede establecer la version o cualquier otro estandar que se considere apropiado.


[Volver al índice](../README.md)  # Enlace para volver al índice

---

<p align="center">
  <samp>Hecho con código, café ☕ y determinación 💻</samp><br>
  <samp>Desarrollado por <a href="https://github.com/FerFranky">[Fernando Olmos]</a> 🚀</samp><br>
  <samp><i>// Siempre en constante evolución // 🔧</i></samp><br>
  <samp><i>if(works) { don't_touch_it(); }</i></samp>
</p>

---