# 🔗 Aula: Criação de Associations e Runtime Objects no Gateway

## 📋 **Visão Geral da Aula**

### 🎯 **Objetivo**
Criar **associações** entre entidades e gerar **objetos de runtime** para o serviço OData

---

## 🔗 **Criação da Association (Relacionamento)**

### 📝 **Passo a Passo - Criar Association**

#### 1. **Acessar Pasta de Associations**
- 📁 **Localização**: `Data Model` → `Associations`
- 🖱️ **Botão direito** → `Create`

#### 2. **Configurar Nome da Association**
- **Padrão**: `{EntidadePai}To{EntidadeFilha}`
- 📝 **Exemplo**: `ScarToSpfly`

#### 3. **Configurar Entidade Principal (SCARR)**
| Configuração | Valor | Descrição |
|-------------|-------|-----------|
| **Principal Entity** | `SCARR` | Entidade pai |
| **Cardinalidade** | `1` | Um-para-muitos |
| **Navigation Property** | `ToSpflyNav` | Nome da navegação |

#### 4. **Configurar Entidade Dependente (SPFLI)**
| Configuração | Valor | Descrição |
|-------------|-------|-----------|
| **Dependent Entity** | `SPFLI` | Entidade filha |
| **Cardinalidade** | `N` | Muitos relacionamentos |

#### 5. **Definir Vinculação das Chaves**
| Entidade | Campo | Tipo |
|----------|-------|------|
| **SCARR** | `Carrid` | 🔑 Chave principal |
| **SPFLI** | `Carrid` | 🔑 Chave estrangeira |

#### 6. **Criar Association Set**
- ✅ **Selecionar opção padrão**
- 📦 **Cria coleção** para navegação

---

## ⚡ **Geração dos Runtime Objects**

### 🔧 **Passo a Passo - Gerar Objetos**

#### 1. **Acessar Gerador**
- 🎯 **Botão**: `Generate Runtime Objects`
- 📍 **Localização**: Barra de ferramentas SEGW

#### 2. **Objetos que Serão Gerados**

| Objeto | Nome | Finalidade |
|--------|------|-----------|
| **Model Provider Class** | `Z{USUARIO}_GW_MPC` | 🏗️ Modelo e metadados |
| **Data Provider Class** | `Z{USUARIO}_GW_DPC` | 💻 Lógica de negócio |
| **Technical Model** | `Z{USUARIO}_GW_MDL` | 🔧 Modelo técnico |
| **Technical Service** | `Z{USUARIO}_GW_SRV` | 🌐 Serviço técnico |

#### 3. **Configuração do Pacote**
- 📦 **Pacote**: `ZFIORI_F` (ou pacote do treinamento)
- 📋 **Transport Request**: Request individual

### ✅ **Resultado da Geração**

#### 📁 **Estrutura Criada no Projeto**

```
📁 Runtime Artifacts
 ├── 🏗️ Z{USUARIO}_GW_MPC (Model Provider Class)
 ├── 💻 Z{USUARIO}_GW_DPC (Data Provider Class)
 ├── 🔧 Z{USUARIO}_GW_MDL (Technical Model)
 └── 🌐 Z{USUARIO}_GW_SRV (Technical Service)

📁 Service Implementation
 ├── ✈️ SCARR Set
 │   ├── 🔍 GET_ENTITY (Leitura individual)
 │   ├── 📋 GET_ENTITYSET (Leitura coleção)
 │   ├── ➕ CREATE_ENTITY (Criação)
 │   ├── ✏️ UPDATE_ENTITY (Atualização)
 │   └── 🗑️ DELETE_ENTITY (Exclusão)
 └── 🛫 SPFLI Set
     ├── 🔍 GET_ENTITY (Leitura individual)
     ├── 📋 GET_ENTITYSET (Leitura coleção)
     ├── ➕ CREATE_ENTITY (Criação)
     ├── ✏️ UPDATE_ENTITY (Atualização)
     └── 🗑️ DELETE_ENTITY (Exclusão)
```

---

## 🎯 **Resumo do Progresso**

### ✅ **Concluído nesta Aula:**

#### 🔗 **Association Criada:**
- **Nome**: `ScarToSpfly`
- **Tipo**: **1 para N** (Um-para-Muitos)
- **Entidades**: SCARR → SPFLI
- **Vinculação**: Campo `Carrid`

#### ⚡ **Runtime Objects Gerados:**
- 🏗️ **Model Provider Class** - Metadados e modelo
- 💻 **Data Provider Class** - Lógica de implementação
- 🔧 **Technical Model** - Modelo técnico
- 🌐 **Technical Service** - Serviço técnico

#### 🔧 **Métodos Disponíveis para Implementação:**
| Operação | Método | Descrição |
|----------|---------|-----------|
| **READ** | `GET_ENTITY` | Buscar registro único |
| **READ** | `GET_ENTITYSET` | Buscar coleção |
| **CREATE** | `CREATE_ENTITY` | Criar novo registro |
| **UPDATE** | `UPDATE_ENTITY` | Atualizar registro |
| **DELETE** | `DELETE_ENTITY` | Excluir registro |

---

## 💡 **Informações Importantes**

### 📝 **Anotar Nomes Técnicos:**
- **Technical Service Name**: `Z{USUARIO}_GW_SRV`
- 🔐 **Essencial** para ativação do serviço

### 🎯 **Próximos Passos (Próxima Aula):**
- 💻 **Implementação dos métodos** CRUD
- 🔍 **Código para leitura** de dados
- ✏️ **Código para manipulação** de dados
- 🚀 **Ativação do serviço** OData

### ⚠️ **Pontos de Atenção:**
- ✅ **Sempre salvar** após cada modificação
- 📋 **Usar transport request** individual
- 🔍 **Verificar logs** de geração
- 📝 **Documentar nomes** técnicos gerados

---

## 🎉 **Status do Projeto**

### 📊 **Progresso Atual:**
```
[✅] Projeto Gateway criado
[✅] Entidades SCARR e SPFLI configuradas
[✅] Association 1-N criada
[✅] Runtime objects gerados
[🔲] Implementação dos métodos CRUD
[🔲] Ativação do serviço
[🔲] Testes do serviço OData
```

---
*🚀 **Associações criadas com sucesso!** Na próxima aula: implementação da lógica CRUD nos métodos do Data Provider!*