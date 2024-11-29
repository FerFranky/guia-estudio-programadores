# Agregar validators a los endpoints.

## Agregar configuracion con los pipes para mostrar los validators.

**Pipes:** Sirven para transformar la data recibida en requests, para asegurar un tipo, valor o instancia de un objeto.
Ej: Transformar a números, validaciones, etc.

- Debemos ubicar el archivo `./src.main.ts`.
- Haremos uso de la libreria `ValidationPipe` contenida en `@nestjs/common` con la siguiente importacion:
```typescript
import { ValidationPipe } from '@nestjs/common';
```
- Justo despues de definir la constante `app` que contiene el objeto de configuracion del aplicativo, debemos agregar la siguiente configuracion.
```typescript
app.useGlobalPipes(
    new ValidationPipe({
      whitelist: true,
      forbidNonWhitelisted: true
    })
  )
```
## Creacion de DTOs
Los archivos `DTO` contienen la preparacion y validacion de los atributos correspondientes a un request, comunmente sirven para preparar data para su uso en diferentes ambitos como interacciones con la BD, interaccion con APIs de terceros, etc.

En `NestJs` los `DTOs` se crean en cada dominio con la siguiente estructura:
```bash
./src/customDomain/dto/action-domain.dto.ts
```
## Uso de validators

En los archivos `dto` agregaremos los valores esperados en el enpoint, por ejemplo trabajaremos con el `POST` de la siguiente manera:

```typescript
export class CreateDomainDto {
    valueFirst: string;
    valueSecond: string
    valueThird: number
}
```
Con lo mencionado anteriormente, podemos recibir el response sin embargo aun no se esta validando, para eso haremos uso de la libreria `class-validator` donde podemos hacer uso de los siguientes decoradores `IsOptional`, `IsPositive`, `IsMongoId`, `IsArray`, `IsString`, `IsUUID`, `IsDecimal`,  `IsDate`, `IsDateString`, `IsBoolean`, `IsEmail`, `IsUrl`.

Agregaremos los correspondientes al ejemplo anterior:

Primero haremos las importaciones correspondientes segun los decoradores que utilizaremos de la siguiente manera:

```typescript
import { IsNumber, IsOptional, IsString } from "class-validator";
```
Posteriormente la implementacion lucira asi:

```typescript
export class CreateProductDto {
    @IsString()
    name: string;

    @IsString()
    @IsOptional()
    description: string

    @IsNumber()
    price: number
}
```

Con esto ya tenemos lo necesario para validar nuestro request, sin embargo podemos dar un paso extra bien podriamos hacer el uso de la libreria `class-transformer` a fin de implementar transformacion de datos del request a un formato especifico, por ejemplo si queremos transformar strings a numeros o a booleanos y esto nos ayuda a que nuestros endpoints puedan ser consumidos como `form` y no solo como `json`

La importacion necesaria luce de la siguiente manera:
```typescript
import { Type } from "class-transformer";
```

Y solo restaria agregar la conversion a nuestro `DTO` en este caso lo haremos en el campo `price` de nuestro `request`:

```typescript
export class CreateProductDto {
    @IsString()
    name: string;

    @IsString()
    @IsOptional()
    description: string

    @IsNumber()
    @Type(() => Number)
    price: number
}
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