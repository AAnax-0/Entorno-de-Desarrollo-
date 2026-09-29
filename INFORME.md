# Ciclo de vida y paradigmas de programación

## Índice

1. [Punto 1. Ciclo de vida del código](#punto-1)
    - [Conceptos básicos](#p1-conceptos)
    - [Fases de compilación y ejecución](#p1-fases)
2. [Punto 2. Clasificación de los lenguajes](#punto-2)
    - [Nivel de abstracción](#p2-nivel)
    - [Paradigmas de programación](#p2-paradigmas)
3. [Punto 3. Identificación de paradigmas](#punto-3)
    - [Análisis de los fragmentos](#punto-3-fragmentos)
4. [Punto 4. Enfoque imperativo y declarativo](#punto-4)
    - [Forma imperativa](#p4-imperativa)
    - [Forma declarativa](#p4-declarativa)
    - [Comparación](#p4-comparacion)
    - [Conclusión](#p4-conclusion)

<a id="punto-1"></a>
## 🔄 Punto 1. Conceptos básicos del ciclo de vida del código

<a id="p1-conceptos"></a>
### Conceptos básicos

Para comprender el ciclo de vida del código, es necesario distinguir tres conceptos: código fuente, código objeto y código ejecutable.

#### Código fuente

Es el texto que escribe un programador utilizando las reglas y la sintaxis de un lenguaje de programación específico. En este curso aprenderé Java.

#### Código objeto

Es el resultado de traducir el código fuente a una representación de bajo nivel. En Java, el compilador genera *bytecode*, que se guarda en archivos `.class` y puede ejecutarse en una Máquina Virtual de Java (JVM).

#### Código ejecutable

Es el código que puede ejecutar el procesador. En Java, la JVM carga el bytecode y lo interpreta o lo compila a código máquina durante la ejecución.

<a id="p1-fases"></a>
### Fases de compilación y ejecución

Para ilustrar el proceso, se utilizará el siguiente ejemplo:

```java
public class HolaMundo {
    public static void main(String[] args) {
        String mensaje = "Hola, mundo!";
        System.out.println(mensaje);
    }
}
```

**Recorrido general.**

El proceso desde `HolaMundo.java` hasta la ejecución en el procesador se divide en dos etapas:

1. **Compilación (`javac`):** convierte el código fuente `.java` en bytecode, que se almacena en un archivo `.class`.
2. **Ejecución (`java` / JVM):** carga el bytecode, lo interpreta o lo compila a código máquina para que pueda ejecutarlo el procesador.

**Etapas del proceso:**

#### 1. Análisis léxico (*Lexer*)

El compilador de Java (`javac`) lee `HolaMundo.java` carácter por carácter y lo descompone en *tokens*, como palabras clave, identificadores y símbolos.

En el ejemplo, identifica:

- **Palabras reservadas:** `public`, `class`, `static`, `void`.
- **Identificadores:** `HolaMundo`, `main`, `mensaje`.
- **Símbolos y puntuación:** `{`, `}`, `(`, `)`, `;`.
- **Literal de texto:** `"Hola, mundo!"`.

#### 2. Análisis sintáctico (*Parser*)

Comprueba que los *tokens* respeten la gramática y la estructura formal de Java, y genera un Árbol de Sintaxis Abstracta (AST).

En el ejemplo, comprueba que:

- La clase `HolaMundo` tenga un bloque delimitado por `{}`.
- La declaración `String mensaje = "Hola, mundo!";` siga la estructura `<Tipo> <Nombre> = <Valor>;`.

Si faltara el paréntesis de cierre en `System.out.println(mensaje;`, esta fase detectaría un error de sintaxis.

#### 3. Análisis semántico

Comprueba el significado del código: revisa los tipos de datos, el ámbito (*scope*) de las variables y que los métodos invocados existan.

En el ejemplo, comprueba que:

- El tipo `String` sea compatible con el valor asignado, `"Hola, mundo!"`.
- La variable `mensaje` esté declarada antes de utilizarse como argumento de `System.out.println()`.
- El método `println` sea accesible y acepte un parámetro de tipo `String`.

#### 4. Generación de código intermedio

`javac` traduce la estructura analizada a una representación independiente de la arquitectura física. En Java, esta representación se llama *bytecode* y se guarda en `HolaMundo.class`.

Por ejemplo, la instrucción `String mensaje = "Hola, mundo!";` puede traducirse a instrucciones de *bytecode* como `ldc` (cargar una constante desde el *constant pool*) y `astore_1` (guardar una referencia en la variable local 1).

#### 5. Optimización de código

La optimización puede aplicarse durante la compilación a *bytecode* y durante la ejecución dentro de la JVM. Su objetivo es mejorar el rendimiento sin modificar el resultado.

Por ejemplo, si se escribiera `"Hola, " + "mundo!"`, el compilador podría concatenar las constantes durante la compilación, evitando esa operación en tiempo de ejecución. Además, el compilador JIT (*Just-In-Time*) de la JVM puede detectar fragmentos de *bytecode* que se ejecutan con frecuencia y optimizarlos sobre la marcha.

#### 6. Generación de código final y ejecución

La JVM carga el *bytecode* `.class`, resuelve las clases y recursos necesarios (como `java.lang.System`) y lo interpreta o lo compila a instrucciones de máquina —por ejemplo, para arquitecturas x86 o ARM— que puede ejecutar el procesador.

En el ejemplo, este proceso permite que se muestre `Hola, mundo!` en la consola.

<a id="punto-2"></a>
## 🧭 Punto 2. Clasificación de lenguajes de programación

Los lenguajes de programación se pueden clasificar de dos formas: según su nivel de abstracción —alto, medio o bajo, dependiendo de cuánto se alejan del lenguaje máquina— y según su paradigma de programación, que describe cómo se estructura y desarrolla un programa.

<a id="p2-nivel"></a>
### 1. Según el nivel de abstracción

#### 1.1. Lenguajes de alto nivel

Son lenguajes que utilizan instrucciones y estructuras fáciles de comprender para las personas y ocultan gran parte de los detalles del hardware. Dentro de este nivel podemos encontrar lenguajes con diferentes paradigmas.

- **Java:** es un lenguaje de alto nivel. Utiliza instrucciones, variables, condiciones y bucles para indicar paso a paso cómo debe realizarse una tarea. Además, permite trabajar sin tener que gestionar directamente la memoria.
- **Python:** es un lenguaje de alto nivel. Tiene una sintaxis sencilla y permite desarrollar programas sin necesidad de conocer los detalles internos del procesador.

#### 1.2. Lenguajes de nivel medio

Son un punto intermedio entre los lenguajes de alto y bajo nivel, ya que combinan características de ambos. Permiten utilizar estructuras de alto nivel, pero también proporcionan un mayor control sobre la memoria y los recursos del sistema.

- **C:** es un lenguaje de nivel medio. Permite utilizar estructuras como condiciones, bucles y funciones, pero también manipular direcciones de memoria mediante punteros.
- **C++:** es un lenguaje de nivel medio. Permite utilizar características de alto nivel, como las clases y los objetos, pero también trabajar directamente con la memoria y los recursos del sistema mediante elementos como los punteros.

#### 1.3. Lenguajes de bajo nivel

Son lenguajes muy próximos al lenguaje máquina y permiten controlar de forma muy directa el funcionamiento del procesador y otros componentes del hardware.

- **Ensamblador x86:** es un lenguaje de bajo nivel e imperativo, ya que utiliza instrucciones que indican directamente al procesador qué operaciones debe realizar, como `MOV` o `ADD`.
- **Ensamblador ARM:** también es un lenguaje de bajo nivel e imperativo, ya que utiliza instrucciones específicas de los procesadores ARM para realizar operaciones directamente sobre el hardware.

Estos lenguajes necesitan un traductor que convierte las instrucciones escritas en ensamblador en instrucciones que el procesador pueda ejecutar.

<a id="p2-paradigmas"></a>
### 2. Clasificación según el paradigma de programación

Aunque anteriormente hemos indicado el paradigma de algunos ejemplos, también podemos clasificarlos de forma general en dos grupos:

#### 2.1. Lenguajes imperativos

Los lenguajes imperativos dicen cómo realizar una tarea mediante una serie de instrucciones que se ejecutan siguiendo un orden y que pueden modificar el estado del programa.

**Ejemplos:**

- **C:** utiliza instrucciones secuenciales, variables, condiciones y bucles para indicar paso a paso cómo resolver un problema.
- **Java:** define una secuencia de instrucciones, utiliza condiciones y bucles y modifica variables para conseguir un resultado.

Por ejemplo, para sumar dos números, podemos indicar al programa que guarde los valores, realice la suma y después muestre el resultado.

#### 2.2. Lenguajes declarativos

Los lenguajes declarativos indican qué resultado se quiere obtener, sin tener que especificar todos los pasos que debe seguir el sistema para conseguirlo.

**Ejemplos:**

- **SQL:** permite solicitar determinados datos de una base de datos mediante consultas, indicando qué información queremos obtener, sin tener que especificar cómo debe localizarla físicamente el sistema.
- **Prolog:** permite expresar hechos y reglas lógicas para que el sistema encuentre soluciones a una consulta.

<a id="punto-3"></a>
## 🧪 Punto 3. Actividad práctica: identificación de paradigmas

<a id="punto-3-fragmentos"></a>
### Análisis de los fragmentos

En cada fragmento se puede reconocer el paradigma utilizado según se describan los pasos para alcanzar un resultado o se indique directamente el resultado esperado.

1. **Fragmento 1 — Imperativo:** se asocia con este paradigma porque hay que seguir una serie de instrucciones que describen cómo realizar la suma paso a paso para llegar al resultado.
2. **Fragmento 2 — Declarativo:** indica el resultado —el nombre de los trabajadores mayores de 30 años— sin detallar el proceso necesario para obtenerlo.
3. **Fragmento 3 — Declarativo:** presenta el resultado sin explicar los pasos del proceso.
4. **Fragmento 4 — Imperativo:** describe detalladamente el proceso para obtener los precios superiores a 10 dólares.








<a id="punto-4"></a>
## ☕ Punto 4. Actividad: enfoque imperativo frente al declarativo

Para esta actividad he elegido una acción cotidiana: preparar un café latte (sí, me gusta el latte). A continuación, describo la receta desde los enfoques imperativo y declarativo, comparo sus ventajas e inconvenientes y expongo una conclusión.

<a id="p4-imperativa"></a>
### A. Forma imperativa

En la forma imperativa se indican todos los pasos necesarios para preparar el café y el orden en el que hay que realizarlos.

1. Coger 18 g de café soluble y echarlo en una batidora.
2. Añadir 150 g de hielo, 60 g de azúcar moreno y 80 ml de agua.
3. Batir todos los ingredientes hasta que se forme una crema con una textura parecida a una mousse.
4. Coger un vaso y añadir varios hielos.
5. Añadir leche hasta que cubra un poco más de la mitad del vaso.
6. Colocar un pegote de la crema de café sobre la leche.
7. Añadir una cañita al vaso.
8. Remover el contenido del vaso para mezclar la crema con la leche.
9. Una vez mezclado, el café latte está listo para beber.

En este caso se indica cómo preparar el café, explicando cada acción y el orden en el que se debe realizar.

<a id="p4-declarativa"></a>
### B. Forma declarativa

En la forma declarativa no indicamos los pasos que hay que seguir, sino únicamente el resultado final que queremos conseguir.

> **Resultado deseado:** un café latte frío en un vaso, con hielo y leche cubriendo un poco más de la mitad del recipiente, acompañado de una crema de café hecha con café soluble, hielo, azúcar moreno y agua, con una textura similar a una mousse. El café debe estar listo para remover y beber con una cañita.

En este caso no se explica cómo conseguir ese resultado ni qué acciones deben realizarse. Solamente se indica cómo se quiere que sea el café terminado.

<a id="p4-comparacion"></a>
### C. Comparación entre los dos enfoques

La diferencia principal entre ambos enfoques es que el imperativo indica cómo realizar una tarea, mientras que el declarativo indica qué resultado queremos obtener.

#### Ventajas del enfoque imperativo

- Permite saber exactamente qué hacer y en qué orden.
- Facilita que otra persona pueda repetir la receta siguiendo los mismos pasos.
- Proporciona un mayor control sobre todo el proceso.

#### Desventajas del enfoque imperativo

- La explicación es más larga porque hay que describir todos los pasos.
- Hay que especificar muchos detalles para que el procedimiento se realice correctamente.
- Si se quiere cambiar la forma de preparar el café, habría que modificar los pasos.

#### Ventajas del enfoque declarativo

- La explicación es más sencilla y se centra en el resultado final.
- No es necesario explicar todos los pasos del proceso.
- Permite utilizar diferentes métodos para conseguir un resultado similar.

#### Desventajas del enfoque declarativo

- No explica cómo se debe preparar el café.
- Puede ser difícil conseguir exactamente el resultado deseado si no se conoce el procedimiento.
- La persona que recibe la indicación tiene que decidir por sí misma cómo conseguir el resultado.

<a id="p4-conclusion"></a>
### D. Conclusión

En mi caso, preparar el café latte de forma imperativa consiste en explicar paso a paso cómo preparo la crema, cómo preparo el vaso con hielo y leche y cómo termino el café.

En cambio, de forma declarativa, simplemente especifico cómo quiero que sea el café terminado, sin explicar las acciones necesarias para prepararlo.

- **Imperativo:** «Haz estos pasos para preparar mi café latte».
- **Declarativo:** «Quiero obtener este café latte como resultado final».
