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