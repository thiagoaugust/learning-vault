## 📖 Definição
O **Factory Method** é um padrão de design criacional que define uma interface para criar objetos, mas permite que as subclasses decidam **qual classe instanciar**.  
O objetivo é **desacoplar o código cliente da lógica de criação** dos objetos, facilitando extensões e manutenções.

## 📝 Resumo rápido

O Factory Method **desacopla o cliente da criação de objetos**, permitindo que subclasses escolham qual instância fornecer.  
É útil quando há **múltiplas variações de um mesmo tipo** de objeto e queremos **flexibilidade sem alterar o código cliente**.

---
## 🛠️ Exemplo em Java

### Interface e produtos concretos
```java
// Produto
public interface Transporte {
    void entregar();
}

// Produtos concretos
public class Caminhao implements Transporte {
    public void entregar() {
        System.out.println("Entrega feita por Caminhão.");
    }
}

public class Navio implements Transporte {
    public void entregar() {
        System.out.println("Entrega feita por Navio.");
    }
}

// Criador abstrato
public abstract class Logistica {
    public abstract Transporte criarTransporte();

    public void planejarEntrega() {
        Transporte transporte = criarTransporte();
        transporte.entregar();
    }
}

// Criadores concretos
public class LogisticaRodoviaria extends Logistica {
    @Override
    public Transporte criarTransporte() {
        return new Caminhao();
    }
}

public class LogisticaMaritima extends Logistica {
    @Override
    public Transporte criarTransporte() {
        return new Navio();
    }
}

public class Main {
    public static void main(String[] args) {
        Logistica logistica1 = new LogisticaRodoviaria();
        logistica1.planejarEntrega();

        Logistica logistica2 = new LogisticaMaritima();
        logistica2.planejarEntrega();
    }
}
```

## 🔄 Variações

- **Simple Factory**: encapsula a lógica de criação em um único método estático (não é considerado um “padrão oficial” pelo GoF, mas é bastante usado).
    
- **Factory Method**: delega a decisão de criação para subclasses, permitindo maior flexibilidade e extensibilidade.
    
- **Abstract Factory**: cria **famílias de objetos relacionados**, garantindo consistência entre eles.
    

---
## 📌 Pontos de atenção

- Pode aumentar a **complexidade do código** ao introduzir várias subclasses.
    
- Traz flexibilidade quando se espera **muitas variações de objetos**.
    
- Ajuda a aplicar o **Princípio Aberto-Fechado (OCP)**, já que novas classes podem ser adicionadas sem modificar o código cliente.   

---

