
# Pipes en NestJS

NestJS proporciona **pipes** como herramientas que transforman y validan datos en los controladores y servicios. Aquí te explicamos algunos de los pipes más comunes y cómo utilizarlos:

---

## **1. ValidationPipe**
Este pipe valida automáticamente los datos de entrada contra un esquema de validación (por ejemplo, utilizando **class-validator**). Es útil para asegurarse de que los datos sean válidos antes de procesarlos.

### **Uso básico**
```typescript
import { Controller, Post, Body, ValidationPipe } from '@nestjs/common';
import { IsString, IsInt } from 'class-validator';

class CreateUserDto {
  @IsString()
  name: string;

  @IsInt()
  age: number;
}

@Controller('users')
export class UsersController {
  @Post()
  create(@Body(new ValidationPipe()) createUserDto: CreateUserDto) {
    return createUserDto; // Solo se procesarán datos válidos.
  }
}
```

### **Opciones comunes**
- `whitelist: true` - Elimina propiedades desconocidas del cuerpo.
- `forbidNonWhitelisted: true` - Lanza una excepción si se encuentran propiedades desconocidas.

---

## **2. ParseIntPipe**
Este pipe transforma el valor de entrada en un número entero. Si la entrada no puede convertirse a un entero, lanza una excepción.

### **Uso básico**
```typescript
import { Controller, Get, Param, ParseIntPipe } from '@nestjs/common';

@Controller('products')
export class ProductsController {
  @Get(':id')
  findOne(@Param('id', ParseIntPipe) id: number) {
    return `Producto con ID: ${id}`;
  }
}
```

### **Opciones**
- `errorHttpStatusCode`: Cambia el código de error HTTP en caso de fallo.

---

## **3. ParseBoolPipe**
Este pipe convierte un valor de entrada en un booleano (`true` o `false`). Si no puede realizar la conversión, lanza una excepción.

### **Uso básico**
```typescript
import { Controller, Get, Query, ParseBoolPipe } from '@nestjs/common';

@Controller('settings')
export class SettingsController {
  @Get()
  find(@Query('enabled', ParseBoolPipe) enabled: boolean) {
    return `Settings enabled: ${enabled}`;
  }
}
```

### **Entrada válida**
- Valores `true`: `"true"`, `"1"`, `true`
- Valores `false`: `"false"`, `"0"`, `false`

---

## **4. ParseArrayPipe**
Este pipe valida y transforma un valor en un array. Es ideal para trabajar con datos de listas en las solicitudes.

### **Uso básico**
```typescript
import { Controller, Post, Body, ParseArrayPipe } from '@nestjs/common';

class ItemDto {
  name: string;
  quantity: number;
}

@Controller('items')
export class ItemsController {
  @Post()
  createMany(
    @Body(new ParseArrayPipe({ items: ItemDto })) items: ItemDto[],
  ) {
    return items; // Devuelve un array validado.
  }
}
```

### **Opciones comunes**
- `items`: Clase DTO para validar cada elemento del array.
- `separator`: Define un separador personalizado para entradas de texto.

---

## **5. ParseFloatPipe**
Este pipe convierte un valor de entrada en un número de punto flotante. Si no puede realizar la conversión, lanza una excepción.

### **Uso básico**
```typescript
import { Controller, Get, Query, ParseFloatPipe } from '@nestjs/common';

@Controller('prices')
export class PricesController {
  @Get()
  find(@Query('amount', ParseFloatPipe) amount: number) {
    return `Monto: ${amount}`;
  }
}
```

---

## **6. ParseUUIDPipe**
Este pipe valida que la entrada sea un UUID válido. Es ideal para identificar recursos de manera única.

### **Uso básico**
```typescript
import { Controller, Get, Param, ParseUUIDPipe } from '@nestjs/common';

@Controller('orders')
export class OrdersController {
  @Get(':id')
  findOne(@Param('id', ParseUUIDPipe) id: string) {
    return `Orden con ID: ${id}`;
  }
}
```

### **Opciones**
- `version`: Especifica la versión del UUID que se debe validar (`'3'`, `'4'`, `'5'`).

---

## **Cómo Usarlos Globalmente**
Puedes aplicar estos pipes de manera global en toda tu aplicación utilizando el archivo `main.ts`.

```typescript
import { ValidationPipe } from '@nestjs/common';
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  // Aplicar ValidationPipe globalmente
  app.useGlobalPipes(new ValidationPipe({ whitelist: true }));

  await app.listen(3000);
}
bootstrap()
```
[Volver al índice](../README.md)  # Enlace para volver al índice

---

<p align="center">
  <samp>Hecho con código, café ☕ y determinación 💻</samp><br>
  <samp>Desarrollado por <a href="https://github.com/FerFranky">[Fernando Olmos]</a> 🚀</samp><br>
  <samp><i>// Siempre en constante evolución // 🔧</i></samp><br>
  <samp><i>if(works) { don't_touch_it(); }</i></samp>
</p>