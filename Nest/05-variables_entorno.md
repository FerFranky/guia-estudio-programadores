# Variables de entorno en NestJS

Existen diferentes alternativas para este proceso, en este caso haremos uso de la libreria **dotenv** ya que es una dependencia super ligera que facilita este proceso.

- Lo primero es instalar nuestra dependencia:
```bash
yarn add dotenv
```
- Posteriormente se debe crear la siguiente estructura de directorios y archivos que seran necesarios para el uso de variables de entorno:
```bash
- proyecto-raiz/
  - src/
    - config/
        - env.ts
  .env
  .env.template
```
- Trabajaremos primero con el archivo `env.ts` donde haremos la importacion de nuestra dependencia `dotenv`
```ts
import 'dotenv/config'
```
Posteriormente definiremos una constante en este caso `envs` donde nombraremos cada una de nuestras variables de entorno y las llamaremos a traves del `process.env` 
```ts
import 'dotenv/config'

export const envs = {
    port: process.env.PORT,
}
```
- El siguiente paso es trabajar con el archivo `.env` que es el que contendra las variables definidas con los valores a utilizar, en este caso como en el ejemplo usamos la variable `PORT` es las que definiremos de la siguiente manera:
```ts
PORT=3001
```
Ahora podemos hacer uso del puerto como variable de entorno si asi lo preferimos, para esto vamos a nuestro archivo `src/main.ts` y en la linea que configura el `app.listen` llamamos nuestra variable de la siguiente manera:
```ts
import { envs } from './config/env';
await app.listen(envs.port);
```
- Con esto solo bastaria con reiniciar nuestro servidor y ya podriamos configurar el puerto desde las variables de entorno, cabe aclarar que podemos definir tantas variables como necesitemos y podemos ocuparlas en cualquier parte del proyecto.
- Ahora solo nos restaria el archivo `env.template`, normalmente este archivo cuenta con el mismo contenido que `.env` solo que si se usan keys o datos sensibles se omiten para poder compartir a los distintos desarrolladores la estructura del mismo sin comprometer informacion.
