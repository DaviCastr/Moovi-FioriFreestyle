# 📝 Aula: Strings, Booleanos e Arrays em JavaScript

## 📚 **Visão Geral da Aula**

### 🎯 **Objetivo:**
Aprender sobre **strings**, **booleanos** e **arrays** em JavaScript, incluindo métodos úteis e manipulação de dados

---

## 🔤 **Strings em JavaScript**

### 📋 **Declaração de Strings:**

| Tipo | Sintaxe | Exemplo |
|------|---------|---------|
| **Aspas Simples** | `'texto'` | `'JavaScript'` |
| **Aspas Duplas** | `"texto"` | `"Programação"` |
| **Template Literals** | `` `texto` `` | `` `Olá ${nome}` `` |

### 🛠️ **Propriedades e Métodos Úteis:**

#### 📏 **Propriedade Length:**
```javascript
let texto = "JavaScript";
console.log(texto.length);  // Output: 10
```

#### 🔍 **Métodos de Busca:**
```javascript
let frase = "Aprenda JavaScript";

// indexOf - encontra posição
console.log(frase.indexOf("Java"));  // Output: 8

// includes - verifica se contém
console.log(frase.includes("Script")); // Output: true
```

#### ✂️ **Métodos de Manipulação:**
```javascript
let texto = "Hello World";

// replace - substitui texto
console.log(texto.replace("World", "JavaScript")); // "Hello JavaScript"

// toUpperCase/toLowerCase - muda caso
console.log(texto.toUpperCase());  // "HELLO WORLD"
console.log(texto.toLowerCase());  // "hello world"

// substring - extrai parte do texto
console.log(texto.substring(0, 5)); // "Hello"
```

#### 🪓 **Split - Divisão de Strings:**
```javascript
let csv = "João,25,Desenvolvedor,São Paulo";
let dados = csv.split(",");
console.log(dados); // ["João", "25", "Desenvolvedor", "São Paulo"]

let linhas = "linha1\nlinha2\nlinha3";
let arrayLinhas = linhas.split("\n");
console.log(arrayLinhas); // ["linha1", "linha2", "linha3"]
```

#### 🔄 **Conversão de Tipos:**
```javascript
// String para Inteiro
let numeroString = "123";
let numeroInt = parseInt(numeroString);
console.log(numeroInt); // 123

// String para Float
let decimalString = "3.14";
let numeroFloat = parseFloat(decimalString);
console.log(numeroFloat); // 3.14
```

---

## ✅ **Booleanos em JavaScript**

### 📋 **Valores Booleanos:**
- ✅ **true** - Verdadeiro
- ❌ **false** - Falso

### 🔄 **Valores que Convertem para False (Falsy):**

| Valor | Tipo | Descrição |
|-------|------|-----------|
| `false` | Boolean | Valor booleano false |
| `0` | Number | Zero |
| `""` | String | String vazia |
| `null` | Object | Valor nulo |
| `undefined` | Undefined | Não definido |
| `NaN` | Number | Não é um número |

### 🧪 **Demonstração no Console:**

```javascript
// Testando valores falsy
let sText = null;
let sVar2; // undefined

if (!sText) {
    console.log("sText é falso"); // ✅ Será executado
}

if (!sVar2) {
    console.log("sVar2 é falso"); // ✅ Será executado
}

if (sText) {
    console.log("sText é verdadeiro"); // ❌ NÃO será executado
}
```

### 💡 **Uso Prático em Validações:**
```javascript
function validarUsuario(usuario) {
    if (!usuario.nome) {
        return "Nome é obrigatório";
    }
    if (!usuario.idade) {
        return "Idade é obrigatória";
    }
    return "Usuário válido";
}

// Teste
let usuario1 = { nome: "", idade: 25 };
console.log(validarUsuario(usuario1)); // "Nome é obrigatório"

let usuario2 = { nome: "João", idade: 0 };
console.log(validarUsuario(usuario2)); // "Idade é obrigatória"
```

---

## 🗃️ **Arrays em JavaScript**

### 📋 **Declaração de Arrays:**

```javascript
// Array com tipos mistos
let meuArray = ["elemento", 2, false];

// Array homogêneo
let numeros = [1, 2, 3, 4, 5];
let nomes = ["Ana", "João", "Maria"];
```

### 🛠️ **Propriedades e Métodos Úteis:**

#### 📏 **Propriedade Length:**
```javascript
let arr = [10, 20, 30];
console.log(arr.length); // Output: 3
```

#### 🔍 **Acesso a Elementos:**
```javascript
let arr = ["primeiro", "segundo", "terceiro"];

console.log(arr[0]); // "primeiro" - índice 0
console.log(arr[1]); // "segundo"  - índice 1  
console.log(arr[2]); // "terceiro" - índice 2
```

#### 🗑️ **Método Pop - Remove Último Elemento:**
```javascript
let arr = [1, 2, 3];
let ultimoElemento = arr.pop();

console.log(ultimoElemento); // 3
console.log(arr); // [1, 2] - array modificado
```

#### ➕ **Método Push - Adiciona Elemento:**
```javascript
let arr = [1, 2, 3];
arr.push(4);
arr.push(true);
arr.push("novo elemento");

console.log(arr); // [1, 2, 3, 4, true, "novo elemento"]
```

### 🔧 **Outros Métodos Úteis de Arrays:**

#### 🔄 **Métodos de Manipulação:**
```javascript
let frutas = ["maçã", "banana", "laranja"];

// shift - remove primeiro elemento
let primeiraFruta = frutas.shift();
console.log(primeiraFruta); // "maçã"
console.log(frutas); // ["banana", "laranja"]

// unshift - adiciona no início
frutas.unshift("uva");
console.log(frutas); // ["uva", "banana", "laranja"]

// splice - adiciona/remove elementos
frutas.splice(1, 1, "morango"); // Remove 1 elemento na posição 1, adiciona "morango"
console.log(frutas); // ["uva", "morango", "laranja"]
```

#### 🔍 **Métodos de Busca:**
```javascript
let numeros = [10, 20, 30, 40, 50];

// find - encontra elemento
let maiorQue25 = numeros.find(num => num > 25);
console.log(maiorQue25); // 30

// filter - filtra elementos
let pares = numeros.filter(num => num % 2 === 0);
console.log(pares); // [10, 20, 30, 40, 50]
```

---

## 🧪 **Demonstração Interativa no Console**

### 💻 **Teste Completo:**
```javascript
// STRINGS
let texto = "JavaScript é incrível";
console.log("Length:", texto.length);
console.log("UpperCase:", texto.toUpperCase());
console.log("Replace:", texto.replace("incrível", "poderoso"));
console.log("Split:", texto.split(" "));

// BOOLEANOS
let valorNulo = null;
let valorUndefined;
let valorZero = 0;
let valorVazio = "";

console.log("null é false?", !valorNulo);
console.log("undefined é false?", !valorUndefined);
console.log("0 é false?", !valorZero);
console.log("string vazia é false?", !valorVazio);

// ARRAYS
let meuArray = ["elemento", 2, false];
console.log("Array length:", meuArray.length);
console.log("Primeiro elemento:", meuArray[0]);

meuArray.pop();
console.log("Após pop:", meuArray);

meuArray.push("novo elemento");
console.log("Após push:", meuArray);
```

---

## 💡 **Casos de Uso Práticos**

### 🛒 **Exemplo: Carrinho de Compras**
```javascript
let carrinho = [];

function adicionarProduto(nome, preco) {
    if (!nome || !preco) {
        console.log("Nome e preço são obrigatórios!");
        return;
    }
    carrinho.push({ nome, preco });
    console.log(`Produto ${nome} adicionado!`);
}

function calcularTotal() {
    let total = 0;
    for (let produto of carrinho) {
        total += produto.preco;
    }
    return total.toFixed(2);
}

// Uso
adicionarProduto("Notebook", 2500.00);
adicionarProduto("Mouse", 89.90);
console.log("Total: R$", calcularTotal());
```

### 📊 **Exemplo: Processamento de Dados CSV**
```javascript
function processarCSV(dadosCSV) {
    if (!dadosCSV) {
        return "Dados inválidos";
    }
    
    let linhas = dadosCSV.split("\n");
    let resultado = [];
    
    for (let linha of linhas) {
        let campos = linha.split(",");
        if (campos.length === 3) {
            resultado.push({
                nome: campos[0].trim(),
                idade: parseInt(campos[1]),
                cidade: campos[2].trim()
            });
        }
    }
    
    return resultado;
}

// Uso
let csvData = "João,30,São Paulo\nMaria,25,Rio de Janeiro\nPedro,35,Belo Horizonte";
console.log(processarCSV(csvData));
```

---
*🎯 **Strings, booleanos e arrays dominados!** Próximo passo: explorar objetos e funções em JavaScript!*