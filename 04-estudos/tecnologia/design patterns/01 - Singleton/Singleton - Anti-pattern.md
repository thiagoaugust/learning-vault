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
