# UT7-A1 – Identificación de “malos olores” en el código


### Objetivo de la práctica

Julian/Peter

El objetivo de esta práctica es **analizar un programa que funciona correctamente pero cuya calidad de código es mejorable**.

Durante la sesión se realizará un **análisis colectivo del código para detectar “malos olores” (code smells)**. Estos son indicios de que el diseño del programa podría mejorarse mediante técnicas de refactorización.

- En esta práctica **no se debe modificar el código**.  
- El trabajo consiste únicamente en **analizarlo y debatir sobre su calidad**.


### Instrucciones de la práctica

Se proporciona un programa sencillo que simula un **sistema básico de gestión de pedidos**.



### Trabajo en clase

1. Lee el código detenidamente.
2. Analiza cómo está organizado.
3. Detecta posibles problemas de diseño o calidad del código.
4. Anota todos los problemas que encuentres.

Durante la sesión se realizará un **debate en clase**, donde cada grupo expondrá los problemas detectados.

### Preguntas que pueden ayudarte en el análisis

Para identificar posibles problemas puedes plantearte las siguientes cuestiones:

- ¿Hay **métodos demasiado largos**?

El main() contiene gran parte del código lo que lo hace insostenible a largo plazo si buscamos optimizar el código

- ¿Las **variables tienen nombres claros y descriptivos**?

Entre todo el código lo menos claro y descriptivo son las variables, siendo que no están definidas con un nombre concreto. Siendo que 

La variable n podría cambiarse por “nombre”.
La variable p podría cambiarse por “precio”.
La variable c podría cambiarse por ”cantidad”.


- ¿Se repite código en diferentes partes del programa?

Se podira decir que si, debido a que el subtotal es una variable definida, y justo despues se aplica en una funcion no tiene ningun sentido.

- ¿Hay **números que aparecen directamente en el código sin explicación**?

Sí, el código hace uso de números sin especificar que son realmente.
El 0.1 en el descuento.
El 5 en el coste de envío.
El 100 en el límite para envío gratis.
El 500 en el límite para considerar al cliente como VIP.

- ¿El código mezcla distintas responsabilidades?
Sí, todos los métodos se realizan dentro del main(). Y esto viola el principio de responsabilidad de los códigos.

- ¿El programa sería fácil de modificar o ampliar?
No. De quererse agregar nuevas modificaciones / funcionalidades, deberíamos modificar el main() y esto aumentaría la probabilidad de que aparezcan errores. Hay que destacar que el código depende bastante de su estructura dada, y eso hace que las modificaciones que se quieran hacer son más complicadas.

- ¿Falta documentación o comentarios que expliquen el funcionamiento?

Sí. En el código no se hace uso de comentarios que documenten ninguna parte del mismo. Por ende, cuando se van a interpretar ciertas partes del código se puede llegar a malinterpretar lo que hace o el porque agrega algo especifico como puede ser un número.











### Código a analizar


El código a analizar es el siguiente:


```java
import java.util.ArrayList;


class Producto {


   String n;
   double p;
   int c;


   public Producto(String n, double p, int c) {
       this.n = n;
       this.p = p;
       this.c = c;
   }
}


public class Tienda {


   public static void main(String[] args) {


       ArrayList<Producto> lista = new ArrayList<>();


       lista.add(new Producto("Teclado", 30, 2));
       lista.add(new Producto("Raton", 15, 3));
       lista.add(new Producto("Monitor", 200, 1));


       double total = 0;


       for (int i = 0; i < lista.size(); i++) {


           Producto p = lista.get(i);


           double subtotal = p.p * p.c;


           if (p.c > 2) {
               subtotal = subtotal - (subtotal * 0.1);
           }


           System.out.println("Producto: " + p.n);
           System.out.println("Precio: " + p.p);
           System.out.println("Cantidad: " + p.c);
           System.out.println("Subtotal: " + subtotal);


           if (subtotal > 100) {
               System.out.println("Envio gratis");
           } else {
               System.out.println("Envio: 5 euros");
               subtotal = subtotal + 5;
           }


           total = total + subtotal;


           System.out.println("-------------------");
       }


       System.out.println("TOTAL PEDIDO: " + total);


       if (total > 500) {
           System.out.println("Cliente VIP");
       }


   }
}

