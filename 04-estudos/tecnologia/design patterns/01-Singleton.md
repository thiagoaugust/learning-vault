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
