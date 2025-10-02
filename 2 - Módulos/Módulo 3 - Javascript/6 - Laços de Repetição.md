# 🔄 Aula: Laços de Repetição em JavaScript

## 📚 **Visão Geral da Aula**

### 🎯 **Objetivo:**
Aprender sobre **laços de repetição** em JavaScript, incluindo `while`, `for` e `for...of` para iteração em arrays e objetos

---

## 🏗️ **Estruturas de Repetição em JavaScript**

### 📋 **Tipos de Laços Disponíveis:**

| Laço | Uso Principal | Sintaxe |
|------|---------------|---------|
| **`while`** | Repetição enquanto condição for verdadeira | `while (condição) { }` |
| **`for`** | Repetição com contador controlado | `for (inicialização; condição; incremento) { }` |
| **`for...of`** | Iteração em elementos de arrays | `for (elemento of array) { }` |
| **`for...in`** | Iteração em propriedades de objetos | `for (propriedade in objeto) { }` |

---

## 🔄 **Laço WHILE**

### 📝 **Sintaxe:**
```javascript
while (condição) {
    // Código a ser repetido
    // Atualização da condição
}
```

### 🧪 **Exemplo Prático no Console:**

```javascript
let counter = 10;

while (counter <= 10) {
    console.log("Valor do contador:", counter);
    counter++;
}
// Output: "Valor do contador: 10"
```

### 💡 **Exemplo Mais Completo:**
```javascript
let contador = 1;

while (contador <= 5) {
    console.log(`Iteração número: ${contador}`);
    contador++;
}
// Output:
// "Iteração número: 1"
// "Iteração número: 2"
// "Iteração número: 3"
// "Iteração número: 4"
// "Iteração número: 5"
```

---

## 🔢 **Laço FOR**

### 📝 **Sintaxe:**
```javascript
for (inicialização; condição; incremento) {
    // Código a ser repetido
}
```

### 🧪 **Exemplo Prático no Console:**

```javascript
for (let i = 0; i < 10; i++) {
    console.log("Valor de i:", i);
}
// Output: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
```

### 🔍 **Anatomia do FOR:**

| Parte | Descrição | Exemplo |
|-------|-----------|---------|
| **Inicialização** | Executada UMA vez no início | `let i = 0` |
| **Condição** | Verificada ANTES de cada iteração | `i < 10` |
| **Incremento** | Executada APÓS cada iteração | `i++` |

### 💡 **Exemplos Adicionais:**

#### 🔽 **Contagem Regressiva:**
```javascript
for (let i = 5; i > 0; i--) {
    console.log(`Contagem: ${i}`);
}
// Output: 5, 4, 3, 2, 1
```

#### 🔼 **Incremento Personalizado:**
```javascript
for (let i = 0; i <= 20; i += 2) {
    console.log(`Número par: ${i}`);
}
// Output: 0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20
```

---

## 🎯 **Laço FOR...OF**

### 📝 **Sintaxe:**
```javascript
for (elemento of array) {
    // Código para cada elemento
}
```

### 🧪 **Exemplo Prático no Console:**

```javascript
let names = ["Amir", "Bruno", "Caio"];

for (let name of names) {
    console.log("Nome:", name);
}
// Output:
// "Nome: Amir"
// "Nome: Bruno" 
// "Nome: Caio"
```

### 💡 **Vantagens do FOR...OF:**

- ✅ **Mais simples** que FOR tradicional
- ✅ **Acesso direto** aos elementos
- ✅ **Não precisa** controlar índices
- ✅ **Funciona com** strings, arrays, etc.

### 🔧 **Mais Exemplos:**

#### 📝 **Iteração em String:**
```javascript
let palavra = "JavaScript";

for (let letra of palavra) {
    console.log(letra);
}
// Output: J, a, v, a, S, c, r, i, p, t
```

#### 🛒 **Iteração em Array de Objetos:**
```javascript
let produtos = [
    { nome: "Notebook", preco: 2500 },
    { nome: "Mouse", preco: 89.90 },
    { nome: "Teclado", preco: 150 }
];

for (let produto of produtos) {
    console.log(`${produto.nome}: R$ ${produto.preco}`);
}
// Output:
// "Notebook: R$ 2500"
// "Mouse: R$ 89.90"
// "Teclado: R$ 150"
```

---

## 🔄 **Comparação entre os Laços**

### 🧪 **Mesma Tarefa com Diferentes Laços:**

#### **Array para Iterar:**
```javascript
let frutas = ["maçã", "banana", "laranja", "uva"];
```

#### **Com FOR tradicional:**
```javascript
for (let i = 0; i < frutas.length; i++) {
    console.log(`Fruta ${i + 1}: ${frutas[i]}`);
}
```

#### **Com FOR...OF:**
```javascript
for (let fruta of frutas) {
    console.log(`Fruta: ${fruta}`);
}
```

#### **Com WHILE:**
```javascript
let i = 0;
while (i < frutas.length) {
    console.log(`Fruta ${i + 1}: ${frutas[i]}`);
    i++;
}
```

---

## 💡 **Casos de Uso Práticos**

### 🛒 **Exemplo: Carrinho de Compras**
```javascript
let carrinho = [
    { produto: "Camiseta", preco: 29.99, quantidade: 2 },
    { produto: "Calça", preco: 89.90, quantidade: 1 },
    { produto: "Tênis", preco: 199.99, quantidade: 1 }
];

// Calcular total com FOR...OF
let total = 0;
for (let item of carrinho) {
    total += item.preco * item.quantidade;
}
console.log(`Total do carrinho: R$ ${total.toFixed(2)}`);
```

### 📊 **Exemplo: Análise de Dados**
```javascript
let notas = [7.5, 8.0, 6.5, 9.0, 7.0, 8.5];

// Encontrar maior nota com FOR
let maiorNota = notas[0];
for (let i = 1; i < notas.length; i++) {
    if (notas[i] > maiorNota) {
        maiorNota = notas[i];
    }
}
console.log(`Maior nota: ${maiorNota}`);

// Calcular média com FOR...OF
let soma = 0;
for (let nota of notas) {
    soma += nota;
}
let media = soma / notas.length;
console.log(`Média: ${media.toFixed(2)}`);
```

---

## ⚠️ **Cuidados e Boas Práticas**

### 🚨 **Problemas Comuns:**

#### **Loop Infinito com WHILE:**
```javascript
// ❌ CUIDADO - Loop infinito!
let i = 0;
while (i < 5) {
    console.log(i);
    // Esqueceu de incrementar i!
}
```

#### **Solução Correta:**
```javascript
// ✅ CORRETO
let i = 0;
while (i < 5) {
    console.log(i);
    i++; // Não esqueça do incremento!
}
```

### ✅ **Boas Práticas:**

1. **Use `for...of`** para arrays quando não precisa do índice
2. **Use `for` tradicional** quando precisa controlar o índice
3. **Use `while`** quando não sabe quantas iterações serão necessárias
4. **Sempre teste** condições para evitar loops infinitos
5. **Use nomes descritivos** para variáveis de iteração

### 🔧 **Exemplo de Código Seguro:**
```javascript
function processarLista(items) {
    // Verificar se array não está vazio
    if (!items || items.length === 0) {
        console.log("Lista vazia");
        return;
    }
    
    // Processar com for...of (mais seguro)
    for (let item of items) {
        if (item && item.nome) {
            console.log(`Processando: ${item.nome}`);
        }
    }
}
```

---
*🎯 **Laços de repetição dominados!** Próximo passo: explorar funções em JavaScript!*