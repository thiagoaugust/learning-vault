**Limitação**: se a Factory crescer muito, pode acabar virando um “switch gigante” (e aí o Factory Method ou Abstract Factory são alternativas melhores).

```java
// Produto
public interface Transporte {
    void entregar();
}

// Produtos concretos
public class Caminhao implements Transporte {
    @Override
    public void entregar() {
        System.out.println("Entrega feita por Caminhão.");
    }
}

public class Navio implements Transporte {
    @Override
    public void entregar() {
        System.out.println("Entrega feita por Navio.");
    }
}

// Simple Factory
public class TransporteFactory {
    public static Transporte criarTransporte(String tipo) {
        switch (tipo.toLowerCase()) {
            case "caminhao":
                return new Caminhao();
            case "navio":
                return new Navio();
            default:
                throw new IllegalArgumentException("Tipo de transporte inválido: " + tipo);
        }
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        Transporte t1 = TransporteFactory.criarTransporte("caminhao");
        t1.entregar();

        Transporte t2 = TransporteFactory.criarTransporte("navio");
        t2.entregar();
    }
}
```

