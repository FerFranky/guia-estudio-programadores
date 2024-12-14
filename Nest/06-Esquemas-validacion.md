# Variables de entorno en NestJS

Existen diferentes alternativas para este proceso, en este caso haremos uso de la libreria **joi**.

- Lo primero es instalar nuestra dependencia:
```bash
yarn add joi
```
- Trabajaremos con el archivo `env.ts` que habiamos creado en nuestra seccion anterior, donde importaremos nuestra dependencia `joi`
```ts
import * as joi from 'joi'
```
Posteriormente definiremos una `interface` que utilizaremos mas adelante para tipar los tipos de datos de nuestras variables de entorno.
```ts
interface EnvVars {
    PORT: number;
}
```
- El siguiente paso es definir el esquema esperado, en este caso lo haremos con las variables de entorno, agregaremos el metodo `unknown(true)` para que reciba todas las variables de entorno incluso las que no se definan en el esquema, en caso de no quererlo asi omitirlo o asignar el valor de `false` quedando de la siguiente manera nuestro esquema:
```ts
const envsSchema = joi.object({
    PORT: joi.number().required()
}).unknown(true)
```
- Una vez construido nuestro esquema, validaremos los valores del mismo con el metodo `validate` y del resultado extraeroemos las constantes `error` y `value` de la siguiente manera, donde si existe algun error desataremos una excepcion que nos evite levantar el server con anomalias y en caso contrario definiremos la constante con los valores ya validados y aplicando el tipado de nuestra interfaz:
```ts
const {error, value} = envsSchema.validate(process.env)
if (error) {
    throw new Error(`Config validation error: ${error.message}`)
}
const envVars:EnvVars = value;
```

El siguiente maso es modificar nuestra variable `envs` para en lugar de obtener los valores de `process.env` los traeremos de nuestro esquema ya validado de la siguiente manera:
```ts
export const envs = {
    port: envVars.PORT,
}
```

Finalmente nuestro archivo `env.ts` lucira de la siguiente manera
```ts
import 'dotenv/config'
import * as joi from 'joi'

interface EnvVars {
    PORT: number;
}

const envsSchema = joi.object({
    PORT: joi.number().required()
}).unknown(true)

const {error, value} = envsSchema.validate(process.env)
if (error) {
    throw new Error(`Config validation error: ${error.message}`)
}
const envVars:EnvVars = value;
export const envs = {
    port: envVars.PORT,
}
```