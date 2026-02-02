<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### En POO suelen señalarse cuatro pilares: abstracción, encapsulamiento, herencia y polimorfismo. La abstracción consiste en modelar entidades del problema resaltando lo esencial y ocultando detalles irrelevantes; por ejemplo, un Punto abstrae sus coordenadas y ofrece operaciones como calcular distancia, sin exponer cómo se implementa internamente. Esta idea es similar a declarar una interfaz de funciones en C, separando qué hace de cómo lo hace.
### El encapsulamiento implica ocultar el estado interno (atributos) detrás de una interfaz pública (métodos). En C se intentaría con static a nivel de módulo y funciones “getter/setter”; en Java es nativo con modificadores de acceso (private, public) y métodos. La herencia permite crear nuevas clases reutilizando y extendiendo el comportamiento de otras (una Figura base, y Circulo, Rectangulo derivadas). El polimorfismo permite tratar objetos de tipos concretos distintos a través de un tipo común y que el comportamiento correcto se resuelva dinámicamente (similar a tablas de función o punteros a función en C, pero integrado en el lenguaje).



## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Entre los lenguajes más populares con soporte POO se encuentran Java, C++, C# y Python. Todos permiten definir tipos (clases) con atributos y métodos, así como usar herencia y polimorfismo, si bien con matices en sintaxis y filosofía.
### C++ ofrece POO con control muy fino de memoria; Java prioriza la portabilidad y seguridad con recolección de basura; C# combina características modernas de .NET; Python tiene un modelo de objetos muy flexible y dinámico. Otros lenguajes populares con POO incluyen Ruby, Swift y Kotlin.



## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### La programación estructurada promueve organizar el flujo de control con estructuras como secuencia, selección (if, switch) e iteración (for, while), evitando saltos incontrolados como goto. El objetivo es mejorar claridad, mantenibilidad y verificabilidad del código. Lenguajes como C apoyan firmemente este enfoque.
### La programación modular divide el programa en módulos cohesionados y con interfaces bien definidas, facilitando reutilización y desarrollo independiente. En C, esto se ve con ficheros .h que exponen la API y .c que implementan; se ocultan detalles internos a través del enlazado y la visibilidad (static). La POO hereda estas ideas y añade modelos de datos+comportamiento (clases) y polimorfismo.



## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Clásicamente, un objeto se caracteriza por estado, comportamiento e identidad. El estado son los datos almacenados en sus atributos (por ejemplo, x e y en un Punto). El comportamiento son las operaciones que puede realizar, definidas por sus métodos (como calcular distancias).
### La identidad distingue a un objeto de otro, aunque su estado sea igual. En Java, dos objetos con idénticos valores pueden ser distintos si son instancias diferentes (referencias distintas). Esta noción es esencial para entender la semántica de referencias, igualdad (equals) y hashing (hashCode).


## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Una clase es el plano (plantilla) que define la estructura (atributos) y el comportamiento (métodos) de un conjunto de objetos. Un objeto es un ejemplar concreto creado a partir de esa clase, con su propio estado en memoria. Por tanto, no son lo mismo: la clase es el tipo; el objeto es el valor vivo con identidad.
### Una instancia es precisamente un objeto creado de una clase, típicamente con new en Java. Aunque la mayoría de lenguajes OO usan clases, existen sistemas basados en prototipos (por ejemplo, JavaScript clásico), donde los objetos se clonan de otros objetos sin clases formales. De ahí que no todos los lenguajes OO requieran el concepto de clase.




## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### En Java, los objetos se almacenan en el heap y se accede a ellos por referencia; las variables locales que apuntan a objetos (referencias) residen en la pila de ejecución (stack), pero el contenido del objeto vive en el heap. En C++, puede elegirse: pila (automáticos), heap (new/delete), estática; la estrategia afecta ciclo de vida y coste.
### La recolección de basura (garbage collection) es un mecanismo automático que libera memoria que ya no es accesible por el programa, evitando fugas. Java y C# lo incorporan; C y C++ no (aunque C++ moderno puede usar smart pointers para aproximarlo). No es idéntico en todos los lenguajes: varía la estrategia del recolector, la temporización y el coste en rendimiento.



## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Un método es una función asociada a una clase/objeto, que puede leer/modificar su estado y define parte de su comportamiento. En términos de C, sería similar a una función que recibe explícitamente un puntero a la estructura como primer parámetro, pero en Java se hace de forma implícita mediante la referencia del objeto.
### La sobrecarga de métodos permite definir varios métodos con el mismo nombre pero distintas firmas (número o tipos de parámetros). El compilador elige cuál invocar en tiempo de compilación según los argumentos. Esto difiere del polimorfismo por herencia (despacho dinámico), que resuelve en tiempo de ejecución.



## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### A continuación se muestra una clase Punto sencilla en Java. Los atributos tienen visibilidad por defecto (package-private). El método calculaDistanciaAOrigen usa la fórmula de distancia euclídea.
// Punto.java
class Punto {
	double x; // visibilidad por defecto
	double y; // visibilidad por defecto

	double calculaDistanciaAOrigen() {
    	return Math.sqrt(x * x + y * y);
	}
}

// Ejemplo de uso:
class Demo {
	public static void main(String[] args) {
    	Punto p = new Punto();
    	p.x = 3.0;
    	p.y = 4.0;
    	double d = p.calculaDistanciaAOrigen(); // debería ser 5.0
    	System.out.println("Distancia al origen: " + d);
	}
}



## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### El punto de entrada en Java es el método public static void main(String[] args), que el lanzador de la JVM busca en la clase especificada al ejecutar java. Debe ser public (para que la JVM pueda invocarlo), static (porque se llama sin crear instancia) y void (no retorna valor al lanzador). El parámetro String[] args recibe argumentos de línea de comandos.
### La palabra clave static indica que el miembro pertenece a la clase y no a instancias concretas (similar a miembros globales o estáticos en C). Se usa en campos y métodos (por ejemplo, Math.sqrt es un método estático). No es exclusivo de main. Combinado con final en un campo suele crear constantes (por convención static final y mayúsculas): static final double PI = 3.141592653589793.


## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Para compilar desde línea de comandos se utiliza javac y para ejecutar java. Dado el ejemplo del punto 8, si están en el mismo directorio y el fichero Demo.java contiene ambas clases (o cada clase en su propio .java), se haría:

javac Demo.java  	# genera Demo.class (y Punto.class si está en archivo propio)
java Demo        	# ejecuta la clase Demo con método main

### Java es compilado a bytecode intermedio: el compilador javac genera ficheros .class que contienen bytecode. Ese bytecode se ejecuta sobre la Máquina Virtual de Java (JVM), que hace verificación, optimización (JIT) y ejecución, aportando portabilidad (“write once, run anywhere”). Así, Java combina compilación y ejecución virtualizada.



## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Un constructor es un método especial de la clase, sin tipo de retorno, que inicializa el objeto recién creado. Si no se define, Java proporciona un constructor por defecto sin parámetros.
### Ejemplo de clase Empleado con constructor:
class Empleado {
	private String dni;
	private String nombre;
	private String apellidos;

	// Constructor
	Empleado(String dni, String nombre, String apellidos) {
    	this.dni = dni;
    	this.nombre = nombre;
    	this.apellidos = apellidos;
	}

	// Getters básicos (opcional)
	String getDni() { return dni; }
	String getNombre() { return nombre; }
	String getApellidos() { return apellidos; }
}



## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### this es la referencia al objeto actual dentro de un método o constructor. Permite acceder a los atributos y métodos de la instancia y resolver ambigüedades de nombres (parámetros con el mismo nombre que atributos). No se llama igual en todos los lenguajes: en C++ también es this, en Python es self como parámetro explícito, y en otros adoptan variantes.
Ejemplo con this en Punto para un constructor:

class Punto {
	double x;
	double y;

	Punto(double x, double y) {
    	this.x = x; // 'this.x' es el atributo, 'x' es el parámetro
    	this.y = y;
	}

	double calculaDistanciaAOrigen() {
    	return Math.sqrt(this.x * this.x + this.y * this.y);
	}
}



## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Se puede añadir un método de instancia que reciba otro Punto y calcule la distancia empleando la diferencia de coordenadas. Se usa this para subrayar que la operación se realiza respecto al objeto actual.

class Punto {
	double x;
	double y;

	Punto(double x, double y) {
    	this.x = x;
    	this.y = y;
	}

	double calculaDistanciaAOrigen() {
    	return Math.sqrt(x * x + y * y);
	}

	double distanciaA(Punto otro) {
    	double dx = this.x - otro.x;
    	double dy = this.y - otro.y;
    	return Math.sqrt(dx * dx + dy * dy);
	}
}



## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### En Java, todo se pasa por valor. Sin embargo, cuando se pasan objetos, lo que se pasa por valor es la referencia al objeto. Por ello, modificar atributos a través de esa referencia sí afecta al objeto original (porque ambos, dentro y fuera, apuntan al mismo objeto). En cambio, reasignar el parámetro a un nuevo objeto no afecta a la variable del llamador, ya que la referencia en el llamador no cambia.
### Para tipos primitivos como int, se pasa el valor y cualquier modificación dentro del método no afecta a la variable original del llamador. Esto se alinea con el paso por valor de C para primitivos; la diferencia radica en que en Java no hay punteros explícitos, pero la semántica de referencias a objetos produce efectos observables sobre el estado compartido.



## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### toString() es un método heredado de Object que devuelve una representación textual del objeto. Es útil para depuración y logging, y se llama implícitamente al concatenar objetos con cadenas o al imprimirlos con System.out.println. Sobrescribirlo mejora la legibilidad.
### Otros lenguajes tienen conceptos equivalentes: en Python se usan __str__/__repr__, en C# también ToString(), y en C++ suele implementarse la sobrecarga de operator<<. Ejemplo en Punto:
class Punto {
	double x;
	double y;

	Punto(double x, double y) {
    	this.x = x;
    	this.y = y;
	}

	@Override
	public String toString() {
    	return "Punto(" + x + ", " + y + ")";
	}
}




## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Un struct de C modela datos agrupados, pero no incorpora de forma nativa métodos, encapsulamiento, herencia ni polimorfismo. En ese sentido, una clase es como un struct más el comportamiento asociado y mecanismos de ocultación y despacho dinámico.
### Para que un struct se acerque a una clase, se deben simular métodos como funciones que reciben un puntero al struct, gestionar encapsulamiento a nivel de módulo (ocultando el contenido real del struct en el .c), y emular polimorfismo con punteros a función y convenciones. No obstante, esto requiere disciplina y no está integrado en el lenguaje como en Java o C++.



## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### En C, puede definirse un struct con x e y y una función que reciba un puntero al struct. El parámetro que actúa como “this” es precisamente ese puntero pasado explícitamente. Esta convención reproduce la llamada a método, pero sin azúcar sintáctico ni encapsulamiento automático.

// punto.h
#ifndef PUNTO_H
#define PUNTO_H

typedef struct {
	double x;
	double y;
} Punto;

double calculaDistanciaAOrigen(const Punto* p);

#endif

// punto.c
#include "punto.h"
#include <math.h>

double calculaDistanciaAOrigen(const Punto* p) {
	return sqrt(p->x * p->x + p->y * p->y);
}


