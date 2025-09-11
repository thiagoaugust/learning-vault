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

## 🚩 Quando o Factory Method vira um Anti-Pattern

### 1. **Quando a hierarquia fica excessiva**

- Criar muitas subclasses apenas para instanciar objetos simples.
    
- Isso adiciona **complexidade desnecessária** em cenários que poderiam ser resolvidos com um simples `new`.
    

👉 Exemplo: ter uma fábrica para cada tipo de DTO simples.

---

### 2. **Quando vira um “switch disfarçado”**

- Se a Factory acaba acumulando muitos `if/else` ou `switch` para decidir qual objeto criar.
    
- Nesse caso, perde-se a vantagem do desacoplamento e a Factory vira um **Deus da criação** centralizado.
    

👉 Exemplo: uma única fábrica com dezenas de condições para diferentes produtos.

---

### 3. **Uso em casos onde não há variação real**

- O Factory Method só faz sentido quando existe a **possibilidade de múltiplas variações de um mesmo tipo de objeto**.
    
- Se você sempre retorna a mesma classe, o padrão vira apenas **um indirection desnecessário**.
    

👉 Exemplo: ter uma `CachorroFactory` que sempre retorna `new Cachorro()`.

---

### 4. **Quando é usado como desculpa para não aplicar Injeção de Dependência**

- Às vezes, desenvolvedores usam Factories para controlar dependências que poderiam ser facilmente resolvidas com **IoC containers** (Spring, Guice, CDI).
    
- Isso pode gerar acoplamento desnecessário ao invés de reduzir.
    

👉 Exemplo: usar factories customizadas em um projeto Spring onde o container já poderia gerenciar as instâncias.

---

## ✅ Quando faz sentido

- Quando o número de variações **pode crescer ao longo do tempo**.
    
- Quando queremos aplicar **OCP (Open-Closed Principle)**, permitindo que novas classes sejam adicionadas sem alterar o cliente.
    
- Quando a lógica de criação é complexa e precisa ser isolada.