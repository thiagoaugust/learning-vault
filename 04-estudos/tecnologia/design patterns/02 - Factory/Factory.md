## 📖 Definição
O **Factory Method** é um padrão de design criacional que define uma interface para criar objetos, mas permite que as subclasses decidam **qual classe instanciar**.  
O objetivo é **desacoplar o código cliente da lógica de criação** dos objetos, facilitando extensões e manutenções.

## 📝 Resumo rápido

O Factory Method **desacopla o cliente da criação de objetos**, permitindo que subclasses escolham qual instância fornecer.  
É útil quando há **múltiplas variações de um mesmo tipo** de objeto e queremos **flexibilidade sem alterar o código cliente**.

---
## 🔄 Variações

- [[Simple Factory]]: encapsula a lógica de criação em um único método estático (não é considerado um “padrão oficial” pelo GoF, mas é bastante usado).
    
- [[Factory Method]]: delega a decisão de criação para subclasses, permitindo maior flexibilidade e extensibilidade.
    
- [[Abstract Factory]]: cria **famílias de objetos relacionados**, garantindo consistência entre eles.    

---
## 📌 Pontos de atenção

- Pode aumentar a **complexidade do código** ao introduzir várias subclasses.
    
- Traz flexibilidade quando se espera **muitas variações de objetos**.
    
- Ajuda a aplicar o **Princípio Aberto-Fechado (OCP)**, já que novas classes podem ser adicionadas sem modificar o código cliente.   

---
## ✅ Quando faz sentido

- Quando o número de variações **pode crescer ao longo do tempo**.
    
- Quando queremos aplicar **OCP (Open-Closed Principle)**, permitindo que novas classes sejam adicionadas sem alterar o cliente.
    
- Quando a lógica de criação é complexa e precisa ser isolada.