# 🚀 Aula: Criação do Primeiro Serviço OData - Passo a Passo

## 📋 **Visão Geral da Aula Prática**

### 🎯 **Objetivo**
Criar um **serviço OData** no SAP Gateway utilizando as tabelas **SCARR** (Companhias Aéreas) e **SPFLI** (Rotas de Voo)

---

## 🔍 **Análise das Tabelas Base**

### ✈️ **Tabela SCARR (Companhias Aéreas)**
| Campo | Tipo | Descrição | Status no OData |
|-------|------|-----------|-----------------|
| `MANDT` | Cliente | ❌ **Removido** | Não utilizado |
| `CARRID` | String | Código companhia | ✅ **Chave primária** |
| `CARRNAME` | String | Nome companhia | ✅ Incluído |
| `CURRCODE` | String | Moeda | ✅ Incluído |
| `URL` | String | Website | ✅ Incluído |

### 🛫 **Tabela SPFLI (Rotas de Voo)**
| Campo | Tipo | Descrição | Status no OData |
|-------|------|-----------|-----------------|
| `MANDT` | Cliente | ❌ **Removido** | Não utilizado |
| `CARRID` | String | Código companhia | ✅ **Chave composta** |
| `CONNID` | String | Número rota | ✅ **Chave composta** |
| `CITYFROM` | String | Cidade origem | ✅ Incluído |
| `CITYTO` | String | Cidade destino | ✅ Incluído |
| Outros campos | Vários | Demais informações | ✅ Incluídos |

---

## 🛠️ **Passo a Passo - Criação do Projeto**

### 1. **Acessar Transação SEGW** 🏗️
- Transação: `SEGW`
- Local: **Tela inicial do SAP**

### 2. **Criar Novo Projeto**
- **Botão**: "Create" ou "Novo"
- **Nome do Projeto**: `Z{USUARIO}_GW`
  - 📝 Exemplo: `ZPSILVA_GW`
- **Descrição**: "Serviço OData"
- **Pacote**: `ZLOCAL` (ou pacote específico do treinamento)

### 3. **Estrutura do Projeto Criado**
```
📁 Data Model
 ├── 📁 Entity Types
 ├── 📁 Associations  
 ├── 📁 Entity Sets
📁 Service Implementation
📁 Runtime Objects
📁 Service Maintenance
```

---

## 🎯 **Criação da Primeira Entidade (SCARR)**

### 🔧 **Importação da Estrutura**
1. **Botão direito** em `Data Model` → `Import` → `DDIC Structure`
2. **Configurações**:
   - **Name**: `SCARR`
   - **Type**: `Entity Type`
   - **DDIC Structure**: `SCARR` (tabela)
   - ✅ **Create Default Entity Set**

### ⚙️ **Seleção de Campos**
- ✅ **Selecionar TODOS os campos**
- ❌ **REMOVER campo `MANDT`** (cliente)

### 🔑 **Definição da Chave**
- ✅ **Marcar `CARRID`** como chave primária
- 📌 Campo `SKey` (Signature Key)

### ✅ **Resultado - Entidade SCARR**
```abap
Entity Type: SCARR
Properties:
  - CarrId (String)     🔑
  - CarrName (String)   📝
  - CurrCode (String)   💰
  - Url (String)        🌐
Entity Set: SCARRSet
```

---

## 🎯 **Criação da Segunda Entidade (SPFLI)**

### 🔧 **Importação da Estrutura**
1. **Botão direito** em `Data Model` → `Import` → `DDIC Structure`
2. **Configurações**:
   - **Name**: `SPFLI`
   - **Type**: `Entity Type`
   - **DDIC Structure**: `SPFLI` (tabela)
   - ✅ **Create Default Entity Set`

### ⚙️ **Seleção de Campos**
- ✅ **Selecionar TODOS os campos**
- ❌ **REMOVER campo `MANDT`** (cliente)

### 🔑 **Definição da Chave**
- ✅ **Marcar `CARRID`** como chave
- ✅ **Marcar `CONNID`** como chave
- 📌 **Chave composta** com dois campos

### ⚠️ **Ajustes de Tipos de Dados**
| Campo | Tipo Original | Tipo Ajustado | Motivo |
|-------|---------------|---------------|--------|
| `FLTIME` | Edm.Time | String | Simplificação |
| `DEPTIME` | Edm.Time | String | Simplificação |
| `ARRTIME` | Edm.Time | String | Simplificação |
| `PERIOD` | Byte | String | Simplificação |

### ✅ **Resultado - Entidade SPFLI**
```abap
Entity Type: SPFLI
Properties:
  - CarrId (String)     🔑
  - ConnId (String)     🔑
  - CityFrom (String)   🏙️
  - CityTo (String)     🏙️
  - ... outros campos
Entity Set: SPFLISet
```

---

## 💾 **Salvamento do Projeto**

### 📦 **Transport Request**
- ✅ **Criar/criar Request** personalizado
- 💡 **Cada desenvolvedor** com sua própria request
- 🛡️ **Evita conflitos** entre objetos

---

## 📊 **Resumo do Progresso**

### ✅ **Concluído nesta Aula:**
1. 🏗️ **Projeto Gateway criado**
2. ✈️ **Entidade SCARR** configurada
3. 🛫 **Entidade SPFLI** configurada
4. 🔑 **Chaves primárias** definidas
5. ⚙️ **Tipos de dados** ajustados

### 🎯 **Próximos Passos (Próximas Aulas):**
- 🔗 **Criação de Associations** (relacionamentos)
- ⚡ **Geração de Runtime Objects**
- 🚀 **Ativação do serviço**
- 🔧 **Implementação dos métodos CRUD**

---

## 💡 **Dicas Importantes**

### 🎨 **Padrão de Nomenclatura:**
- **Projeto**: `Z{USUARIO}_GW`
- **Entidades**: Nomes descritivos em inglês
- **Campos**: **Camel Case** (primeira letra maiúscula)

### ⚠️ **Atenção a Campos:**
- ❌ **Sempre remover `MANDT`** (já gerido pelo sistema)
- 🔄 **Ajustar tipos complexos** para String quando necessário
- ✅ **Manter consistência** nos nomes dos campos

### 🛡️ **Boas Práticas:**
- 📋 **Salvar em requests** individuais
- 🔍 **Revisar metadados** gerados
- 📝 **Documentar alterações** realizadas

---
*🎉 **Primeira etapa concluída!** Na próxima aula: relacionamentos e associações entre as entidades!*