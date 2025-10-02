# 📝 Aula: Variáveis e Constantes em JavaScript

## 📚 **Visão Geral da Aula**

### 🎯 **Objetivo:**
Aprender sobre **declaração de variáveis** e **constantes** em JavaScript, entendendo as diferenças entre `var`, `let` e `const`

---

## 🏗️ **Declaração de Variáveis**

### 🔧 **Tipos de Declaração:**

| Palavra-chave | Escopo | Hoisting | Reatribuição | Redeclaração |
|---------------|--------|----------|--------------|--------------|
| **`var`** | Function | ✅ Sim | ✅ Sim | ✅ Sim |
| **`let`** | Block | ❌ Não | ✅ Sim | ❌ Não |
| **`const`** | Block | ❌ Não | ❌ Não | ❌ Não |

### 📝 **Exemplos de Declaração:**

#### 🔄 **Variáveis com `var`:**
```javascript
var clientName;                    // Declaração sem valor (undefined)
var clientName = "customer1";      // Declaração com valor
clientName = 300;                  // Reatribuição permitida
var clientName = "novo valor";     // Redeclaração permitida
```

#### 🔄 **Variáveis com `let`:**
```javascript
let secondClientName;              // Declaração sem valor (undefined)
let secondClientName = "cliente2"; // Declaração com valor
secondClientName = 450;            // Reatribuição permitida
// let secondClientName = "erro";  // ❌ Redeclaração NÃO permitida
```

#### 🔒 **Constantes com `const`:**
```javascript
const sClient = "customer";        // ✅ Declaração obrigatória com valor
// const sClient;                  // ❌ Erro: deve ter valor
// sClient = "novo valor";        // ❌ Erro: reatribuição não permitida
```

---

## 🧪 **Demonstração Prática no Console**

### 🌐 **Acesso ao Console:**
- **Tecla**: `F12` → Aba `Console`
- **Local**: Ferramentas do Desenvolvedor do Chrome

### 💻 **Testes no Console:**

#### 1. **Teste com `var`:**
```javascript
var sClientName = "customer1";
console.log(sClientName);  // Output: "customer1"

sClientName = 300;
console.log(sClientName);  // Output: 300
```

#### 2. **Teste com `let`:**
```javascript
let customer2 = "segundo cliente";
console.log(customer2);    // Output: "segundo cliente"

customer2 = 450;
console.log(customer2);    // Output: 450
```

#### 3. **Teste com `const`:**
```javascript
const sClient = "customer";
console.log(sClient);      // Output: "customer"

// sClient = "novo valor"; // ❌ TypeError: Assignment to constant variable
```

---

## 🔄 **Conceito de Hoisting**

### 📖 **O que é Hoisting?**
- **Elevação** de declarações para o topo do escopo
- ✅ **`var`**: Sofre hoisting (é "içada")
- ❌ **`let`/`const`**: Não sofrem hoisting

### 🧪 **Exemplo Prático de Hoisting:**

#### ✅ **Com `var` (funciona):**
```javascript
// Código escrito:
showMessage = () => {
    console.log(message);      // Acesso ANTES da declaração
    var message = "Módulo 3";  // Declaração DEPOIS do uso
}
showMessage();                // Output: "Módulo 3"

// Como JavaScript interpreta:
showMessage = () => {
    var message;              // Hoisting: declaração "içada"
    console.log(message);     // Output: undefined
    message = "Módulo 3";     // Atribuição
}
```

#### ❌ **Com `let` (erro):**
```javascript
showMessageLet = () => {
    console.log(msg);         // ❌ ReferenceError: Cannot access 'msg' before initialization
    let msg = "Módulo 3";
}
showMessageLet();
```

---

## 🎯 **Escopo de Variáveis**

### 📋 **Diferenças de Escopo:**

#### 🔄 **`var` - Function Scope:**
```javascript
function exemploVar() {
    if (true) {
        var message = "Olá";  // Disponível em toda a função
    }
    console.log(message);     // ✅ Funciona: "Olá"
}
```

#### 🔄 **`let`/`const` - Block Scope:**
```javascript
function exemploLet() {
    if (true) {
        let message = "Olá";  // Disponível apenas no bloco if
        const pi = 3.14;      // Disponível apenas no bloco if
    }
    console.log(message);     // ❌ ReferenceError: message is not defined
    console.log(pi);          // ❌ ReferenceError: pi is not defined
}
```

### 🧪 **Exemplo Completo de Escopo:**
```javascript
function showMessages() {
    // var message - sofre hoisting para o topo da função
    if (true) {
        var message = "Variável var";     // ✅ Disponível em toda função
        let localMessage = "Variável let"; // ❌ Disponível apenas no bloco
    }
    
    console.log(message);        // ✅ Output: "Variável var"
    console.log(localMessage);   // ❌ ReferenceError
}
```

---

## 📝 **Boas Práticas de Nomenclatura**

### 🎨 **Padrão Camel Case:**
- ✅ **Correto**: `firstName`, `birthDate`, `totalAmount`
- ❌ **Evitar**: `first_name`, `first-name`, `FirstName`

### 📋 **Exemplos de Nomenclatura:**

| Tipo | Exemplo Correto | Exemplo Incorreto |
|------|-----------------|-------------------|
| **Variável simples** | `counter` | `Counter` |
| **Variável composta** | `fullName` | `full_name`, `full-name` |
| **Constante** | `MAX_SIZE` | `max_size`, `maxSize` |

---

## 🚫 **Palavras Reservadas**

### 📋 **Principais Palavras Reservadas:**
```javascript
// ❌ NÃO use estas palavras como nomes de variáveis:
break, case, catch, class, const, continue, debugger, default,
delete, do, else, export, extends, finally, for, function, if,
import, in, instanceof, new, return, super, switch, this, throw,
try, typeof, var, void, while, with, yield
```

### ⚠️ **Palavras Removidas (ainda evitar):**
`enum, implements, interface, let, package, private, protected, public, static`

---

## 💡 **Resumo de Recomendações**

### 🎯 **Quando Usar Cada Tipo:**

| Situação | Recomendação | Exemplo |
|----------|-------------|---------|
| **Variável mutável** | `let` | `let counter = 0;` |
| **Constante** | `const` | `const PI = 3.14;` |
| **Código legado** | `var` | `var oldVariable;` |
| **Evitar hoisting** | `let`/`const` | `let name = "João";` |

### 🛡️ **Boas Práticas:**
1. ✅ **Prefira `const`** para valores que não mudam
2. ✅ **Use `let`** para variáveis que precisam mudar
3. ❌ **Evite `var`** em código novo
4. ✅ **Siga camelCase** para nomenclatura
5. ✅ **Declare variáveis** no topo do escopo

---
*🎉 **Variáveis e constantes dominadas!** Próximo passo: explorar tipos de dados em JavaScript!*