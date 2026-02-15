<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

### # Encapsulación y Ocultación de Información en POO

## **Objetivos principales:**

**Encapsulación**:
 - Agrupar datos (atributos) y métodos (comportamientos) que operan sobre esos datos en una sola unidad (clase).
 - Controlar el acceso a los datos internos mediante interfaces públicas bien definidas.

**Ocultación de Información**:
 - Ocultar los detalles de implementación internos de una clase.
 - Exponer solo lo que es necesario y seguro para el exterior.
 - Proteger el estado interno del objeto de modificaciones inadecuadas.

### **Ventajas de la Ocultación de Información:**

1. **Reducción de la Complejidad**: Los usuarios de la clase solo necesitan conocer la interfaz pública, no los detalles internos.

2. **Mejora del Mantenimiento**: Se pueden modificar los detalles internos de la clase sin afectar el código que la utiliza.

3. **Aumento de la Seguridad**: Protege los datos críticos de modificaciones accidentales o malintencionadas.

4. **Mejor Modularidad**: Permite desarrollar componentes independientes que interactúan a través de interfaces bien definidas.

5. **Facilita la Depuración**: Al limitar el acceso a los datos, se reducen los puntos donde pueden ocurrir errores.

6. **Promueve la Reutilización**: Las clases bien encapsuladas son más fáciles de reutilizar en diferentes contextos.

7. **Permite Validación y Control**: Al acceder a los datos a través de métodos (getters/setters), se pueden implementar validaciones y lógica de control.

### La combinación de encapsulación y ocultación de información es fundamental para lograr los principios de **abstracción** y **modularidad** en el diseño de software orientado a objetos.


## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### # **Interfaz Pública en POO**

### **¿Qué es la Interfaz Pública?**

La **interfaz pública** de un objeto o clase en POO es el conjunto de **métodos y propiedades** que están **accesibles desde fuera** de la clase. Constituye la "cara visible" que la clase expone al mundo exterior para interactuar con ella.

**Componentes típicos de una interfaz pública:**
- Métodos públicos (declarados como `public`)
- Propiedades/atributos públicos (con getters/setters)
- Constantes públicas
- Constructores
- En algunos lenguajes: operadores sobrecargados visibles externamente

### **Relación con la Ocultación de Información**

La interfaz pública **se relaciona directamente con la ocultación de información** mediante:

### **1. Separación entre "qué" y "cómo"**
- **La interfaz pública define "QUÉ"** puede hacer el objeto (sus capacidades)
- **La implementación interna define "CÓMO"** lo hace (detalles ocultos)

### **2. Contrato bien definido**
La interfaz actúa como un **contrato** que garantiza ciertas funcionalidades sin revelar cómo se implementan, permitiendo:
```java
// Ejemplo: La interfaz solo muestra QUÉ hace
public class CuentaBancaria {
    // Interfaz pública
    public void depositar(double monto) { ... }
    public void retirar(double monto) { ... }
    public double obtenerSaldo() { ... }
    
    // Implementación oculta (privada)
    private double saldo;
    private void registrarTransaccion() { ... }
}
```

### **3. Mecanismo de acceso controlado**
- **La interfaz pública es la única vía** para interactuar con el objeto
- **Protege el estado interno** (atributos privados) de accesos directos
- **Valida y controla** las operaciones antes de modificar datos internos

### **4. Abstracción como resultado**
La combinación de:
- **Interfaz pública** (lo que se expone)
- **Ocultación de información** (lo que se esconde)
  
... produce **abstracción** - el usuario trabaja con conceptos de alto nivel sin preocuparse por detalles de implementación.

### **Analogía práctica**

Piensa en un **automóvil**:
- **Interfaz pública**: Volante, pedales, palanca de cambios
- **Ocultación de información**: Motor, transmisión, sistema eléctrico
- **Beneficio**: Puedes conducir (usar la interfaz) sin saber ingeniería mecánica (implementación)

Esta separación permite **evolucionar la implementación** (mejorar el motor) **sin cambiar la interfaz** (los controles siguen funcionando igual).


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### # **Interfaz Pública: Diseño y Cambios**

### **¿Por qué diseñarla con cuidado?**

- Es el **contrato permanente** con el código cliente
- Define **cómo otros interactúan** con tu clase
- **Refleja la abstracción** que ofreces
- Una mala interfaz genera **código frágil y difícil de mantener**

### **¿Es fácil cambiarla?**

**NO.** Cambiarla es **costoso y arriesgado** porque:

1. **Rompe compatibilidad** con todo el código existente que la usa
2. **Requiere refactorizar** todas las dependencias
3. **Puede introducir bugs** en sistemas en producción
4. **En APIs públicas/librerías**, obliga a los usuarios a adaptar su código

### **Conclusión clave**

Diseña interfaces **minimalistas, estables y bien abstraídas** desde el inicio. Una vez publicada, cambiarla tiene **alto costo**.


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### # **Invariantes de Clase y Ocultación de Información**

### **¿Qué son las Invariantes de Clase?**

Son **condiciones o reglas** que deben mantenerse **siempre verdaderas** para todas las instancias de una clase, en **todo momento** (excepto durante la ejecución de un método). Representan el **estado válido y consistente** del objeto.

### **Ejemplos de invariantes:**
- En `CuentaBancaria`: `saldo ≥ 0` (no puede haber saldo negativo)
- En `Rectángulo`: `ancho > 0 && altura > 0`
- En `Fecha`: `1 ≤ día ≤ 31` (dependiendo del mes)
- En `ListaCircular`: `últimoNodo.siguiente == primerNodo`

### **¿Cómo ayuda la Ocultación de Información?**

### **1. Control Centralizado**
Al ocultar los datos (atributos privados), **solo los métodos de la clase** pueden modificarlos, permitiendo:
```java
public void retirar(double monto) {
    if (monto <= saldo) {       // Verifica invariante
        saldo -= monto;         // Modificación segura
    } else {
        // Manejo de error
    }
}
```

### **2. Validación en Punto Único**
Los setters/propiedades pueden **validar invariantes**:
```java
private int edad;

public void setEdad(int edad) {
    if (edad >= 0 && edad <= 120) {  // Invariante: edad válida
        this.edad = edad;
    }
}
```

### **3. Preservación entre Operaciones**
Cada método **asegura** que al terminar, las invariantes se mantienen:
- **Precondiciones**: Lo que debe ser cierto ANTES de ejecutar
- **Postcondiciones**: Lo que será cierto DESPUÉS de ejecutar
- **Invariante**: Lo que es cierto ANTES y DESPUÉS

### **4. Encapsulación del Conocimiento**
Solo la clase **conoce sus propias reglas** de consistencia, evitando que código externo viole invariantes accidentalmente.

### **Beneficio Clave**

La ocultación transforma las invariantes de **"reglas documentadas"** (que los usuarios podrían ignorar) en **"reglas impuestas"** (garantizadas por el código), aumentando la **robustez** y **confiabilidad** del sistema.


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

### # **Clase `Punto` en Java con Ocultación de Información**

```java
public class Punto {
    // Atributos PRIVADOS - ocultación de información
    private double x;
    private double y;
    
    // Constructor PÚBLICO - parte de la interfaz
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    // Método PÚBLICO - parte de la interfaz
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
    
    // Getters PÚBLICOS - parte de la interfaz
    public double getX() {
        return x;
    }
    
    public double getY() {
        return y;
    }
    
    // Setters PÚBLICOS con validación opcional
    public void setX(double x) {
        this.x = x;
    }
    
    public void setY(double y) {
        this.y = y;
    }
    
    // Método PRIVADO - no es parte de la interfaz pública
    private boolean estaEnOrigen() {
        return x == 0 && y == 0;
    }
}
```

### **Interfaz Pública de la Clase `Punto`**

La interfaz pública incluye **todo lo declarado como `public`**:

1. **Constructor**: `Punto(double x, double y)`
2. **Métodos públicos**:
   - `calcularDistanciaAOrigen()`
   - `getX()`, `getY()`
   - `setX(double x)`, `setY(double y)`

Esto es **todo lo que el código externo puede usar**:
```java
// Uso desde otra clase
Punto p = new Punto(3.0, 4.0);  // Usa constructor público
double distancia = p.calcularDistanciaAOrigen();  // Usa método público
double coordX = p.getX();  // Usa getter público
```

### **Significado de `public` y `private`**

### **`private`**
- **Acceso restringido**: Solo accesible **desde dentro de la misma clase**
- **Ocultación**: Los atributos `x` e `y` son **internos**, no visibles externamente
- **Control**: La clase decide **cómo** exponer su estado (vía getters/setters)

### **`public`**
- **Acceso abierto**: Accesible **desde cualquier clase**
- **Interfaz**: Define **cómo interactuar** con el objeto
- **Contrato**: Promete funcionalidad al mundo exterior

### **Ventaja de este Diseño**

Si mañana cambiamos la implementación interna (ej: usar coordenadas polares), **la interfaz pública sigue igual**:
```java
// Nueva implementación (los usuarios no notan el cambio)
public class Punto {
    private double radio;  // Cambiamos atributos
    private double angulo; // ¡Pero son privados!
    
    public double calcularDistanciaAOrigen() {
        return radio;  // Mismo resultado, implementación diferente
    }
    
    public double getX() {
        return radio * Math.cos(angulo);  // getter mantiene contrato
    }
    // ... resto igual
}
```

**Los usuarios siguen usando** `p.calcularDistanciaAOrigen()` **igual que antes**, sin saber que internamente cambió todo. Ese es el poder de la ocultación.

## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### # **Alcance de los Modificadores `public` y `private` en Java**

### **Elementos que pueden tener `public` o `private`**

### **1. CLASES**
```java
public class ClasePublica { }    // Accesible desde cualquier paquete
private class ClasePrivada { }   // Solo clases internas/anidadas
```

### **2. ATRIBUTOS (Variables de instancia/clase)**
```java
public class Ejemplo {
    public int atributoPublico;     // Acceso directo desde cualquier clase
    private int atributoPrivado;    // Solo accesible dentro de esta clase
}
```

### **3. MÉTODOS**
```java
public void metodoPublico() { }   // Invocable desde cualquier clase
private void metodoPrivado() { }  // Solo invocable dentro de esta clase
```

### **4. CONSTRUCTORES**
```java
public MiClase() { }    // Cualquiera puede crear instancias
private MiClase() { }   // Solo la propia clase puede crear instancias
                         // (útil para Singleton, Builder)
```

### **5. INTERFACES**
```java
public interface MiInterface { }   // Implementable por cualquier clase
// private interface NoValido { }  // ❌ NO PERMITIDO (excepto anidadas)
```

### **6. ENUMERACIONES (enums)**
```java
public enum DiaSemana { LUNES, MARTES }
// private enum SoloInterno { }   // Solo como enum anidado
```

### **7. CLASES INTERNAS/ANIDADAS**
```java
public class Externa {
    public class InternaPublica { }
    private class InternaPrivada { }  // Solo visible para la clase Externa
}
```

### **Restricciones Importantes**

### **NO se pueden aplicar a:**
- **Variables locales** (dentro de métodos)
  ```java
  void miMetodo() {
      // private int x = 5;  // ❌ ERROR
      int x = 5;             // ✅ Solo visible en el método
  }
  ```
- **Parámetros de métodos**
- **Bloques de código** (como bloques `static` o de instancia)

### **Resumen Visual**

| Elemento | `public` | `private` | Notas |
|----------|----------|-----------|-------|
| Clase externa | ✅ | ❌ | Una clase de nivel superior no puede ser `private` |
| Clase interna | ✅ | ✅ | Clases anidadas pueden ser `private` |
| Atributos | ✅ | ✅ | Control de acceso a datos |
| Métodos | ✅ | ✅ | Control de visibilidad de operaciones |
| Constructores | ✅ | ✅ | Control de creación de instancias |
| Interfaces | ✅ | ❌* | *Excepto interfaces anidadas |
| Enums | ✅ | ❌* | *Excepto enums anidadas |

### **Jerarquía de Paquetes**
Para clases `public` de nivel superior:
```
proyecto/
├── paqueteA/
│   └── ClasePublica.java  // public class ClasePublica
└── paqueteB/
    └── OtraClase.java     // Puede usar ClasePublica importando
```

### **Principio Básico**
**`public`** = "Visible para todos"  
**`private`** = "Visible solo para mí (mi clase)"  

Esta distinción es **fundamental** para la ocultación de información: lo que es `private` está **oculto**, lo que es `public` forma la **interfaz**.


## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### # **Tipos de Visibilidad en POO**

### **Más allá de Público y Privado**

En POO existen **más niveles de visibilidad** que solo `public` y `private`. Estos niveles permiten un **control más granular** del acceso, especialmente importante para la modularidad y la ocultación de información.

### **En Java: 4 Niveles de Visibilidad**

Java tiene **4 modificadores de acceso**, ordenados de más a menos restrictivo:

### **1. `private`** - Más restrictivo
- **Visible solo** dentro de la **misma clase**
- **No accesible** por subclases, clases del mismo paquete, u otras clases
- **Ejemplo**: Datos internos, métodos auxiliares

### **2. `default` (package-private)** - Sin modificador
- **Visible** dentro del **mismo paquete**
- **No visible** fuera del paquete, incluso para subclases en otro paquete
- **Ejemplo**: `int x;` (sin `public`, `private` o `protected`)
```java
class ClaseDefault {  // Clase visible solo en su paquete
    int atributoDefault;  // Accesible solo en el mismo paquete
}
```

### **3. `protected`**
- **Visible** dentro del **mismo paquete** (como `default`)
- **PLUS**: También visible para **subclases**, incluso en otros paquetes
- **Ejemplo**: Atributos/métodos para herencia
```java
public class Padre {
    protected int dato;  // Subclases pueden acceder
}
```

### **4. `public`** - Menos restrictivo
- **Visible desde cualquier clase** en cualquier paquete
- **Ejemplo**: Interfaz pública de la clase

### **Resumen de Visibilidad en Java**

| Modificador | Misma Clase | Mismo Paquete | Subclase (otro paquete) | Cualquier Clase |
|-------------|-------------|---------------|-------------------------|-----------------|
| `private`   | ✅          | ❌            | ❌                      | ❌              |
| `default`   | ✅          | ✅            | ❌                      | ❌              |
| `protected` | ✅          | ✅            | ✅                      | ❌              |
| `public`    | ✅          | ✅            | ✅                      | ✅              |

### **En Otros Lenguajes**

### **C++** (Más complejo)
- `private`, `protected`, `public` (similares a Java)
- Amigos (`friend`): Clases/funciones específicas que pueden acceder a miembros privados
- Herencia con modificadores: `class Derivada : private Base`

### **C#** (Similar a Java pero con más opciones)
- `private`, `protected`, `internal`, `public`
- `internal`: Como `default` en Java (accesible en el mismo ensamblado)
- `protected internal`: Unión de `protected` e `internal`
- `private protected`: Intersección (solo subclases en mismo ensamblado)

### **Python** (Por convención)
- **Público**: `atributo`
- **"Protegido"**: `_atributo` (convención, realmente público)
- **"Privado"**: `__atributo` (name mangling, no totalmente privado)
- Sin verificación en tiempo de compilación

### **Kotlin** (Simplificado)
- `private`, `protected`, `internal`, `public` (por defecto)
- `internal`: Visible en el mismo módulo
- Sin modificador = `public`

### **JavaScript/TypeScript**
- `public`, `private`, `protected` (desde ES6/TypeScript)
- `#atributo`: Campos privados reales (ES2022)
- Anteriormente por convención: `_atributoPrivado`

### **Comparativa entre Lenguajes**

| Lenguaje | Niveles | Característica Única |
|----------|---------|---------------------|
| Java | 4 | `default` (package) muy usado internamente |
| C++ | 3 + `friend` | Control más fino con herencia y friends |
| C# | 6 | `internal` para control de ensamblado |
| Python | Por convención | Sin enforcement estricto |
| Kotlin | 4 | `internal` para modularidad |

### **Importancia del Diseño de Visibilidad**

Cada nivel responde a diferentes necesidades de diseño:
- **`private`**: Ocultación total (implementación interna)
- **`default`/`internal`**: Modularidad a nivel de paquete/módulo
- **`protected`**: Herencia controlada
- **`public`**: Interfaz pública estable

### **Elección de Visibilidad según Contexto**

```java
public class Biblioteca {
    private List<Libro> inventario;     // Detalle de implementación
            int contadorInterno;        // Uso interno del paquete
    protected void metodoParaHerencia() // Para subclases
    public void prestarLibro()          // Interfaz pública
}
```

La **visibilidad adecuada** es clave para:
1. **Mínima exposición** necesaria
2. **Acoplamiento controlado** entre módulos
3. **Facilidad de mantenimiento**
4. **Evolución del sistema** sin romper dependencias


## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### # **Visibilidad de Miembros Privados entre Instancias**

### **Respuesta Correcta: (a) otras clases**

Los miembros `private` están **ocultos para otras clases**, pero **NO para otras instancias de la misma clase**. Una instancia **puede acceder directamente** a los miembros privados de otra instancia **de la misma clase**.

### **Ejemplo con `Punto`**

```java
public class Punto {
    private double x;
    private double y;
    
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    // Método que ACCEDE a miembros privados de OTRA instancia
    public double calcularDistanciaAPunto(Punto otro) {
        // Acceso DIRECTO a otro.x y otro.y aunque sean privados
        // Porque 'otro' es otra instancia de la MISMA clase Punto
        double dx = this.x - otro.x;    // otro.x es privado pero accesible
        double dy = this.y - otro.y;    // otro.y es privado pero accesible
        return Math.sqrt(dx * dx + dy * dy);
    }
    
    // Otro ejemplo: comparar coordenadas
    public boolean tieneMismaX(Punto otro) {
        return this.x == otro.x;  // Acceso directo a privado de otra instancia
    }
}
```

### **Uso del Método**

```java
public class Main {
    public static void main(String[] args) {
        Punto p1 = new Punto(3, 4);
        Punto p2 = new Punto(6, 8);
        
        // p1 accede a privados de p2 internamente
        double distancia = p1.calcularDistanciaAPunto(p2);
        System.out.println("Distancia: " + distancia);
    }
}
```

### **¿Por qué es posible esto?**

### **Fundamento en POO:**
1. **`private` significa "privado a la clase"**, no "privado a la instancia"
2. La **clase** es la unidad de encapsulación, no cada instancia individual
3. Todos los objetos de una misma clase **comparten conocimiento** de su estructura interna

### **Analogía:**
- En una empresa, los **empleados (instancias)** pueden ver los **datos privados de otros empleados** si pertenecen al **mismo departamento (clase)**
- Pero **empleados de otra empresa (otra clase)** no pueden acceder

### **Imposibilidad de Acceso desde Otra Clase**

```java
public class OtraClase {
    public void intentarAcceder() {
        Punto p = new Punto(1, 2);
        
        // double valor = p.x;  // ❌ ERROR COMPILACIÓN
        // double valor = p.y;  // ❌ ERROR: x e y son privados
        
        // Solo métodos públicos son accesibles
        double distancia = p.calcularDistanciaAPunto(new Punto(3, 4));  // ✅
    }
}
```

### **Regla de Acceso a Privados en Java**

| Desde | Acceso a `private` de otra instancia | Ejemplo |
|-------|--------------------------------------|---------|
| **Misma clase** | ✅ **PERMITIDO** | `otro.atributoPrivado` |
| **Otra clase** | ❌ **PROHIBIDO** | Error de compilación |

### **Implicaciones de Diseño**

Esta regla permite:
1. **Métodos de comparación** eficientes (`equals`, `compareTo`)
2. **Métodos de copia** que acceden directamente a datos (`copy`, `clone`)
3. **Patrones como Factory** que necesitan construir objetos accediendo a privados
4. **Operaciones entre objetos** sin exponer getters innecesarios

```java
// Ejemplo útil: método equals
@Override
public boolean equals(Object obj) {
    if (this == obj) return true;
    if (!(obj instanceof Punto)) return false;
    Punto otro = (Punto) obj;
    // Acceso directo a privados para comparación eficiente
    return Double.compare(this.x, otro.x) == 0 &&
           Double.compare(this.y, otro.y) == 0;
}
```

### **Conclusión**

La visibilidad `private` **oculta información de otras clases**, pero **no de otras instancias de la misma clase**. Esto es **diseñado intencionalmente** para permitir operaciones entre objetos relacionados mientras se mantiene la encapsulación frente al mundo exterior.


## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

###  **Métodos Getter y Setter en POO**

### **Definición**

Los **getters** y **setters** (también llamados **accesores** y **mutadores**) son métodos públicos que permiten **leer** y **modificar** atributos privados de una clase, respetando el principio de **ocultación de información**.

### **Getter (Accesor)**
- **Lee/obtiene** el valor de un atributo privado
- Convención de nombre: `getAtributo()` o `isAtributo()` para booleanos
- **No modifica** el estado del objeto

### **Setter (Mutador)**
- **Escribe/modifica** el valor de un atributo privado
- Convención de nombre: `setAtributo(valor)`
- **Puede incluir validaciones** antes de modificar

### **Ejemplo Básico**

```java
public class Persona {
    // Atributos PRIVADOS (ocultación)
    private String nombre;
    private int edad;
    private boolean activo;
    
    // GETTERS
    public String getNombre() {
        return nombre;
    }
    
    public int getEdad() {
        return edad;
    }
    
    public boolean isActivo() {  // "is" para booleanos
        return activo;
    }
    
    // SETTERS
    public void setNombre(String nombre) {
        // Puede incluir validación
        if (nombre != null && !nombre.trim().isEmpty()) {
            this.nombre = nombre;
        }
    }
    
    public void setEdad(int edad) {
        // Validación de invariante
        if (edad >= 0 && edad <= 120) {
            this.edad = edad;
        } else {
            throw new IllegalArgumentException("Edad inválida");
        }
    }
    
    public void setActivo(boolean activo) {
        this.activo = activo;
    }
}
```

### **Propósito y Beneficios**

### **1. Control de Acceso**
```java
// Sin getter/setter (mal diseño)
public class Cuenta {
    public double saldo;  // ¡Acceso directo peligroso!
}

// Con getter/setter (buen diseño)
public class Cuenta {
    private double saldo;
    
    public double getSaldo() {
        return saldo;
    }
    
    public void depositar(double monto) {  // Setter especializado
        if (monto > 0) {
            saldo += monto;
        }
    }
    
    // NO hay setSaldo() - control total sobre modificaciones
}
```

### **2. Validación y Lógica**
```java
public void setEmail(String email) {
    if (email != null && email.contains("@")) {
        this.email = email;
    } else {
        throw new IllegalArgumentException("Email inválido");
    }
}
```

### **3. Encapsulación de Cambios**
```java
public class Producto {
    private double precio;
    
    // Getter puede incluir lógica de cálculo
    public double getPrecioConIVA() {
        return precio * 1.21;  // Cambio interno transparente
    }
    
    // Cambio futuro: si cambia la tasa IVA, solo se modifica aquí
}
```

### **4. Compatibilidad hacia Atrás**
Si cambias la implementación interna, la interfaz (getters/setters) permanece:
```java
public class Persona {
    // Antes: almacenamos edad directamente
    // private int edad;
    
    // Después: calculamos edad desde fecha nacimiento
    private LocalDate fechaNacimiento;
    
    // Getter MANTIENE la misma interfaz
    public int getEdad() {
        return Period.between(fechaNacimiento, LocalDate.now()).getYears();
    }
    
    // Setter se adapta
    public void setEdad(int edad) {
        this.fechaNacimiento = LocalDate.now().minusYears(edad);
    }
}
```

## **Patrones Relacionados**

### **1. Read-Only (Solo getter)**
```java
public class Configuracion {
    private final String version = "1.0";
    
    public String getVersion() {
        return version;  // Solo lectura
    }
    // NO hay setVersion()
}
```

### **2. Write-Only (Solo setter) - Raro**
```java
public class Logger {
    private String archivoLog;
    
    public void setArchivoLog(String archivo) {
        this.archivoLog = archivo;
        inicializarLog();  // Lógica interna
    }
    // NO hay getArchivoLog()
}
```

### **3. Getters/Setters Inteligentes**
```java
public class Cache {
    private Map<String, Object> datos;
    private Date ultimaActualizacion;
    
    public Object get(String clave) {
        if (datos == null) {
            cargarCache();  // Lazy initialization
        }
        return datos.get(clave);
    }
}
```

### **Críticas y Alternativas Modernas**

### **Problema del "Bean Anémico"**
Clases con solo getters/setters y sin lógica de negocio.

### **Alternativas:**
1. **Principio "Tell, Don't Ask"**: En lugar de pedir datos y actuar, decirle al objeto qué hacer.
   ```java
   // MAL: Pedir y modificar desde afuera
   if (cuenta.getSaldo() > 100) {
       cuenta.setSaldo(cuenta.getSaldo() - 100);
   }
   
   // BIEN: El objeto maneja su lógica
   cuenta.retirar(100);
   ```

2. **Records en Java (Java 14+)**: Inmutables automáticos.
   ```java
   public record Persona(String nombre, int edad) {}
   // Getters automáticos: nombre(), edad()
   // Inmutable: NO tiene setters
   ```

3. **Patrón Builder**: Para objetos complejos.
4. **Lombok**: Anotaciones para generar getters/setters automáticamente.
   ```java
   @Getter @Setter
   public class Persona {
       private String nombre;
       private int edad;
   }
   ```

### **Conclusión**

Los getters/setters son el **mecanismo estándar** para acceder a atributos privados manteniendo la **encapsulación**. Sin embargo, el diseño moderno favorece:
- **Objetos ricos** con comportamiento sobre datos
- **Inmutabilidad** cuando sea posible
- **Métodos con significado semántico** (`retirar()`, `activar()`) sobre setters genéricos

La clave es **exponer comportamiento, no solo datos**.


## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Respuesta


## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Respuesta


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Respuesta


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta


## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### Respuesta


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Respuesta


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Respuesta


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### Respuesta


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### Respuesta


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Respuesta


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Respuesta


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

### Respuesta


## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta
