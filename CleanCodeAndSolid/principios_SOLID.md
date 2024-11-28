# Principios SOLID
Los principios son sugerencias mas no reglas, pero el violentarlos debe ser una excepción aislada y no respetarlos pueden incrementar su deuda técnica.

Los principios **SOLID** nos indican como organizar nuestras funciones y estructuras de tatos en componentes y como dichos componentes deben estar interconectados.

Los 5 principios **S.O.L.I.D.** de diseño de software son:

- **S** - Single Responsibility Principle (SRP): Responsabilidad unica.
- **O** - Open/Closed Principle (OCP): Abierto y cerrado.
- **L** - Liskov Substitution Principle (LSP): Sustitucion de Liskov.
- **I** - Interface Segregation Principle (ISP): Segregacion de interfaz.
- **D** - Dependency Inversion Principle (DIP): Inversion de dependencias.

### Single Responsibility Principle (SRP):
Este principio esta enfocado a la creacion de clases y metodos y nos dice que cada uno de estos debe tener una unica responsabilidad

**"Nunca deberia haber mas de un motivo por el cual cambiar una clase o un modulo". - Robert C. Martin.**

Para implementar este principio de debe tomar en cuenta esta regla:

```typescript
"tener una unica responsabilidad" !== "hacer una unica cosa"
```

#### Detectar violaciones a SRP
- Tener nombres de clases y modulos demasiado genericos.
- Cambios en el codigo suelen afectar la clase o modulo.
- La clase involucra multiples capas.
- Numero elevado de importaciones.
- Cantidad elevada de metodos publicos.
- Excesivo numero de lineas de codigo.

#### Ejemplo de implementacion de SRP.

A continuacion se muestra una clase que **NO** aplica el principio de responsabilidad unica, el motivo de esto es que la clase `ProductBloc` hace multiples cosas, esta clase se encaga de:
- Obtener detalles de un producto.
- Almacenar productos.
- Agregar al carrito.
- Enviar notificaciones (emails) a los clientes.

```typescript
interface Product { 
        id:   number;
        name: string;
    }

    class ProductBloc {

        loadProduct( id: number ) {
            // Realiza un proceso para obtener el producto y retornarlo
            console.log('Producto: ',{ id, name: 'OLED Tv' });
        }

        saveProduct( product: Product ) {
            // Realiza una petición para salvar en base de datos 
            console.log('Guardando en base de datos', product );
        }

        notifyClients() {
            console.log('Enviando correo a los clientes');
        }

        onAddToCart( productId: number ) {
            // Agregar al carrito de compras
            console.log('Agregando al carrito ', productId );
        }

    }

    const productBloc = new ProductBloc();

    productBloc.loadProduct(10);
    productBloc.saveProduct({ id: 10, name: 'OLED TV' });
    productBloc.notifyClients();
    productBloc.onAddToCart(10);
```

Este codigo aunque es funcional no es escalable y es complicado testear. A continuacion haremos las mejoras necesarias para aplicar el principio de responsabilidad unica sin alterar el resultado obtenido.

**Paso 1:**

Lo primero que haremos es extraer el metodo `onAddToCart()` de la clase `ProductBloc`. 
Para esto, como en el contexto de productos la funcionalidad del carrito podemos asumir que es ajena a la logica de `ProductBloc` por lo que crearemos una nueva clase de la siguiente manera:
```typescript
class CartBlock {
        private itemsInCart: Object[] = []
        onAddToCart(productId: number) {
            // Agregar al carrito de compras
            console.log('Agregando al carrito ', productId);
        }
    }
```
Y en la implementacion del consumo de ese metodo cambia a la siguiente pero esta vez a traves de la clase `CartBlock`:
```typescript
const cartBlock = new CartBlock();
cartBlock.onAddToCart(10);
```

**Paso 2:**

El siguiente paso es aplicar `SRP` a los metodos `loadProduct` y `saveProduct`, si analizamos estos metodos actualmente tienen 2 funciones, funcionar como controlador para recibir la informacion y a la vez interacturar con los datos (En el producto final seria la Base de Datos), lo que haremos es sacar esta interaccion con los datos para que queden separadas las responsabilidades.

Para esto definiremos una clase `ProductService` que es la que contendra los metodos que interactuan con los datos:

```typescript
class ProductService {
        // private httpAdapter: Object = null;

        getProduct(id: number){
            // Realiza un proceso para obtener el producto y retornarlo
            console.log('Producto: ', { id, name: 'OLED Tv' });
        }
        saveProduct(product: Product){
            // Realiza una petición para salvar en base de datos 
            console.log('Guardando en base de datos', product);
        }
}
```
Una vez implementada esta clase cambiaremos el funcionamiento de `loadProduct` y `saveProduct` en la clase `ProductBloc` a traves de una instancia de la clase y de esta manera aseguramos el desacoplamiento de sus funcionalidades.
```typescript
class ProductBloc {

        private productService: ProductService

        constructor(productService: ProductService){
            this.productService = productService
        }

        loadProduct(id: number) {
            // Realiza un proceso para obtener el producto y retornarlo
            this.productService.getProduct(id)
        }

        saveProduct(product: Product) {
            // Realiza una petición para salvar en base de datos 
            this.productService.saveProduct(product)
        }
}
```
Con esto ya tendriamos abordado este tema, ahora tocara actualizar la instanciacion de estos metodos al consumirlos y quedarian de la siguiente manera junto con el que ya habiamos actualizado para el carrito.
```typescript
    const productService = new ProductService
    const productBloc = new ProductBloc(productService);
    const cartBlock = new CartBlock();

    productBloc.loadProduct(10);
    productBloc.saveProduct({ id: 10, name: 'OLED TV' });
    cartBlock.onAddToCart(10);
```
Lo anterior nos beneficia porque su implementacion esta desacoplada y por ejemplo si quisieramos hacer un test de la case `ProductBloc` por el nivel de desacoplamiento bastaria con hacer un mock de la clase `ProductService` haciendolo mas testeable y escalable.

**Paso 3:**

Para el metodo `notifyClients` como es una funcionalidad que posibliemente puede existir lo dejaremos en la misma clase de `ProductBloc`, en este caso en particular lo podemos dejar ahi pero es algo que se debe evaluar segun las necesidades de cada proyecto (Si en tu proyecto la necesidad es parecida, tocaria evaluar que pueda o no extraerse de aqui), lo que si tocara es de manera similar a lo evaluado en las funciones para producto, el metodo se queda ahi sin embargo la funcionalidad de las notificaciones se extreae en una nueva clase que en este caso simulara envio de Emails como se muestra a continuacion:

```typescript
class Mailer {
        private masterEmail: string = 'fol@email.com'

        sendEmail(emailList: string[], template: 'to-clients' | 'to-admins'){
            console.log('Enviado correo a los clientes', template);
            
        }
    }
```
Con esto ya aplicamos SRP ahora debemos hacer el cambio en el metodo `notifyClients` en la clase `ProductBloc` de la siguiente manera:
```typescript
notifyClients() {
    this.mailer.sendEmail(['contactos@email.com'], 'to-clients')
}
```
La clase `ProductBloc` se veria completa asi, actualizando el uso de la instanciacion del mailer que acabamos de crear:
```typescript
 class ProductBloc {

        private productService: ProductService
        private mailer: Mailer

        constructor(productService: ProductService, mailer: Mailer){
            this.productService = productService
            this.mailer = mailer
        }

        loadProduct(id: number) {
            // Realiza un proceso para obtener el producto y retornarlo
            this.productService.getProduct(id)
        }

        saveProduct(product: Product) {
            // Realiza una petición para salvar en base de datos 
            this.productService.saveProduct(product)
        }

        notifyClients() {
            this.mailer.sendEmail(['contactos@email.com'], 'to-clients')
        }
    }
```
Ahora solo nos faltaria cambiar nuestras instanciaciones para consumir nuestra clase:
```typescript
const mailer = new Mailer
    const productService = new ProductService
    const productBloc = new ProductBloc(productService, mailer);
    const cartBlock = new CartBlock();

    productBloc.loadProduct(10);
    productBloc.saveProduct({ id: 10, name: 'OLED TV' });
    productBloc.notifyClients();
    cartBlock.onAddToCart(10);
```
### Open - Close Principle (OCP):

Por su traduccion se le conoce como **Principio de Abierto y Cerrado** y la implementacion del mismo depende del contexto (La manera como se este ejecutando la aplicacion).

Establece que las entidades de software (clases, modulos, metodos, etc.) deben estar abiertas para la extension, pero cerradas para la modificacion.

#### Ejemplo 1 - Implementacion basica:
Supongamos que tenemos un requerimiento inicial donde creamos un archivo llamado **primero.txt** si no aplicamos **OCP** nuestra solucion pudiera verse asi:

```typescript
writeFile() {
    createFile('primero.txt')
}

this.writeFile()
```
Ahora suponiendo que en algun punto cambia el requerimiento y ahora debemos crear un archivo llamado **segundo.txt**, la modificacion natural seria ir y modificar la funcion con el nuevo nombre:
```typescript
writeFile() {
    createFile('segundo.txt')
}

this.writeFile('primero.txt')
this.writeFile('segundo.txt')
this.writeFile('el_que_sea.txt')
```

En el codigo anterior podemos obtener las siguientes conclusiones:
- Es **cerrado** porque la funcion cumple con su objetivo y ante cambios no requiere su modificacion.
- Es **abierto** porque la definicion de la misma permite escalar el proyecto, implementar la funcion en multiples contextos a partir de la misma base de codigo.

Aunque lo anterior es correcto, no permite que el software crezca sin necesidad de modificar la funcion original, siendo que si surgen nuevas necesidades de nombres, utilizar distintos al mismo tiempo, etc. Volveria a esta funcion un codigo cambiante que pudiera comprometer en cada modificacion el aplicativo.

Para esto debemos aplicar **OCP** de la siguiente manera:

```typescript
writeFile(fileName: string) {
    createFile(fileName)
}

this.writeFile()
```

El principio **abierto-cerrado** tambien se puede lograr de muchas maneras, incluso mediante el uso de **herencia** o mediante **patrones de disenio de composicion** como el **patron de estrategia**, **patron de adaptador**, entre otros.

#### Ejemplo 2 - Implementacion del patron adapter:

Imaginemos que tenemos el siguiente codigo para obtener items, posts y photos.

```typescript
const todoService = new TodoService();
const postService = new PostService();
const photosService = new PhotosService();

const todos = await todoService.getTodoItems();
const posts = await postService.getPosts();
const photos = await photosService.getPhotos();


console.log({ todos, posts, photos });
```

El codigo anterior depende de la implementacion de cada una de estas clases que se encargue de devolver esta informacion, una idea sencilla de como hacelo luciria asi:

```typescript
import axios from 'axios';


export class TodoService { 

    async getTodoItems() {
        const { data } = await axios.get('https://jsonplaceholder.typicode.com/todos/');
        return data;
    }
}


export class PostService {

    async getPosts() {
        const { data } = await axios.get('https://jsonplaceholder.typicode.com/posts');
        return data;
    }
}


export class PhotosService {

    async getPhotos() {
        const { data } = await axios.get('https://jsonplaceholder.typicode.com/photos');
        return data;
    }

}
```

El codigo anterior es funcional, sin embargo esta fuertemente ligado y dependiente de la libreria axios, una libreria de terceros, el uso de esta libreria nos da una fuerte dependencia hacia un sw de terceros que nosotros no controlamos.

Para el uso de librerias de terceros, se recomienda la implementacion de una clase adaptadora que se encargue de de la gestion de la misma para desacoplarla del resto de la funcionalidad del proyecto.

Un ejemplo de esto luciria asi:

```typescript
import axios from "axios";

export class HttpClient {
    async get(url: string) {
        const { data, status } = await axios.get(url)
        console.log(status);
        return { data, status }

    }
}
```

En la clase anterior podemos ver que:
- Extragimos el consumo del metodo get a un metodo propio que consume el metodo de `Axios`
- Centralizamos la importacion de la dependencia `Axios` en un solo lugar, por lo que si su implementacion cambia solo afectamos esta clase
- Se pide el campo `url` como `parametro` de la misma manera en que resolvimos la problematica en el ejemplo 1.

El siguiente paso es consumir nuestra clase en las clases que hacen peticiones `GET` quedando de la siguiente manera:

```typescript
export class TodoService { 
    constructor(private http: HttpClient){}
    async getTodoItems() {
        const { data } = await this.http.get('https://jsonplaceholder.typicode.com/todos/');
        return data;
    }
}


export class PostService {
    constructor(private http: HttpClient){}

    async getPosts() {
        const { data } = await this.http.get('https://jsonplaceholder.typicode.com/posts');
        return data;
    }
}


export class PhotosService {
    constructor(private http: HttpClient){}

    async getPhotos() {
        const { data } = await this.http.get('https://jsonplaceholder.typicode.com/photos');
        return data;
    }

}
```

Como podemos ver el unico cambio en cada clase fue la implementacion del `constructor` que condiciona el uso de la clase `HttpClient` y que cambiamos `axios.get` por `this.http.get`, es mas codigo pero ya no tenemos una dependencia directa con `axios` como podemos ver.

Finalmente solo inyectamos nuestra clase `HttpClient` en las instanciaciones y ya tendriamos cubierto el uso de **OCP** quedando de la siguiente manera:

```typescript
const http = new HttpClient()
const todoService = new TodoService(http);
const postService = new PostService(http);
const photosService = new PhotosService(http);

const todos = await todoService.getTodoItems();
const posts = await postService.getPosts();
const photos = await photosService.getPhotos();


console.log({ todos, posts, photos });
```

Pero... Cual es el beneficio de todo esto??? 

En escencia escribimos mas codigo, creamos una clase extra y esto puede hacernos pensar que lo hicimos mas complejo.

Ahora bien para entender el porque de las cosas imaginemos el siguiente escenario: Por una decision de "mejora tecnica" al reducir tanto como se pueda el numero de dependencias de terceros se decide no usar mas `Axios` y en su lugar implementar `Fetch` que es nativo del lenguaje. 

A partir de la clase adaptadora que creamos este cambio es super sencillo y transparente, ya que solo basta con remover en la clase `HttpClient` la importacion de axios, eliminar del proyecto la dependencia y hacer las adecuaciones necesarias al metodo `get` de esta manera:

```typescript
export class HttpClient {
    async get(url: string) {
        const resp = await fetch(url)
        const data = await resp.json()
        return { data, status: resp.status }

    }
}
```
Con ese cambio el proyecto funciona exactamente igual a cuando se tenia `Axios`, si no lo ubieramos hecho de esta manera tendriamos que aplicar esta modificacion en las 3 clases que hacen peticiones `http`, lo cual puede ser tedioso mientras mas grande sea el proyecto, pero al centralizarlo y desacoplarlo, unicamente modificamos la clase responsable y tenemos el mismo comportamiento que el inicial.

#### Detectar incumplimiendo de OPC

- Cuando los cambios agectan nuestra clase o modulo.
- Cuando una clase o modulo afecta muchas capas (Presentacion, almacenamiento, etc.).

### Principio de Sustitucion de Liskov

**"Las funciones que utilicen punteros o referencias a clases base, deben ser capaces de usar objetos de clases derivadas sin saberlo"- Robert C. Martin.**

El principio de sustitucion de Liskov se nombra asi en honor a la doctora Barbara Liskov.

Consiste en "Siendo *U* subtipo de *T*, cualquier instancia de *T* deberia poder ser sustituida por cualquier instancia de *U* sin alterar las propiedades del sistema".

#### Ejemplo:

Supongamos que tenemos la siguiente implementacion para diferentes marcas de coches, considerando que cada marca va a tener sus criterios propios no se ha centralizado en una unica funcion luciendo cada clase de esta manera:
```typescript
export class Tesla {

    constructor( private numberOfSeats: number ) {}

    getNumberOfTeslaSeats() {
        return this.numberOfSeats;
    }
}

export class Audi {

    constructor( private numberOfSeats: number ) {}

    getNumberOfAudiSeats() {
        return this.numberOfSeats;
    }
}

export class Toyota {

    constructor( private numberOfSeats: number ) {}

    getNumberOfToyotaSeats() {
        return this.numberOfSeats;
    }
}

export class Honda {

    constructor( private numberOfSeats: number ) {}

    getNumberOfHondaSeats() {
        return this.numberOfSeats;
    }
}
```

Ahora bien, se ha propuesto la siguiente implementacion para mostrar el numero de asientos de cada una de estas clases:

```typescript
    const printCarSeats = ( cars: (Tesla | Audi | Toyota | Honda)[] ) => {
        
        for (const car of cars) {
         
            if( car instanceof Tesla ) {
                console.log( 'Tesla', car.getNumberOfTeslaSeats() )
                continue;
            }
            if( car instanceof Audi ) {
                console.log( 'Audi', car.getNumberOfAudiSeats() )
                continue;
            }
            if( car instanceof Toyota ) {
                console.log( 'Toyota', car.getNumberOfToyotaSeats() )
                continue;
            }
            if( car instanceof Honda ) {
                console.log( 'Honda', car.getNumberOfHondaSeats() )
                continue;
            }         

        }
    }
    
    const cars = [
        new Tesla(7),
        new Audi(2),
        new Toyota(5),
        new Honda(5),
    ];


    printCarSeats( cars );
```

Apliquemos el principio de Liskov. Para esto trabajaremos sobre la definicion de las clases, si nos damos cuenta todas las clases implementan un metodo para obtener asientos, al ser una caracteristica en comun, podemos hacer uso de clases abstractas para tener una implementacion estandarizada del mismo para todas nuestras clases.

```typescript
export abstract class Vehicle {
    abstract getNumberOfSeats(): number
}
```

Una vez implementado nuestra clase abstracta con el metodo abstracto para obtener los asientos podemos implementarlo en cada una de nuestras clases de la siguiente manera:

```typescript
export class Tesla extends Vehicle {

    constructor(private numberOfSeats: number) {
        super()
    }

    getNumberOfSeats() {
        return this.numberOfSeats;
    }
}

export class Audi extends Vehicle {

    constructor(private numberOfSeats: number) {
        super()
    }

    getNumberOfSeats() {
        return this.numberOfSeats;
    }
}

export class Toyota extends Vehicle{

    constructor( private numberOfSeats: number ) {
        super()
    }

    getNumberOfSeats() {
        return this.numberOfSeats;
    }
}

export class Honda extends Vehicle{

    constructor( private numberOfSeats: number ) {
        super()
    }

    getNumberOfSeats() {
        return this.numberOfSeats;
    }
}
```

Aparentemente es mas codigo, pero gracias a esta implementacion hemos implementado el **Principio de Sustitucion Liskov** 

Ahora en nuestra funcion `printCarSeats`, gracias a la implementacion anterior podemos simplificar su implementacion de la siguiente manera haciendola mas sencilla ya que sabemos que todas nuestras instancias de las diferentes marcas son pertenecientes a la clase `Vehicle`:

```typescript
const printCarSeats = ( cars: Vehicle[] ) => { }
```

Nuestro codigo ya es funcional, sin embargo gracias a la implementacion que hicimos podemos hacerlo mas mantenible si lo implementamos asi:

```typescript
const printCarSeats = ( cars: Vehicle[] ) => {
        
    cars.forEach(car => {
        console.log( car.constructor.name, car.getNumberOfSeats() )
        
    });
}
```
Anteriormente se habia comentado que es importante evitar el uso de herencia, sin embargo recordemos que los principios abordados son sugerencias mas no reglas, por lo que aqui tenemos un ejemplo donde es perfectamente justificado el uso de herencia.

### Principio de Segregacion de Interfaz.

Establece que **"Los clientes no deberian estar obligados a depender de interfaces que no utilicen" - Robert C. Martin**.

Este principio consiste en dividir las interfaces si su implementacion no puede ser generalizada para su implementacion, a continuacion desarrollaremos un ejemplo para verlo de mejor manera:

Imaginemos que tenemos la implementacion de un sistema donde trabajaremos con distintas clases de aves, el paso natural al no conocer mayor detalles haria que a partir de una interface `Bird` hagamos la implementacion de nuestros metodos luciendo asi la verision inicial:

```typescript
interface Bird {
    fly(): void;
    eat(): void;
}
```
Una vez tenemos la interfaz podemos implementarla en nuestras clases, en este caso tendremos la clase `Tucan` y la clase `Humminbird`

```typescript
class Tucan implements Bird {
    public fly() { }
    public eat() { }
}

class Humminbird implements Bird {
    public fly() { }
    public eat() { }
}
```

Luce bien no? Ahora supongamos que nuestro requerimiento crece y debemos implementar tambien las clases `Ostrich` y `Penguin` pero si analizamos esto las avestruces son conocidas por correr rapido en lugar de volar y los pinguinos por nadar, agregamos estos metodos y bueno, podemos tomar diferentes acciones pero la realidad es que esta implementacion puede resultar no ser la mas adecuada como vemos a continuacion:
```typescript
interface Bird {
    fly(): void;
    eat(): void;
    run(): void;
    swim(): void;
}

class Tucan implements Bird {
    public fly() { }
    public eat() { }
    public run() { }
    public swim() { }
}

class Humminbird implements Bird {
    public fly() { }
    public eat() { }
    public run() { }
    public swim() { }
}

class Ostrich implements Bird {
    public fly() { }
    public eat() { }
    public run() { }
    public swim() { }
}

class Penguin implements Bird {
    public fly() { }
    public eat() { }
    public run() { }
    public swim() { }
}
```
Ahora bien, como solucionar esto, implementaremos una estrategia de segregacion, lo primero que haremos es dividir la interface `Bird` en interfaces mas especificas segun las necesidades especificas de cada clase y conservando unicamente los metodos que aplican a todas las clases de la siguiente manera:
```typescript
interface Bird {
    eat(): void;
}

interface FlyingBird {
    fly(): void;
}

interface RunningBird {
    run(): void;
}

interface SwimmerBird {
    swim(): void;
}
```

Con esto lo unico que queda es actualizar nuestras clases por las interfaces especificas para cada clase:

```typescript
class Tucan implements Bird, FlyingBird {
    public fly() { }
    public eat() { }
}

class Humminbird implements Bird, FlyingBird {
    public fly() { }
    public eat() { }
}

class Ostrich implements Bird, RunningBird {
    public eat() { }
    public run() { }
}

class Penguin implements Bird, SwimmerBird {
    public eat() { }
    public swim() { }
}
```

Esta implementacion pudiera parecer mas compleja, sin embargo, al hacerlo de esta manera las nuevas interfaces pueden crecer o bien agregar nuevas no dependientes unas de otras segun las necesidades del proyecto.

**NOTA:** Si las interfaces que diseñamos nos obligan a violentar los principios de responsabilidad unica y substitucion de Liskov es posible que se requiera aplicar **Segregacion de intefaz**.

### Depency Inversion (Principio de inversion de dependencias).

**"Los modulos de alto nivel no deben depender de modulos de bajo nivel. Ambos deben depender de abstracciones. Las abstracciones no deben depender de concreciones. Los detalles deben depender de las abstracciones" - Robert C. Martin.**

Lo anterior quiere decir que:

- Los modulos de alto nivel no deberian depender de modulos de bajo nivel.
- Ambos deberian depender de abstracciones.
- Las abstracciones no deberian depender de detalles.
- Los detalles deberian depender de abstracciones.

Al mencionar *Depender de abstracciones* nos referimos al uso de clases abstractas o interfaces.
Uno de los motivos mas importantes por el cual las reglas de negocio o capa de dominio deben depender de estas y no la concreciones es que aumenta su tolerancia al cambio.

**Por que obtenemos este beneficio?**
- Cada cambio en un componente abstracto implica un cambio en su implementacion.
- Por el contrario, los cambios en implementaciones concretas, la mayoria de las veces, no requieren cambios en las interfaces que implementa.

#### Inyeccion de dependencias:
Dependencia en programacion, significa que un modulo o componente requiere de otro para poder realizar su trabajo.

En algun momento nuestro programa o aplicacion llegara a estar formado por muchos modulos. Cuando esto pase, es cuando debemos usar inyeccion de dependencias.

Ejemplo:

A continuacion se muestra un ejemplo fuertemente dependiente entre dependencias.
```typescript
class UseCase {
    constructor() {
        this.externalService = new ExternalService();
    }

    doSomething() {
        this.externalService.doExternalTask();
    }
}

class ExternalService {
    doExternalTask() {
        console.log("Doing task...")
    }
}
```

Ahora aplicaremos inyeccion de dependencias para reducir la dependencia entre clases, tener mayor posibilidad de escalamiento y facilitar la creacion de Mocks para su testing.

```typescript
class UseCase {
    constructor(externalService: ExternalService) {
        this.externalService = externalService;
    }

    doSomething() {
        this.externalService.doExternalTask();
    }
}

class ExternalService {
    doExternalTask() {
        console.log("Doing task...")
    }
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