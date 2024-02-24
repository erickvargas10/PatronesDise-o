import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;
// Interfaz Componente
interface Producto {
    public String descripcion();
    public double precio();
}

// Clase Concreta Componente
class ProductoX implements Producto {
    public String descripcion() {
        return "Mesa rectangular";
    }

    public double precio() {
        return 100.00;
    }
}

// Clase Decoradora
abstract class ProductoDecorator implements Producto {
    protected Producto ProductoDecorado;

    public ProductoDecorator(Producto ProductoDecorado) {
        this.ProductoDecorado = ProductoDecorado;
    }

    public String descripcion() {
        return ProductoDecorado.descripcion();
    }

    public double precio() {
        return ProductoDecorado.precio();
    }
}

// Decorador con Iva actual
class ConIva extends ProductoDecorator {
    public ConIva(Producto ProductoDecorado) {
        super(ProductoDecorado);
    }

    public String descripcion() {
        return ProductoDecorado.descripcion() + ", con Iva Actual 12%";
    }

    public double precio() {
        return ProductoDecorado.precio() * 1.12;
    }
}

// Decorador Con Iva Nuevo
class ConIvaNuevo extends ProductoDecorator {
    public ConIvaNuevo(Producto ProductoDecorado) {
        super(ProductoDecorado);
    }

    public String descripcion() {
        return ProductoDecorado.descripcion() + ", con nuevo Iva 15%";
    }

    public double precio() {
        return ProductoDecorado.precio() * 1.15;
    }
}

public class Main {
    public static void main(String[] args) {
        // Producto 
        Producto Miproducto = new ProductoX();
        System.out.println("Descripción: " + Miproducto.descripcion());
        System.out.println("Precio: $" + Miproducto.precio());

        //Producto Con iva Actual
        Producto ProductoIva = new ConIva(new ProductoX());
        //System.out.println("Descripción: " + ProductoIva.descripcion());
        System.out.println("Precio con Iva actual 12%: $" + ProductoIva.precio());

        // Producto Con nuevo Iva
        Producto ProductoIvaNuevo = new ConIvaNuevo(new ProductoX());
        //System.out.println("Descripción: " + ProductoIvaNuevo.descripcion());
        System.out.println("Precio con Iva 15%: $" + ProductoIvaNuevo.precio());
    }
}


