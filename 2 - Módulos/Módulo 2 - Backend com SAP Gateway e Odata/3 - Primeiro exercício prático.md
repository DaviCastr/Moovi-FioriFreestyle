# 🚀 Aula: Introdução ao Primeiro Exercício Prático - SAP NetWeaver Gateway

## 📋 **Visão Geral do Projeto**

### 🎯 **Objetivo do Exercício**
Criar um **serviço OData** no SAP Gateway que retornará dados de **duas tabelas standard** do SAP

### 📊 **Tabelas Utilizadas**

#### ✈️ **Tabela SCARR (Companhias Aéreas)**
| Campo | Descrição | Tipo |
|-------|-----------|------|
| `CARRID` | Código da companhia | 🔑 Chave |
| `CARRNAME` | Nome da companhia | 📝 Texto |
| `URL` | Website | 🌐 URL |
| `CURRCODE` | Moeda | 💰 Código |

#### 🛫 **Tabela SPFLI (Rotas de Voo)**
| Campo | Descrição | Tipo |
|-------|-----------|------|
| `CARRID` | Código companhia | 🔑 Chave estrangeira |
| `CONNID` | Número conexão | 🔑 Chave |
| `CITYFROM` | Cidade origem | 🏙️ Texto |
| `CITYTO` | Cidade destino | 🏙️ Texto |

### 🔗 **Relacionamento**
- **SCARR → SPFLI**: **1 para N** (Um-para-Muitos)
- 📌 Uma companhia aérea pode ter **zero, uma ou várias rotas**
- 🔄 Relacionamento através do campo `CARRID`

---

## 🛠️ **Transações SAP Utilizadas**

### 🔧 **Transações Principais**

| Transação | Ícone | Finalidade |
|-----------|--------|------------|
| **SEGW** 🏗️ | `🔨` | **Criação de projetos** Gateway - Ponto de partida |
| **/IWFND/MAINT_SERVICE** ⚡ | `🚀` | **Ativação do serviço** OData |
| **SMICM** 🌐 | `🔍` | **Consulta de portas** HTTP/HTTPS disponíveis |

### 🐛 **Transações para Análise (Aulas Futuras)**
| Transação | Finalidade |
|-----------|------------|
| **Logs** 📊 | Análise de erros e monitoramento |
| **Debug** 🔍 | Depuração do serviço |

---

## 🎯 **Estrutura do Serviço OData**

### 📦 **Entidades a Serem Criadas:**

#### 1. **Entidade: CompanhiasAereas** ✈️
- 📋 Baseada na tabela **SCARR**
- 🔑 Chave: `CARRID`
- 🔗 Relacionamento com Rotas

#### 2. **Entidade: RotasVoo** 🛫
- 📋 Baseada na tabela **SPFLI**
- 🔑 Chave composta: `CARRID` + `CONNID`
- 🔗 Navegação para CompanhiaAerea

### 🔄 **Operações CRUD a Implementar:**
- ✅ **CREATE** - Criar novos registros
- 🔍 **READ** - Consultar dados
- ✏️ **UPDATE** - Atualizar informações
- 🗑️ **DELETE** - Excluir registros

---

## 📝 **Próximos Passos**

### 🎓 **Na Próxima Aula:**
- 🏗️ **Início da construção prática** do serviço
- 🔨 **Criação do projeto** na transação SEGW
- 📊 **Definição das entidades** e relacionamentos
- ⚙️ **Configuração inicial** do serviço OData

---

## 💡 **Dica Importante**
> ✨ Este exercício servirá como **base fundamental** para todo o treinamento, portanto é essencial compreender bem cada etapa!

---
*📚 Preparado para a prática? Na próxima aula, mãos à obra no SAP NetWeaver Gateway!*