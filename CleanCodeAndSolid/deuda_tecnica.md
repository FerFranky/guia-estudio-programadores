# Entendiendo el concepto de Deuda Técnica

## Definición
La **deuda técnica** es la falta de calidad en el código, que repercutirá en costos futuros. No se refiere solo al código, sino también a la ausencia de documentación, pruebas, o refactorización. Es importante ser consciente de que, de una forma u otra, esta deuda tendrá que ser "pagada" en el futuro.

## Costos Económicos de la Deuda Técnica
Los principales costos derivados de la deuda técnica incluyen:
- **Tiempo en realizar mantenimientos**: Mayor complejidad para implementar cambios.
- **Tiempo en refactorizar el código**: Esfuerzo adicional para limpiar o reestructurar el código.
- **Tiempo en entender el código**: Dificultad para que otros desarrolladores comprendan el código existente.
- **Tiempo adicional en la transferencia del código**: Complejidad adicional al compartir el conocimiento y colaborar en el código.

## Esquema de Deuda Técnica de Martin Fowler

Fowler define la deuda técnica en función de su origen y su impacto:

### 1. Intencionada
Se genera de manera consciente, cuando el equipo de desarrollo toma decisiones rápidas para cumplir plazos. Ejemplo: copiar y pegar código sin detenerse en optimizarlo. Aunque puede ser útil a corto plazo, tiende a generar proyectos de baja calidad y poca tolerancia al cambio.

### 2. Inadvertida
Es el tipo de deuda técnica que surge por desconocimiento o falta de experiencia. No se toma conscientemente, pero se acumula debido a prácticas ineficientes o errores que pasan desapercibidos.

### 3. Prudente
Aquí se es consciente de la deuda técnica y se la tolera porque se considera manejable. Sin embargo, el costo aumentará con el tiempo si no se paga.

### 4. Prudente Inadvertida
Este tipo de deuda se hace evidente solo cuando el proyecto ha avanzado considerablemente. En este punto, se enfrenta la decisión de continuar o reescribir partes del proyecto.

## Gestión de la Deuda Técnica

La deuda técnica es normal y, en general, inevitable en el desarrollo de software. Sin embargo, su gestión es fundamental para minimizar sus efectos a largo plazo. 

### Pagando la Deuda Técnica
El pago de la deuda técnica se realiza a través de la **refactorización** del código, y para hacerlo de manera segura, es esencial contar con **pruebas automáticas**. Sin pruebas automáticas, es difícil asegurar que el código refactorizado cumple con los criterios esperados, lo que aumenta los riesgos, especia

[Volver al índice](../README.md)  # Enlace para volver al índice

---

<p align="center">
  <samp>Hecho con código, café ☕ y determinación 💻</samp><br>
  <samp>Desarrollado por <a href="https://github.com/FerFranky">[Fernando Olmos]</a> 🚀</samp><br>
  <samp><i>// Siempre en constante evolución // 🔧</i></samp><br>
  <samp><i>if(works) { don't_touch_it(); }</i></samp>
</p>

---