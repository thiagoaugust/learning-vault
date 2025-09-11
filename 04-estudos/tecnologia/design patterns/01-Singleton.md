# 🟦 Design Pattern: Singleton

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
    
- Dificulta testes unitários, pois a instância global é difícil de isolar/mocar.
    
- Deve ser aplicado somente quando realmente faz sentido ter **uma única instância**.
    

---

## 🔗 Links úteis

- Refactoring.Guru – Singleton
    
- Wikipedia – Singleton
    

---

## 📝 Resumo rápido

O Singleton garante **uma única instância global** de uma classe.  
É útil para gerenciar recursos compartilhados (ex: configurações, logs, conexões), mas deve ser usado com cautela para evitar mau uso como anti-pattern.