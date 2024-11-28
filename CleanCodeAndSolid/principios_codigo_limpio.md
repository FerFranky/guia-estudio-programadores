# Principios de Código Limpio

**Código limpio** es aquel que se escribe con la intención de que sea comprensible para otros desarrolladores. Algunos principios clave incluyen:
- **Simplicidad y claridad**: El código debe ser directo y fácil de leer.
- **Legibilidad**: Programar es el arte de decirle a otro humano lo que quieres que la computadora haga. El código debe leerse con la misma facilidad que un texto bien escrito.

Un enfoque en el código limpio reduce la deuda técnica y facilita el mantenimiento y la colaboración en el proyecto.

## Nombres de variables pronunciables y expresivos

- **Evitar el uso de iniciales:** El nombre debe ser completamente descriptivo para referirse y entender el porque de su implementacion
    - Mal: `const n = 53`
    - Bien: `const numberOfUnits = 53`
- **Evitar el uso de abreviaciones:** Este tipo de terminos generalmente no son entendibles para las personas que leen el codigo por primera vez e incluso dificulta entenderse si el mismo programador lo retoma despues de un largo tiempo.

    - Mal: `const tx = 0.16`
    - Mal: `const cat = "T-Shirts"`
    - Bien: `const tax = 0.16`
    - Bien: `const category = "T-Shirts"`
- **Nombres descriptivos:** El nombre de las variables debe de expresar el concepto al que se refiere, evitando el uso de nomenclaturas propias que pueden mas bien ser confusas
    - Mal: `const ddmmyyyy = new Date('August 15, 1965 00:00:00')`
    - Bien: `const birthDate = new Date('August 15, 1965 00:00:00')`

## Nombres de clases e interfaces
Los nombres de las clases e interfaces se recomienda sean lo mas limpias posibles.
- Evitar agregar el tipo de clase al nombre del archivo, en el siguiente ejemplo se muestra como NO debe nombrarse una clase abstracta ya que no es necesario ya que en el codigo se especifica esto, por lo que agregarlo resulta redundante.
    - Mal: `class AbstractUser {};`
- Evitar especificar las caracteristicas o acciones que realiza la clase.
    - Mal: `class UserImplementation {};`
- La definicion de interfaces no requiere indicar el tipo de archivo ya que en su definicion misma se especifica.
    - Mal: `interface UserInterface {};`
- Los nombres tanto de clases como de interfaces deben indicar la entidad tal cual sobre la que esta trabajando, por ejemplo.
    - Bien: `class User {};`
    - Bien: `interface User {};`
### Consideraciones al nombrar clases
Deben formar su nombre por sustantivos o frases de sustantivos evitando el uso de nombres genericos.

Se deben nombrar utilizando UpperCamelCase

Para saber si se esta nombrando correctamente una clase de debe considerar:
- Que hace exactamente la clase?
- Como exactamente esta clase realiza cierta tarea?
- Hay algo especifico sobre su ubicacion?
- Recuerda que si algo no tiene sentido, remuevelo o refactorizalo.
## Nombres segun su tipo de dato
### Arrays:
Los nombres de los arrays no deben ser en singular, ya que este tipo de dato esta pensado para almacenar n numero de elementos de un mismo tipo
- Mal: `const fruit = ['manzana', 'platano', 'fresa']`

En ocaciones buscando ser descriptivos optamos por especificar que el array es una lista, aunque esto no es del todo incorrecto no siempre es la mejor opcion.
- Aceptable:  `const fruitList = ['manzana', 'platano', 'fresa']`

Generalmente la mejor opcion es definir el array con el nombre en plural ya que da el contexto especifico de lo que se esta hablando, de igual manera, generalmente se utiliza esta forma de definir los arrays cuando hay mas de una caracteristica en el array.
- Correcto:  `const fruits = ['manzana', 'platano', 'fresa']`

Aunque el ejemplo anterior es correcto, para este caso en especifico la mejor opcion es nombrar el array especificando de manera concreta el contenido del mismo, como podemos ver en el ejemplo no estamos almacenando frutas junto con sus multiples caracteristicas, en especifico lo que almacena son nombres de frutas
- Optimo: `const fruitNames = ['manzana', 'platano', 'fresa']`

### Booleanos

Se considera una buena practica que este tipo de variables tengan un verbo asignado que ayude a identificar de mejor manera a que se refiere.
El verbo `is` generalmente se ocupa para indicar si la variable esta en un estado especifico, el siguiente ejemplo comun sirve para determinar las interacciones de apertura de un elemento que requiere una constante llamada `open` y como nombrarla correctamente:
- Mal: `const open = true`
- Bien: `const isOpen = true`

Los valores que pueden tomar las variables booleanas en general son `true` o `false` por lo que se puede tomar tambien `false` al inicializar una variable en caso de necesitarlo
- Mal: `const active = false`
- Bien: `const isActive = false`

De igual manera en ocasiones este tipo de variables se ocupan como banderas para otorgar/quitar permisos de ciertas acciones, para esto complementamos el nombre con el verbo `can`
- Mal: `const write = true`
- Bien: `const canWrite = true`

Otro uso que se le da a este tipo de variables es como bandera para determinar la pertenencia de un elemento a otro, para esto usamos el metodo `has`
- Mal: `const fruit = true`
- Bien: `const hasFruit = true`

Otra consideracion es que los nombres de las variables deben evitar el uso de expresiones negativas y esto aplica en cualquiera de los verbos mencionados anteriormente, de igual manera se debe considerar que el ajuste de nombres en este tema impacta tambien en el valor al inicializarse como en los siguientes ejemplos
- Mal: `const noValues = true`
- Bien: `const hasValues = false`
- Mal: `const notEmpty = true`
- Bien: `const isEmpty = false`

### Variables numericas
En ocaciones se ocupa tal cual el nombre del objeto al que se hace referencia como se muestra a continuacion:
- Mal: `const fruits = 3`
- Mal: `const cars = 10`

Sin embargo al hacerlo de la manera anterior, el contexto de a que se refiere la variable queda muy ambiguo ya que puede referirse a lo mismo en diferentes contextos, para esto, es buena practica utilizar prefijos auxiliares como `max`, `min`, `total` o bien `totalOf` estos, a discresion de las necesidades del valor que se este ocupando
- Bien: `const maxFruits = 5`
- Bien: `const minFruits = 1`
- Bien: `const totalFruits = 3`
- Bien: `const totalOfFruits = 3`

### Funciones
"Sabemos que estamos desarrollando codigo limpio cuando cada funcion hace exactamente lo que su nombre indica". - Ward Cunningham.

En ocasiones al nombrar nuestras funciones, se suele recurrir a hacerlo mencionando ciertas caracteristicas importantes con las que cumple la funcion y esto puede hacer inecesariamente largas nuestras definiciones:
- Mal: `createUserIfNotExists();`
- Mal: `updateUserIfIsNotEmpty();`
- Mal: `sendEmailIfFieldsValid();`

La recomendacion para definir de manera mas limpia los nombres de las funciones es hacerlo con un verbo seguido de la entidad a la que hace referencia, obviando que las acciones o validaciones propias de la funcion las realiza como parte de su comportamiento aceptado y no es necesario hacer mencion de este de manera explicita, a continuacion de muestran las funciones anteriores corregidas
- Bien: `createUser();`
- Bien: `updateUser();`
- Bien: `sendEmail();`

Como buena practica de Clean code, se recomienda que tenga cuando maximo 3 argumentos:
```typescript
// Correcto
function sendEmail(email: string): boolean {}

// Correcto
function sendEmail(email: string, subject: string): boolean {}

// Correcto
function sendEmail(email: string, subject: string, apiKey: string): boolean {}
```
A continuacion veremos como seria una implementacion con multiples argumentos que no seria tan legible y entendible:
```typescript
// Incorrecto
function sendEmail(email: string, from: string, body:string, subject: string, apiKey: string): boolean {}
```
Existen diferentes maneras en que el codigo anterior se puede mejorar,por ejemplo en typescript se puede lograr una implementacion mas limpia haciendo uso de interfaces y desestructurando los argumentos enviados, por ejemplo:
```typescript
interface SendEmailOptions {
    email: string;
    from: string;
    body: string;
    subject: string;
    apiKey: string;
}

function sendEmail({ email, from, body, subject, apiKey }: SendEmailOptions): boolean {}
```
Otra recomendacion a seguir para facilitar la lectura de nuestra funcion, es ordenar los argumentos recibidos en orden alfabetico de manera que nuestra funcion quedaria de la siguiente manera:
```typescript
interface SendEmailOptions {
    apiKey: string;
    body: string;
    email: string;
    from: string;
    subject: string;
}

function sendEmail({ apiKey, body, email, from, subject }: SendEmailOptions): boolean {}
```
#### Otras recomendaciones en funciones:
- La simplicidad es fundamental.
- Las funciones deben tener un tamaño reducido.
- Las funciones de una sola linea no deben causar complejidad excesiva.
- Su extencion en lineas de codigo debe ser de menos de 20 lineas de codigo
- Evitar el uso de `else` tanto como sea posible.
- Priorizar el uso de condiciones ternarias cuando aplique.

## Principio DRY (Don't Repeat Yourself)

"Si quieres ser un programado productivo esfuerzate en escribir codigo legible" - Robert C. Martin.

- Consiste en evitar tener duplicidad en el codigo.
- Simplificar la pruebas.
- Ayudar a centralizar los procesos.
- Aplicar el principio DRY, comunmente lleva a refactorizar codigo.

## Estructura de clases

**"El buen codigo parece estar escrito por alguien a quien le importa - Michael Feathers."**

Para explicarlo de mejor manera haremos un ejemplo para definir la clase `HtmlElement`.
```typescript
class HtmlElement { }
```

### Definir propiedades.

El orden en que se recomienda definir es el siguiente:

1. Propiedades estaticas.
2. Propiedades privadas, protegidas y publicas de ultimo

Ejemplo:

```typescript
class HtmlElement { 
    public static domReady: boolean = false;

    private _id: string;
    private type: string;
    private updatedAt: number;
 }
```

### Definir metodos.

El orden en que se recomiendadp definir es el siguiente:

1. Empezando por los constructores estaticos.
2. Definir el constructor.
3. Definir metodos estaticos.
4. Definir metodos privados.
5. Cualquier otro metodo y se deben ordenar de mayor a menor importancia.
6. Getters y Setters al final.

Ejemplo:

```typescript
class HtmlElement { 
    public static domReady: boolean = false;

    private _id: string;
    private type: string;
    private updatedAt: Date;

    static createInput( id: string) {
        return new HtmlElement(id, 'input')
    }

    constructor(id: string, type: string) {
        this._id = id;
        this.type = type;
        this.updatedAt = Date.now();
    }

    setType(type: string) {
        this.type = type;
        this.updatedAt = Date.now();
    }

    get id(): string {
        return this.id;
    }
 }
```

## Uso de comentarios.

**"No comentes el codigo mal escrito, reescribelo". -Brian W. Kernighan.**

Antes de agregar comentarios a tu codigo debes tener en cuenta las siguientes consideraciones:

- En general se debe evitar incluir comentarios en el codigo.
- El uso de comentarios debe ser la excepcion, no la regla.
- Algunas situaciones es cuando la solucion es bastante compleja o bien se esta ocupando algun "hack" que merece ser explicado, algunos de estos ejemplos son:
    - Al usar librerias de terceros.
    - Al consumir APIs.
    - Al hacer uso de ciertas funcionalidades de los frameworks.

## Uniformidad del proyecto

**"A problemas similares, soluciones similares"**

### Definicion de metodos:

Supongamos que estamos desarrollando un nuevo proyecto, y decidimos nombrar a nuestros metodos de nuestros controladores de la siguiente manera:

```typescript
const createProduct = () => { }
const updateProduct = () => { }
const deleteProduct = () => { }
```
Como podemos ver en el ejemplo anterior, nuestra definicion es bastante explicita y aunque no existe "Una forma correcta en estricta regla", una vez comenzamos un patron debemos continuarlo.

A continuacion, imaginando que estamos trabajando en el mismo proyecto mostraremos una forma incorrecta de nombrar los metodos de controlador ahora para la entidad `User`

```typescript
const createNewUser = () => { }
const modifyUser = () => { }
const removeUser = () => { }
```

En el ejemplo anterior aunque el codigo es descriptivo y funcionalmente es el adecuado, el problema es que no estamos siguiendo el mismo patron al nombrar nuestros metodos, una mejor manera de hacerlo es siguiendo la misma estructura del ejemplo de `Product` quedando de la siguiente manera:
```typescript
const createUser = () => { }
const updateUser = () => { }
const deleteUser = () => { }
```
**Ojo!** Se considero de esa manera ya que fue la primer propuesta que se trabajo, obviamente segun como se empiece a trabajar es el mismo estandar que deben se debe emplear en todos los metodos nuevos que surjan.

## Estructura de directorios

A continuacion se describe una estructura que pudiera parecer correcta pero no lo es, viendo la estructura de directorios los archivos correspondientes a `product-list` estan encarpetados, pero en el caso de `product-item.ts` no se aplico la misma logica

```bash
- proyecto-raiz/
  - src/
    - components/
        - product-list
            - product-list.html
            - product-list.ts
        - product-item.ts
```

Para corregir el punto anterior, basta con mover `product-item.ts` a una nueva carpeta llamada `product-item` y con eso ya estariamos siguiendo el estandar correcto de directorios.

Ejemplo:

```bash
- proyecto-raiz/
  - src/
    - components/
        - product-list
            - product-list.html
            - product-list.ts
        - product-item
            - product-item.ts
```

## Indentacion

Esto es muy a criterio de cada equipo de desarrolladores, pero debe haber un consenso de la indentacion ya sean tabulaciones o espacios, cada desarrollador debe de implementar la misma acordada por el equipo.

Esto a fin de que la legibilidad sea mejor, que el codigo se vea uniforme y que cuando varios desarrolladores modifiquen el mismo archivo no se cambie el formato.

La configuracion de indentacion puede ser configurandola en el editor directamente, o tambien se puede auxiliar de dependencias externas como linters que den el formato acordado al guardar el archivo.

## Aplicar principio de responsabilidad unica en clases

### Ejemplo restructuracion de herencia.

A continuacion se describe un ejemplo con varias clases que hace uso de herencia donde:
- La clase `Person` es una clase simple que no depende de ninguna otra.
- La clase `User` hereda las propiedades de `Person` y le agrega propiedades y metodos propios de la misma.
- La clase `UserSeattings` hereda de `User` por lo que a su vez cuenta con las propiedades de `Person`, llegados a este punto, la gestion de las clases se empieza a volver complicado.

```typescript
(() => {
    type Gender = 'M' | 'F'
    class Person {
        constructor(
            public name: string,
            public gender: Gender,
            public birthdate: Date
        ) {

        }
    }

    class User extends Person {
        private lastAccess: Date
        constructor(
            public email: string,
            public role: string,
            name: string,
            gender: Gender,
            birthdate: Date
        ) {
            super(name, gender, birthdate)
            this.lastAccess = new Date()
        }

        checkCredentials() {
            return true
        }
    }

    class UserSeattings extends User {
        constructor(
            public workingDirectory: string,
            public lastOpenFolder: string,
            email: string,
            role: string,
            name: string,
            gender: Gender,
            birthdate: Date
        ) {
            super(email, role, name, gender, birthdate)
        }
    }

    const userSeattings = new UserSeattings('/usr/root', '/usr/bin', 'fol@gmail.com', 'admon', 'Fernando Olmos', 'M', new Date('1996-02-18'))

    console.log(userSeattings);

})()
```

### Mejorando el uso de herencia.

Aunque el codigo anterior es correcto hay varios puntos que pueden darle una mejor legibilidad.

- Definir interfaces que indiquen las propiedades que puede recibir cada clase creamos `PersonProperties`, `UserProperties` y `UserSeattingsProperties`.

- Al tener la interfaz, podemos en lugar de mandar a llamar todas las propiedades, se manda a llamar una unica que desestructura las propiedades.

- Definir las propiedades publicas, protegidas y privadas antes del constructor

- Inicializar las propiedades en el constructor y en el metodo `super()` actualizar la implementacion al consumo de la propiedad desestructurada.
```typescript
(() => {
    type Gender = 'M' | 'F'

    interface PersonProperties {
        birthdate: Date;
        gender: Gender;
        name: string;
    }
    class Person {
        protected birthdate: Date;
        protected gender: Gender;
        protected name: string;
        constructor({ birthdate, gender, name }: PersonProperties
        ) {
            this.birthdate = birthdate
            this.gender = gender
            this.name = name
        }
    }
    const person = new Person({ birthdate: new Date('1996-02-18'), gender: "M", name: 'Fernando Olmos' })
    interface UserProperties {
        email: string;
        role: string;
        name: string;
        gender: Gender;
        birthdate: Date;
    }
    class User extends Person {
        protected lastAccess: Date
        protected email: string
        protected role: string
        constructor({
            email,
            role,
            name,
            gender,
            birthdate
        }: UserProperties) {
            super({ name, gender, birthdate })
            this.lastAccess = new Date()
            this.email = email
            this.role = role
        }

        checkCredentials() {
            return true
        }
    }
    interface UserSeattingsProperties {
        workingDirectory: string,
        lastOpenFolder: string,
        email: string,
        role: string,
        name: string,
        gender: Gender,
        birthdate: Date
    }
    class UserSeattings extends User {
        public workingDirectory: string
        public lastOpenFolder: string
        constructor({
            workingDirectory,
            lastOpenFolder,
            email,
            role,
            name,
            gender,
            birthdate
        }: UserSeattingsProperties) {
            super({ email, role, name, gender, birthdate })
            this.workingDirectory = workingDirectory
            this.lastOpenFolder = lastOpenFolder
        }
    }

    const userSeattings = new UserSeattings({
        workingDirectory: '/usr/root',
        lastOpenFolder: '/usr/bin',
        email: 'fol@gmail.com',
        role: 'admon',
        name: 'Fernando Olmos',
        gender: 'M',
        birthdate: new Date('1996-02-18')
    })

    console.log(userSeattings);


})()
```

## Priorizar la composicion sobre la herencia

El ejemplo anterior aunque es mas largo es mas entendible y tiene una mejor legibilidad, ahora bien en sistemas altamente cambiantes se recomienda en medida de lo posible usar `composicion` en lugar de `herencia`.

Partiendo de la misma base de codigo, haremos los cambios suficientes para eliminar la dependencia entre clases.

- Primero se deben eliminar todos los `extends` del codigo anterior en las clases de `User` y `UserSeattings` para eliminar la dependencia entre clases.

- Como ya cada clase es independiente, no necesitamos del metodo `super()` por lo que tambien lo retiramos de las clases

- Como te habras dado cuenta la clase `UserSeattings`, ya no depende de `User` por lo que la debemos renombrar a un nombre mas acorde a lo que hace, en este caso `Seattings`.

- Como ya no hay dependencia entre clases, eliminamos las propiedades que no corresponden a cada una dejando unicamente las que si pertenecen a la clase en cuestion.

- Finalmente, necesitamos una nueva clase que se encargue de orquestar todas nuestras clases a fin de que el funcionamiento por composicion sea el mismo que por herencia, para esto definimos la clase `UserSeattings` (Se llama igual que la que renombramos) y en esta clase recibimos todas nuestras `props` para finalmente en el constructor hacer la instanciacion de nuestras 3 clases pasandole sus respectivas propiedades, esto hace que ninguno de nuestros componentes sea dependiente, esten desacoplados y a la larga sea mas facil de escalar.

```typescript
(() => {
    type Gender = 'M' | 'F'

    interface PersonProperties {
        birthdate: Date;
        gender: Gender;
        name: string;
    }
    class Person {
        protected birthdate: Date;
        protected gender: Gender;
        protected name: string;
        constructor({ birthdate, gender, name }: PersonProperties
        ) {
            this.birthdate = birthdate
            this.gender = gender
            this.name = name
        }
    }
    const person = new Person({ birthdate: new Date('1996-02-18'), gender: "M", name: 'Fernando Olmos' })
    console.log({ person });
    interface UserProperties {
        email: string;
        role: string;
    }
    class User {
        protected lastAccess: Date
        protected email: string
        protected role: string
        constructor({
            email,
            role,
        }: UserProperties) {
            this.lastAccess = new Date()
            this.email = email
            this.role = role
        }

        checkCredentials() {
            return true
        }
    }
    interface SeattingsProperties {
        workingDirectory: string,
        lastOpenFolder: string,
    }
    class Seattings {
        public workingDirectory: string
        public lastOpenFolder: string
        constructor({
            workingDirectory,
            lastOpenFolder,
        }: SeattingsProperties) {
            this.workingDirectory = workingDirectory
            this.lastOpenFolder = lastOpenFolder
        }
    }

    interface UserSeattingsProperties {
        workingDirectory: string,
        lastOpenFolder: string,
        email: string,
        role: string,
        name: string,
        gender: Gender,
        birthdate: Date
    }

    class UserSeattings {
        protected person: Person
        protected user: User
        protected seattings: Seattings
        constructor({
            workingDirectory,
            lastOpenFolder,
            email,
            role,
            name,
            gender,
            birthdate
        }: UserSeattingsProperties){
            this.person = new Person({ birthdate, gender, name})
            this.user = new User({ email, role})
            this.seattings = new Seattings({ workingDirectory, lastOpenFolder})
        }
    }

    const userSeattings = new UserSeattings({
        workingDirectory: '/usr/root',
        lastOpenFolder: '/usr/bin',
        email: 'fol@gmail.com',
        role: 'admon',
        name: 'Fernando Olmos',
        gender: 'M',
        birthdate: new Date('1996-02-18')
    })

    console.log(userSeattings);
})()


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