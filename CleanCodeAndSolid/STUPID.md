# Acronimo STUPID

**Code Smells:** Son todas las malas practicas, anti patrones de diseño que existen en nuestro codigo.
Traducido de ingles "Algo que huele mal", podria definirse como todas aquellas funcionalidades que resuelven su objetivo, pero sabemos que su implementacion no es del todo correcta.

**STUPID** se refiere a toda la deuda tecnica que nosotros podemos acumular en nuestro proyecto y va directamente relacionado a los **Code Smells**.

Significado de **STUPID** por sus siglas:

- **S**ingleton: Implementacion del patron singleton.
- **T**ight Coupling: Alto acoplamiento.
- **U**ntestability: Codigo no probable (Unit Test).
- **P**remure optimization: Optimizaciones prematuras
- **I**ndescriptive Naming: Nombres poco descriptivos.
- **D**uplication: Duplicidad de codigo, es decir no aplicar el principio `DRY`.

A continuacion describiremos cada uno de estos puntos:

### Singleton (S):

- Pros:
    - Garantiza una unica instancia de clase a lo largo de toda la aplicacion.
- Contras:
    - Vive en un contexto global.
    - Puede ser modificado por cualquiera y en cualquier momento.
    - No es rastreable.
    - Dificil de testear debido a su ubicacion

### Alto aclopamiento.
**"Queremos diseñar componentes que sean auto contenidos, auto suficientes e independientes. Con un objetivo y un proposito bien definido". - The pragmatic Programmer.**

Lo ideal en cualquier proyecto de software es tener un bajo acoplamiento y una buena cohesion.

#### Desventajas del alto acoplamiento:
- Un cambio en un modulo por lo general provoca un efecto domino de cambios en otros modulos.
- El ensamblaje de modulos puede requerir mas esfuerzo y tiempo debido a la dependencia existente entre modulos.
- Un modulo en particular puede ser mas dificil de reutilizar y de probar ya que requiere incluir modulos dependientes.

#### Soluciones al alto acoplamiento.
- **"A"** tiene un atributo que se refiere a **"B"**.
- **"A"** llama a los servicios de un objeto **"B"**.
- **"A"** tiene un metodo que hace referencia a **"B"** (a traves del tipo de retorno o parametro).
- **"A"** es una subclase de (o implementa) la clase **"B"**.

#### Cohesion
**La cohesion se refiere a lo que la clase (o modulo) puede hacer.**
- La baja cohesion significaria que la clase realiza una gran variedad de acciones: es amplia, no se enfoca en lo que debe hacer.
- Alta cohesion significa que la clase se enfoca en lo que deberia estar haciendo, es decir, solo metodos relacionados con la intencion de la clase.

#### Acoplamiento.

**Se refiere a cuan relacionadas o dependientes son dos clases o modulos entre si.**

- **En bajo acoplamiento,** cambiar algo importante en una clase no deberia afectar a la otra.
- **En alto acoplamiento,** dificultaria el cambio y el mantenimiento de su codigo; dado que las clases esta muy unidas, hacer un cambio podria requerir una renovacion completa del sistema.

**Un buen diseño de software tiene alta cohesion y bajo acoplamiento.**

### Codigo no probable.
- Codigo dificilmente testeable.
- Codigo con alto acoplamiento.
- Codigo con muchas dependencias no inyectadas.
- Dependencias en el contexto global (Tipo Singleton).

**Debemos tener en mente las pruebas desde la creacion de codigo.**

### Optimizaciones prematuras.

Mantener abiertas las opciones retraseando la toma de deciociones nos permite darle mayor relevancia a lo que es mas importante en una aplicacion.

No debemos anticiparnos a los requisitos y desarrollar abstracciones innecesarias que puedan agregar complejidad accidental.

Se debe considerar:

- **Complejidad escencial:** La complegidad que es inherente al problema.
- **Complejidad accidental:** Cuando implementamos una solucion compleja a la minima indispensable.

Recuerda que debe haber un balance entre la complejidade escencial y la complejidad accidental.

### Nombres poco descriptivos.

- Nombres de variables mal nombradas.
- Nombres de clases genericas.
- Nombres de funciones mal nombradas.
- Ser muy especifico o demasiado generico.

### Duplicidad de codigo

No aplicar el principio **DRY**.

#### Duplicidad real:

- El codigo es identico y cumple la misma funcion.
- Un cambio implicaria actualizar todo el codigo identico en varios lugares.
- Incrementa posibilidades de error humano al olvidar una parte para actualizar.
- Mayor cantidad de pruebas innecesarias.

#### Duplicidad accidental:

- El codigo luce similar pero cumple funciones distintas.
- Cuando hay un cambio, solo hay que modigicar un solo lugar.
- Este tipo de duplicidad se puede trabajar con parametros u optimizaciones.

### Otros Code Smells.

#### Inflacion:
Cuando un metodo tiene demasiadas lineas de codigo (mas de 10 se debe analizar).

Se debe buscar hacer mas pequenio ese metodo a traves de submetodos.

Otro caso es cuando las clases son muy largas. Cuando una clase hace muchas cosas seria bueno separarlo en subclases o submodulos evitando la duplicidad de codigo y haciendo que cada clase se encargue de una tarea especifica.

#### Obsesion primitiva:

Crear un exceso de datos primitivos para hacer validaciones o asignar valores,uso de muchas banderas, mismas que en dado caso pueden agruparse en la misma estructura o reemplazarse por clases o metodos que resuelvan lo mismo.

#### Lista larga de parametros:

Se da al tener mas de 3 parametros en un metodo.

Pueden ser producto de sobre esfuerzos de hacerlos que tengan demasiada funcionalidad.

Se puede reemplazar enviando un solo objeto de parametros en lugar de recibir multiples parametros en el mismo.

### Acopladores
#### Feature Envy
 Como resultado, el método en cuestión se acopla estrechamente a la otra clase, lo que dificulta el cambio o el mantenimiento de cualquiera de las clases de forma independiente.

Algunos indicadores comunes de Feature Envy incluyen:

- Un método que accede o manipula datos o comportamientos de otra clase con más frecuencia que el suyo.
- Un método que realiza tareas que no son su responsabilidad principal, sino que pertenecen a otra clase.
- Un método que contiene lógica compleja que es más adecuado para otra clase.

Característica Envy puede conducir a varios problemas, tales como:

Acoplamiento estrecho entre clases, lo que dificulta el cambio o mantenimiento de cualquiera de las clases de forma independiente.
- Encapsulación reducida, ya que los detalles internos de una clase se exponen a otra.
Mayor complejidad y dificultad para entender el código.
- Reducción de la reutilización del código, ya que el método en cuestión no se centra en sus propias responsabilidades.

Para abordar Feature Envy, los desarrolladores pueden aplicar técnicas de refactorización, tales como:

- Extraer métodos o comportamientos en sus propias clases, permitiendo que cada clase se centre en sus propias responsabilidades.
- Mover métodos o comportamientos de una clase a otra, donde pertenecen.
Reducir el acoplamiento entre clases mediante la introducción de interfaces o clases abstractas.

Al reconocer y abordar Feature Envy, los desarrolladores pueden mejorar el diseño general y la capacidad de mantenimiento de sus sistemas de software.

#### Intimidad inapropiada

En programación, el término "intimidad inapropiada" se refiere a una situación en la que una clase o módulo accede a detalles internos de otra clase o módulo de una manera que viola los principios de encapsulamiento y diseño limpio. Esto puede hacer que el código sea frágil, difícil de mantener y propenso a errores cuando se realizan cambios.

#### Encadenamiendo de mensajes

Ocurre cuando los metodos dependen bastante uno de otro ejemplo A llama a B y B para contestar a B llama a C y asi sucesivamente.

#### The Middle Man

Cuando una clase existe solo para delegar la funcionalidad a otra clase. Se debe tratar de evitar este punto intermedio.

[Volver al índice](../README.md)  # Enlace para volver al índice

---

<p align="center">
  <samp>Hecho con código, café ☕ y determinación 💻</samp><br>
  <samp>Desarrollado por <a href="https://github.com/FerFranky">[Fernando Olmos]</a> 🚀</samp><br>
  <samp><i>// Siempre en constante evolución // 🔧</i></samp><br>
  <samp><i>if(works) { don't_touch_it(); }</i></samp>
</p>

---