```Práctica de Refactorización del código

import java.util.ArrayList;
import java.util.List;

// Clase Producto mejor encapsulada
class Producto {
    // Cambio 1: usar nombres descriptivos y privados (encapsulación)
    private String nombre;
    private double precio;
    private int cantidad;

    // Constructor y elementos nombrados de manera adecuada
    public Producto(String nombre, double precio, int cantidad) {
        this.nombre = nombre;
        this.precio = precio;
        this.cantidad = cantidad;
    }

    // Cambio 2: getters para acceder a los atributos (buena práctica)
    public String getNombre() {
        return nombre;
    }

    public double getPrecio() {
        return precio;
    }

    public int getCantidad() {
        return cantidad;
    }

    // Cambio 3: método para calcular subtotal con descuento aplicado
    public double calcularSubtotal() {
        double subtotal = precio * cantidad;

        // Aplicar descuento si cantidad > 2
        if (cantidad > 2) {
            subtotal *= 0.9; // más limpio que subtotal - (subtotal * 0.1)
        }

        return subtotal;
    }
}

public class Tienda {
    public static void main(String[] args) {

        // Cambio 4: usar interfaz List en lugar de implementación concreta
        List<Producto> lista = new ArrayList<>();

        lista.add(new Producto("Teclado", 30, 2));
        lista.add(new Producto("Ratón", 15, 3));
        lista.add(new Producto("Monitor", 200, 1));

        double total = 0;

        // Cambio 5: usar for-each (más limpio y legible)
        for (Producto producto : lista) {

            double subtotal = producto.calcularSubtotal();

            System.out.println("Producto: " + producto.getNombre());
            System.out.println("Precio: " + producto.getPrecio());
            System.out.println("Cantidad: " + producto.getCantidad());
            System.out.println("Subtotal: " + subtotal);

            // Cambio 6: simplificar lógica de envío
            if (subtotal > 100) {
                System.out.println("Envío gratis");
            } else {
                System.out.println("Envío: 5 euros");
                subtotal += 5;
            }

            // Cambio 7: uso de operador += (más claro)
            total += subtotal;

            System.out.println("-------------------");
        }

        System.out.println("TOTAL PEDIDO: " + total);

        // Cambio 8: mensaje VIP más claro y separado
        if (total > 500) {
            System.out.println("Cliente VIP");
        }
    }
}```

##  Diferencias principales entre ambos códigos

### 1. **Encapsulación (muy importante)**

* **Código original:**
  Los atributos (`n`, `p`, `c`) son públicos y se accede directamente a ellos.
* **Código corregido:**
  Los atributos son `private` y se accede mediante *getters*.

 **Por qué es mejor:**
Protege los datos y evita modificaciones indebidas. Es un principio básico de la programación orientada a objetos.

---

### 2. **Nombres más descriptivos**

* **Original:** `n`, `p`, `c`
* **Corregido:** `nombre`, `precio`, `cantidad`

 **Ventaja:**
El código es mucho más fácil de entender sin necesidad de explicaciones adicionales.

---

### 3. **Separación de responsabilidades**

* **Original:**
  Toda la lógica (cálculos, descuentos) está en `main`.
* **Corregido:**
  Se crea el método `calcularSubtotal()` dentro de `Producto`.

 **Ventaja:**

* Código más organizado
* Reutilizable
* Más fácil de mantener

---

### 4. **Uso de interfaz `List`**

* **Original:**

  ```java
  ArrayList<Producto> lista = new ArrayList<>();
  ```
* **Corregido:**

  ```java
  List<Producto> lista = new ArrayList<>();
  ```

 **Ventaja:**
Permite cambiar la implementación (por ejemplo a `LinkedList`) sin modificar el resto del código.

---

### 5. **Tipo de bucle**

* **Original:** bucle clásico con índice (`for` con `i`)
* **Corregido:** bucle `for-each`

 **Ventaja:**

* Más limpio
* Menos propenso a errores
* Más legible

---

### 6. **Simplificación de operaciones**

* **Original:**

  ```java
  subtotal = subtotal - (subtotal * 0.1);
  total = total + subtotal;
  ```
* **Corregido:**

  ```java
  subtotal *= 0.9;
  total += subtotal;
  ```

 **Ventaja:**
Código más corto y claro.

---

### 7. **Mejor organización del código**

* **Original:**
  Código más “mezclado” y difícil de escalar.
* **Corregido:**
  Código más modular (cada clase hace su trabajo).

 **Ventaja:**
Facilita futuras mejoras (ej: impuestos, descuentos adicionales, interfaz gráfica).

---

### 8. **Legibilidad general**

* **Original:** funcional pero básico.
* **Corregido:** sigue buenas prácticas de Java profesional.

---

##  Conclusión para tu presentación

El código original **funciona**, pero el corregido:

* Es más **seguro**
* Más **claro**
* Más **mantenible**
* Más **escalable**
