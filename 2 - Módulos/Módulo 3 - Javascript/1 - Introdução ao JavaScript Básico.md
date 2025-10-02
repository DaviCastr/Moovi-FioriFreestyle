# 🌟 Aula: Introdução ao JavaScript Básico

## 📚 **Visão Geral do Módulo**

### 🎯 **Objetivo do Módulo:**
Aprender os **conceitos fundamentais** do JavaScript que serão a base para o desenvolvimento de aplicações **SAP Fiori**

---

## 🔍 **História do JavaScript**

### 📅 **Origem e Evolução:**

| Ano | Marco Histórico | Detalhes |
|-----|----------------|----------|
| **1995** | 🎯 Criação por **Brendan Eich** | Desenvolvido em **10 dias** |
| **1995** | 🌐 Navegador **Netscape Navigator 2.0** | Primeira implementação |
| **1996** | 🔄 Nomes: **Mocha → LiveScript → JavaScript** | Evolução da nomenclatura |
| **1996** | 📝 Padronização **ECMA** | Especificação ECMAScript |
| **1996** | 💻 Microsoft adota | Internet Explorer 3.0 |

### ⚠️ **Importante:**
- ❌ **JavaScript ≠ Java** - Linguagens completamente diferentes
- ✅ **JavaScript**: Linguagem interpretada
- 🌐 **Roda no client** (navegador) e **server** (Node.js)

---

## 🏗️ **Padrão ECMAScript**

### 📋 **O que é ECMAScript?**
- 🏢 **ECMA**: European Computer Manufacturers Association
- 📝 **Especificação** que define a sintaxe JavaScript
- 🎯 **Padroniza** palavras-chave, estruturas, funcionalidades

### 🔧 **Benefícios:**
- ✅ **Consistência** entre navegadores
- 📚 **Documentação** oficial
- 🔄 **Evolução** contínua da linguagem

---

## 💼 **Por que Aprender JavaScript?**

### 🚀 **Aplicações no Mercado:**

#### 📱 **Frontend:**
- 🌐 **Aplicações Web** modernas
- 📱 **SAP Fiori** e Fiori Freestyle
- 🎨 **Interatividade** em páginas web

#### ⚙️ **Backend:**
- 🔧 **Node.js** - JavaScript no servidor
- ☁️ **SAP Cloud Applications**
- 🔗 **APIs** e serviços web

### 📊 **Demanda do Mercado:**
- 👥 **Desenvolvedores JavaScript** muito requisitados
- 💡 **Habilidade essencial** para Fiori
- 🏢 **Grande comunidade** e recursos

---

## 🛠️ **Ambientes de Desenvolvimento**

### 💻 **Editores e IDEs:**

| Ferramenta | Tipo | Uso |
|------------|------|-----|
| **Visual Studio Code** | 🖥️ Desktop | ⭐ Mais popular |
| **Eclipse** | 🖥️ Desktop | 🏢 Corporativo |
| **WebStorm** | 🖥️ Desktop | 💼 Profissional |
| **Business Application Studio** | 🌐 Nuvem | ☁️ SAP Cloud |
| **Editores Online** | 🌐 Navegador | 🔧 Prototipagem rápida |

### 🌐 **Business Application Studio:**
- ☁️ **IDE na nuvem** da SAP
- 🔗 **Acesso via navegador**
- 📱 **Otimizado** para desenvolvimento Fiori

---

## 🎯 **Primeiro Exemplo: "Hello World" Interativo**

### 🔧 **Demonstração Prática:**

#### 🌐 **Cenário:**
Modificar o texto do site **SAP.com** usando JavaScript puro

#### 🛠️ **Ferramentas:**
- **Navegador**: Google Chrome
- **Acesso**: Tecla **F12** → Ferramentas do Desenvolvedor

### 💻 **Código Executado:**

#### 1. **Selecionar Elemento HTML:**
```javascript
// Acessa elemento H1 da página
document.getElementsByTagName('H1')[0]
```

#### 2. **Modificar Texto:**
```javascript
// Altera o conteúdo de texto
document.getElementsByTagName('H1')[0].innerText = "Olá mundo com JavaScript!"
```

#### 3. **Modificar Estilo (CSS):**
```javascript
// Altera a cor para vermelho
document.getElementsByTagName('H1')[0].style.color = "red"
```

### 📋 **Passo a Passo no Console:**

1. **Abrir Ferramentas**: `F12` → Aba `Console`
2. **Selecionar Elemento**: 
   ```javascript
   document.getElementsByTagName('H1')[0]
   ```
3. **Modificar Texto**:
   ```javascript
   document.getElementsByTagName('H1')[0].innerText = "Novo texto"
   ```
4. **Modificar Cor**:
   ```javascript
   document.getElementsByTagName('H1')[0].style.color = "red"
   ```

---

## 🎨 **Capacidades do JavaScript Demonstradas**

### ✨ **Manipulação de DOM:**
- 📝 **Conteúdo**: Modificar textos, HTML
- 🎨 **Estilo**: Alterar CSS dinamicamente
- 🖼️ **Elementos**: Imagens, formulários, etc.

### 🔧 **Recursos Avançados:**
- 🎬 **Animações** e transições
- 📊 **Validações** de formulários
- 🔄 **Comunicação** com APIs
- 💾 **Armazenamento** local

---

## 🔄 **Comportamento do JavaScript**

### ⚡ **Execução Imediata:**
- 🎯 **Código roda** instantaneamente no console
- 🔄 **Alterações visíveis** em tempo real
- 📝 **Não persistente** - refresh restaura original

### 🌐 **Contexto de Execução:**
- 🖥️ **Client-side**: No navegador do usuário
- ⚡ **Interpretado**: Executado linha por linha
- 🔒 **Sandboxed**: Segurança por restrições

---

## 📚 **Próximos Tópicos do Módulo**

### 🎯 **O que Virá:**
1. 📝 **Sintaxe básica** - variáveis, funções, estruturas
2. 🔧 **Manipulação DOM** - interação com páginas web
3. 📊 **Estruturas de dados** - arrays, objetos
4. 🔄 **Eventos** - respostas a ações do usuário
5. 🌐 **APIs** - comunicação com serviços externos

### 💡 **Aplicação em Fiori:**
- 📱 **Controllers** JavaScript em apps Fiori
- 🎨 **Manipulação** de UI5 controls
- 🔗 **Consumo** de serviços OData
- 💾 **Gestão** de modelos de dados
