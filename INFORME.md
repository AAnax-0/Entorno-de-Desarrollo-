# Punto 1. Conceptos básicos del ciclo de vida del código

## 1. Conceptos básicos

Para comprender el ciclo de vida del código, es necesario distinguir tres conceptos: código fuente, código objeto y código ejecutable.

### Código fuente

Es el texto que escribe un programador utilizando las reglas y la sintaxis de un lenguaje de programación específico. En este curso aprenderé Java.

### Código objeto

Es el resultado de traducir el código fuente a una representación de bajo nivel. En Java, el compilador genera *bytecode*, que se guarda en archivos `.class` y puede ejecutarse en una Máquina Virtual de Java (JVM).

### Código ejecutable

Es el código que puede ejecutar el procesador. En Java, la JVM carga el bytecode y lo interpreta o lo compila a código máquina durante la ejecución.

## 2. Fases de compilación y ejecución

Para ilustrar el proceso, se utilizará el siguiente ejemplo:

```java
public class HolaMundo {
    public static void main(String[] args) {
        String mensaje = "Hola, mundo!";
        System.out.println(mensaje);
    }
}
```

### Recorrido general

El proceso desde `HolaMundo.java` hasta la ejecución en el procesador se divide en dos etapas:

1. **Compilación (`javac`):** convierte el código fuente `.java` en bytecode, que se almacena en un archivo `.class`.
2. **Ejecución (`java` / JVM):** carga el bytecode, lo interpreta o lo compila a código máquina para que pueda ejecutarlo el procesador.

### Etapas del proceso

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
# Punto 2. Clasificación de lenguajes de programación

Los lenguajes de programación se pueden clasificar de dos formas: según su nivel de abstracción —alto, medio o bajo, dependiendo de cuánto se alejan del lenguaje máquina— y según su paradigma de programación, que describe cómo se estructura y desarrolla un programa.

## 1. Según el nivel de abstracción

### 1.1. Lenguajes de alto nivel

Son lenguajes que utilizan instrucciones y estructuras fáciles de comprender para las personas y ocultan gran parte de los detalles del hardware. Dentro de este nivel podemos encontrar lenguajes con diferentes paradigmas.

- **Java:** es un lenguaje de alto nivel. Utiliza instrucciones, variables, condiciones y bucles para indicar paso a paso cómo debe realizarse una tarea. Además, permite trabajar sin tener que gestionar directamente la memoria.
- **Python:** es un lenguaje de alto nivel. Tiene una sintaxis sencilla y permite desarrollar programas sin necesidad de conocer los detalles internos del procesador.

### 1.2. Lenguajes de nivel medio

Son un punto intermedio entre los lenguajes de alto y bajo nivel, ya que combinan características de ambos. Permiten utilizar estructuras de alto nivel, pero también proporcionan un mayor control sobre la memoria y los recursos del sistema.

- **C:** es un lenguaje de nivel medio. Permite utilizar estructuras como condiciones, bucles y funciones, pero también manipular direcciones de memoria mediante punteros.
- **C++:** es un lenguaje de nivel medio. Permite utilizar características de alto nivel, como las clases y los objetos, pero también trabajar directamente con la memoria y los recursos del sistema mediante elementos como los punteros.

### 1.3. Lenguajes de bajo nivel

Son lenguajes muy próximos al lenguaje máquina y permiten controlar de forma muy directa el funcionamiento del procesador y otros componentes del hardware.

- **Ensamblador x86:** es un lenguaje de bajo nivel e imperativo, ya que utiliza instrucciones que indican directamente al procesador qué operaciones debe realizar, como `MOV` o `ADD`.
- **Ensamblador ARM:** también es un lenguaje de bajo nivel e imperativo, ya que utiliza instrucciones específicas de los procesadores ARM para realizar operaciones directamente sobre el hardware.

Estos lenguajes necesitan un traductor que convierte las instrucciones escritas en ensamblador en instrucciones que el procesador pueda ejecutar.

## 2. Clasificación según el paradigma de programación

Aunque anteriormente hemos indicado el paradigma de algunos ejemplos, también podemos clasificarlos de forma general en dos grupos:

### 2.1. Lenguajes imperativos

Los lenguajes imperativos dicen cómo realizar una tarea mediante una serie de instrucciones que se ejecutan siguiendo un orden y que pueden modificar el estado del programa.

**Ejemplos:**

- **C:** utiliza instrucciones secuenciales, variables, condiciones y bucles para indicar paso a paso cómo resolver un problema.
- **Java:** Define una secuencia de instrucciones, utiliza condiciones y bucles y modifica variables para conseguir un resultado.

Por ejemplo, para sumar dos números, podemos indicar al programa que guarde los valores, realice la suma y después muestre el resultado.

### 2.2. Lenguajes declarativos

Los lenguajes declarativos dicen que resultado se quiere obtener, sin tener que especificar todos los pasos que debe seguir el sistema para conseguirlo.

**Ejemplos:**

- **SQL:** Solicita determinados datos de una base de datos mediante consultas, indicando qué información queremos obtener, sin tener que especificar cómo debe localizarla físicamente el sistema.
- **Prolog:** Expresa hechos y reglas lógicas para que el sistema encuentre soluciones a una consulta.
