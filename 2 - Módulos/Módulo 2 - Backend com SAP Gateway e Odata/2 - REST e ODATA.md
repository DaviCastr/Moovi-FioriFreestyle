# 📚 Aula: REST e OData - Conceitos Fundamentais

## 🌐 **Web Services: Conceito Básico**

### 🔄 O que são Web Services?
- **Conjunto de métodos** acessados por diversas plataformas e tecnologias
- **Permitem troca de informações** entre sistemas diferentes
- **Protocolo de comunicação comum** entre sistemas

### 🏢 **Exemplos Práticos:**
```
Sistema ABAP (legado) ↔ Sistema .NET
```
```
Sistema Empresarial ↔ Web Service da SEFAZ (Nota Fiscal)
```

### ⚡ **Características:**
- 🤝 Comunicação via **HTTP/HTTPS**
- 📨 Mensagens **XML** (no caso SOAP)
- 🔄 Acesso por qualquer tecnologia com biblioteca HTTP

---

## 🏗️ **Arquitetura REST**

### 📋 **REST - Representational State Transfer**
- **Transferência de Estado Representacional**
- **Arquitetura stateless** (não armazena estado)

### ⚡ **Características Principais:**

#### 🔄 **Stateless**
- ❌ **Não armazena histórico** de chamadas
- 🔌 Se conexão cai, precisa **refazer a chamada**
- ⏱️ Resposta **síncrona**

#### 👥 **Client-Server**
- 🖥️ Servidor: publica o serviço
- 📱 Cliente: consome o serviço

#### 🎯 **Interface Uniforme**
- ✅ **Padrão único** para construção de serviços
- 🔗 **Mesmo endpoint** para múltiplas operações

---

## 🛠️ **Operações REST (CRUD)**

| Método HTTP | Operação | Descrição |
|------------|----------|-----------|
| **GET** 🔍 | Read | Busca/consulta de dados |
| **POST** ➕ | Create | Criação de novos registros |
| **PUT** ✏️ | Update | Atualização de informações |
| **DELETE** 🗑️ | Delete | Exclusão de registros |

### 💡 **Vantagem:**
- **Um endpoint único** para todas as operações CRUD
- **Diferente do SOAP** que precisa de endpoint para cada método

---

## 🎯 **Estrutura de URL REST**

### 🔗 **Componentes da URL:**
```
https://servidor.com/api/v1/categorias(1)/produtos?$top=2&$orderby=nome
```

| Componente | Exemplo | Descrição |
|------------|---------|-----------|
| **Service Root** 🌱 | `https://servidor.com/api/v1` | Raiz do serviço |
| **Recurso** 📁 | `categorias` | Entidade/coleção |
| **Chave** 🔑 | `(1)` | Identificador único |
| **Navegação** 🧭 | `/produtos` | Relacionamento entre entidades |
| **Query Options** ⚙️ | `?$top=2&$orderby=nome` | Filtros e ordenação |

---

## 🔄 **REST vs RESTful**

### 📖 **REST**
- ✅ **Conjunto de princípios** da arquitetura
- 📋 **Define a interface** e protocolo

### 🎯 **RESTful**
- ✅ **Sistema que aplica** os princípios REST
- 🚫 **Cada método faz APENAS** sua função designada

### ❌ **Violação dos Princípios:**
- ⚠️ GET realizando UPDATE
- ⚠️ GET realizando CREATE
- ⚠️ Métodos com funcionalidades mistas

---

## 📊 **OData (Open Data Protocol)**

### 🌟 **O que é OData?**
- **Protocolo aberto** para APIs REST
- Desenvolvido pela **Microsoft** em conjunto com outras empresas
- **Padronizado** para operações CRUD

### 🛠️ **Tecnologias Base:**
- 🌐 **HTTP/HTTPS**
- 📄 **XML**
- 📋 **JSON** (JavaScript Object Notation)

### 🎯 **Ideal para:**
- ✅ **Sistemas que operam CRUD**
- ✅ **Aplicações que precisam** de operações padronizadas

---

## 🏗️ **Componentes OData**

### 📋 **Modelo de Dados (Metadados)**
```xml
<!-- Exemplo de metadados OData -->
<EntityType Name="Produto">
    <Property Name="ID" Type="Edm.Int32" Nullable="false"/>
    <Property Name="Nome" Type="Edm.String" MaxLength="100"/>
    <Property Name="Preco" Type="Edm.Decimal" Precision="10" Scale="2"/>
</EntityType>
```

### 🔧 **Elementos do Modelo:**

#### 📦 **Entity Set**
- 📚 **Coleções** de recursos
- 🗂️ Listas de entidades

#### 🔗 **Navigation Property**
- 🧭 **Links** entre entidades relacionadas
- 🔄 Ex: Categoria → Produtos

#### 🤝 **Association**
- 🔗 **Relacionamentos** entre entidades
- 📊 Define como entidades se conectam

#### 🎯 **Entity Type**
- 📝 **Estrutura** de um objeto único
- 🔑 **Chave obrigatória** para identificação

---

## 💻 **Exemplos Práticos OData**

### 🔍 **Consultas Básicas:**

#### 1. **Buscar todas as categorias**
```http
GET /api/v1/categorias
```

#### 2. **Buscar categoria específica**
```http
GET /api/v1/categorias(1)
```

#### 3. **Buscar produtos de uma categoria**
```http
GET /api/v1/categorias(1)/produtos
```

#### 4. **Buscar propriedade específica**
```http
GET /api/v1/categorias(1)/nome
```

### ⚙️ **Query Options:**
| Operação | Sintaxe | Descrição |
|----------|---------|-----------|
| **Filtro** | `$filter=preco gt 100` | Filtra registros |
| **Ordenação** | `$orderby=nome` | Ordena resultados |
| **Paginação** | `$top=10&$skip=20` | Controla paginação |
| **Seleção** | `$select=nome,preco` | Busca apenas campos específicos |

---

## 🎓 **Resumo dos Conceitos Chave**

### 🌐 **Web Service**
- 🤝 **Ponte entre sistemas** diferentes
- 🔄 **Protocolo comum** de comunicação

### 🏗️ **REST**
- 🎯 **Arquitetura stateless**
- 🔄 **Interface uniforme**
- 🛠️ **Operações HTTP padrão**

### 📊 **OData**
- ✅ **Protocolo padronizado** para REST
- 📋 **Metadados** ricos
- 🔧 **Operações CRUD** consistentes

---

## 🚀 **Próximos Passos**
> 💡 **Na próxima aula:** Criação do primeiro serviço OData no SAP Gateway que servirá de base para o projeto do treinamento!

---
*📝 Anotações criadas com base na aula do professor Paulinho Silva sobre REST e OData*