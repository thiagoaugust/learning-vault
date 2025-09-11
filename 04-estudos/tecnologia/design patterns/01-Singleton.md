# 🟦 Design Pattern: Singleton

## 📝 Resumo rápido

O Singleton garante **uma única instância global** de uma classe.  
É útil para gerenciar recursos compartilhados (ex: configurações, logs, conexões), mas deve ser usado com cautela para evitar mau uso como anti-pattern.

---
## 📖 Definição
O **Singleton** é um padrão de design criacional que garante que uma classe possua **apenas uma instância** em todo o sistema e fornece um ponto global de acesso a ela.  
É útil quando precisamos controlar o acesso a um recurso compartilhado 
(ex: conexão a banco, gerenciador de configuração, logger).

---
## 🛠️ Exemplo em Java

```java
public class Singleton {

    // 1. Instância única (criada de forma "lazy")
    private static Singleton instance;

    // 2. Construtor privado para evitar criação externa
    private Singleton() {}

    // 3. Método público de acesso
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    // 4. Exemplo de método
    public void showMessage() {
        System.out.println("Hello from Singleton!");
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        Singleton singleton = Singleton.getInstance();
        singleton.showMessage();
    }
}
```

## 🔄 Variações

- **Eager Initialization**  
  A instância é criada no momento em que a classe é carregada.  
  Mais simples, mas pode desperdiçar recursos se a instância não for usada.  

- **Lazy Initialization**  
  A instância só é criada quando for necessária.  
  Economia de recursos, mas precisa de cuidado com **thread-safety**.  

- **Thread-safe Singleton**  
  Utiliza `synchronized` ou técnicas como **Double-Checked Locking** para garantir segurança em ambientes concorrentes.  

- **Enum Singleton**  
  A forma mais simples e segura em Java. O `enum` garante instância única e é thread-safe por natureza.  

```java
public enum EnumSingleton {
    INSTANCE;

    public void showMessage() {
        System.out.println("Hello from Enum Singleton!");
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        EnumSingleton.INSTANCE.showMessage();
    }
}
```
## 📌 Pontos de atenção

- Singleton pode aumentar **acoplamento global** se usado de forma excessiva.    
- Dificulta testes unitários, pois a instância global é difícil de isolar/mockar.    
- Deve ser aplicado somente quando realmente faz sentido ter **uma única instância**.   

---

## 🚩 Quando o Singleton vira Anti-Pattern

### 1. **Uso como “variável global disfarçada”**

- Se a classe Singleton começa a ser usada apenas para **acessar dados globais** em qualquer parte do código.    
- Isso aumenta **acoplamento** e torna o sistema rígido → qualquer mudança no Singleton afeta múltiplas partes da aplicação.   

👉 Exemplo: usar Singleton para guardar estado de sessão do usuário.

---

### 2. **Dificuldade em testes unitários**

- Como o Singleton fornece uma **instância única global**, é difícil substituir por mocks ou fakes em testes.
    
- Muitas vezes você acaba com testes que **dependem de estado compartilhado**, criando inconsistências.    

👉 Exemplo: Singleton para gerenciar conexões de banco → vários testes acabam “brigando” pela mesma instância.

---

### 3. **Abuso para resolver qualquer dependência**

- Sempre que há dúvida sobre onde colocar algo, joga-se no Singleton.

- Isso gera classes **inchadas e com múltiplas responsabilidades**, quebrando o **SRP (Single Responsibility Principle)**.    

👉 Exemplo: um `ConfigManager` Singleton que guarda configs, faz logs, inicializa cache e conecta no banco.

---

### 4. **Problemas de concorrência**

- Em ambientes multi-thread, um Singleton mal implementado pode gerar **condições de corrida**.    

- A tentativa de resolver isso com `synchronized` em excesso pode causar **gargalos de performance**.    

👉 Exemplo: Singleton criado com _lazy initialization_ sem double-checked locking.

---

### 5. **Dificulta evolução do sistema**

- Como o Singleton é “único por natureza”, se no futuro você precisar de **múltiplas instâncias** (ex: múltiplas conexões a diferentes bancos), terá que **reescrever o código**.
    

👉 Exemplo: `DatabaseConnectionSingleton` → depois a empresa passa a usar **dois bancos diferentes** e a arquitetura quebra.

---
## 🔗 Links úteis
- [Refactoring.Guru – Singleton](https://refactoring.guru/pt-br/design-patterns/singleton) → Explicação detalhada com exemplos em várias linguagens.  
- [Wikipedia – Singleton Pattern](https://en.wikipedia.org/wiki/Singleton_pattern) → Visão geral, história e variações do padrão.  
- [Baeldung – Singleton in Java](https://www.baeldung.com/java-singleton) → Exemplos práticos de implementação em Java, incluindo Enum e Double-Checked Locking.  
- [GeeksforGeeks – Singleton Design Pattern](https://www.geeksforgeeks.org/singleton-design-pattern/) → Abordagem simplificada com prós e contras.  
- [DZone – When to Avoid the Singleton Pattern](https://dzone.com/articles/why-singleton-pattern-is-bad) → Discussão crítica sobre quando **não** usar o padrão.
---
