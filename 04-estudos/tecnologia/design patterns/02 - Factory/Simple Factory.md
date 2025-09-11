## 📖 Definição – Simple Factory

O **Simple Factory** não é considerado um padrão oficial do GoF, mas é uma abordagem muito usada no dia a dia.  
Ele consiste em **encapsular a lógica de criação de objetos em uma única classe ou método estático**, de forma que o cliente não precise instanciar os objetos diretamente com `new`.

Em outras palavras:  
👉 O cliente pede um objeto para a fábrica → a fábrica decide **qual classe instanciar e retornar**.

## ✅ Quando usar

- Quando há **múltiplas variações** de um objeto e não queremos expor `new` em todos os lugares.

- Para **centralizar** a lógica de criação (especialmente quando envolve regras de negócio simples).

- Em casos simples, antes de partir para padrões mais complexos como **Factory Method** ou **Abstract Factory**.

## 🚩 Quando **não usar** o Simple Factory

### 1. **Quando há muitas variações complexas de objetos**

Se a fábrica começa a ter dezenas de `if/else` ou `switch`, ela vira um **Deus da criação** centralizado e difícil de manter.  
👉 Nesse caso, pode ser melhor evoluir para **Factory Method** ou **Abstract Factory**.

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

