# 🔢 Aula: Números e Operadores Aritméticos em JavaScript

## 📚 **Visão Geral da Aula**

### 🎯 **Objetivo:**
Aprender sobre **tipos numéricos** e **operadores aritméticos** em JavaScript, incluindo funções úteis para manipulação de números

---

## 🏗️ **Tipos de Números em JavaScript**

### 📋 **Categorias Numéricas:**

| Tipo | Descrição | Exemplo |
|------|-----------|---------|
| **Inteiros** | Números sem casa decimal | `10`, `-5`, `1000` |
| **Ponto Flutuante** | Números com casa decimal | `3.14`, `-2.5`, `0.1` |
| **Notação Científica** | Números muito grandes/pequenos | `1e6` (1.000.000), `2.5e-3` (0.0025) |

### 💻 **Exemplos Práticos:**
```javascript
let inteiro = 10;
let float = 3.14;
let cientifico = 2.5e6;  // 2.500.000
let negativo = -15.75;
```

---

## 🛠️ **Funções Úteis para Números**

### 🔧 **toFixed() - Formatação de Casas Decimais**

#### 📝 **Sintaxe:**
```javascript
numero.toFixed(casasDecimais)
```

#### 🧪 **Exemplo no Console:**
```javascript
let nValue = 10;
console.log(nValue.toFixed(2));  // Output: "10.00"

let preco = 19.99;
console.log(preco.toFixed(1));   // Output: "20.0"
```

#### ⚠️ **Importante:**
- ✅ **Retorna uma string**, não um número
- 🔄 **Arredonda** automaticamente
- 📝 **Útil para** formatação de moedas, porcentagens

### 🔍 **isNaN() - Verificação se NÃO é Número**

#### 📝 **Sintaxe:**
```javascript
isNaN(valor)
```

#### 🧪 **Exemplos Práticos:**
```javascript
let numero = 10;
console.log(isNaN(numero));      // Output: false (É um número)

let texto = "JavaScript";
console.log(isNaN(texto));       // Output: true (NÃO é um número)

let numeroString = "123";
console.log(isNaN(numeroString)); // Output: false (É convertível para número)
```

#### 💡 **Uso em Validações:**
```javascript
function validarCalculo(a, b) {
    if (isNaN(a) || isNaN(b)) {
        console.log("Erro: Valores devem ser números!");
        return;
    }
    return a + b;
}
```

---

## ➕ **Operadores Aritméticos**

### 📋 **Operadores Básicos:**

| Operador | Nome | Exemplo | Resultado |
|----------|------|---------|-----------|
| `+` | Adição | `5 + 3` | `8` |
| `-` | Subtração | `10 - 4` | `6` |
| `*` | Multiplicação | `3 * 4` | `12` |
| `/` | Divisão | `15 / 3` | `5` |
| `%` | Módulo (Resto) | `10 % 3` | `1` |
| `**` | Exponenciação | `2 ** 3` | `8` |

### 🔄 **Operadores de Incremento/Decremento:**

| Operador | Nome | Exemplo | Equivalente |
|----------|------|---------|-------------|
| `++` | Incremento | `x++` | `x = x + 1` |
| `--` | Decremento | `x--` | `x = x - 1` |

#### 🧪 **Exemplos:**
```javascript
let contador = 5;
contador++;    // contador agora é 6
contador--;    // contador volta para 5
```

---

## 🎯 **Operadores de Atribuição Aritmética**

### 📋 **Operadores Combinados:**

| Operador | Exemplo | Equivalente | Descrição |
|----------|---------|-------------|-----------|
| `+=` | `x += 5` | `x = x + 5` | Soma e atribui |
| `-=` | `x -= 3` | `x = x - 3` | Subtrai e atribui |
| `*=` | `x *= 2` | `x = x * 2` | Multiplica e atribui |
| `/=` | `x /= 4` | `x = x / 4` | Divide e atribui |
| `%=` | `x %= 3` | `x = x % 3` | Módulo e atribui |

### 🧪 **Exemplos Práticos:**
```javascript
let saldo = 100;

saldo += 50;   // saldo = 150
saldo -= 30;   // saldo = 120
saldo *= 2;    // saldo = 240
saldo /= 4;    // saldo = 60
```

---

## 🔄 **Demonstração Interativa no Console**

### 💻 **Teste Completo:**
```javascript
// Declaração de variáveis
let nValue = 10;
let precoProduto = 29.99;
let texto = "JavaScript";

// Teste toFixed()
console.log("toFixed(2):", nValue.toFixed(2));        // "10.00"
console.log("Preco formatado:", precoProduto.toFixed(2)); // "29.99"

// Teste isNaN()
console.log("10 é NaN?", isNaN(nValue));             // false
console.log("Texto é NaN?", isNaN(texto));           // true
console.log("'123' é NaN?", isNaN("123"));           // false

// Operações aritméticas
console.log("Soma:", 10 + 5);                        // 15
console.log("Subtração:", 20 - 8);                   // 12
console.log("Multiplicação:", 6 * 7);                // 42
console.log("Divisão:", 15 / 3);                     // 5
console.log("Resto:", 10 % 3);                       // 1

// Operadores de atribuição
let total = 100;
total += 25;    // total = 125
console.log("Total após += 25:", total);
```

---

## 💡 **Casos de Uso Práticos**

### 🛒 **Exemplo: Cálculo de Carrinho de Compras**
```javascript
function calcularTotal(itens, taxa) {
    let subtotal = 0;
    
    // Validar se todos os valores são números
    if (isNaN(taxa)) {
        return "Erro: Taxa inválida!";
    }
    
    // Calcular subtotal
    for (let item of itens) {
        if (isNaN(item.preco)) {
            return "Erro: Preço inválido encontrado!";
        }
        subtotal += item.preco;
    }
    
    // Calcular total com taxa
    let total = subtotal + (subtotal * taxa);
    
    // Retornar formatado
    return "Total: R$ " + total.toFixed(2);
}

// Uso
let carrinho = [
    { nome: "Produto A", preco: 29.99 },
    { nome: "Produto B", preco: 15.50 }
];

console.log(calcularTotal(carrinho, 0.1)); // "Total: R$ 50.04"
```

### 📊 **Exemplo: Contador com Validação**
```javascript
let contador = 0;

function incrementarContador(valor) {
    if (isNaN(valor)) {
        console.log("Valor deve ser um número!");
        return;
    }
    contador += valor;
    console.log("Contador:", contador);
}

incrementarContador(5);   // Contador: 5
incrementarContador("abc"); // "Valor deve ser um número!"
```

---

## ⚠️ **Cuidados e Boas Práticas**

### 🚨 **Problemas Comuns:**
```javascript
// Cuidado com concatenação vs soma
console.log("10" + 5);    // "105" (concatenação)
console.log("10" - 5);    // 5 (subtração converte)

// Sempre validar entradas numéricas
function dividir(a, b) {
    if (isNaN(a) || isNaN(b)) {
        return "Entradas inválidas";
    }
    if (b === 0) {
        return "Divisão por zero";
    }
    return a / b;
}
```

### ✅ **Boas Práticas:**
1. 🛡️ **Sempre validar** entradas com `isNaN()`
2. 💰 **Usar `toFixed()`** para formatação monetária
3. 🔄 **Prefira `+=`** em vez de `x = x + valor`
4. 📝 **Documentar** operações complexas

---
*🎯 **Números e operadores dominados!** Próximo passo: explorar strings e manipulação de texto em JavaScript!*