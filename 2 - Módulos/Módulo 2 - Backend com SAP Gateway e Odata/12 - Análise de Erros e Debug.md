# 🔍 Aula: Análise de Erros e Debug no SAP Gateway

## 📋 **Visão Geral da Aula**

### 🎯 **Objetivo**
Aprender a **analisar erros** e realizar **debug** em serviços OData no ambiente NetWeaver Gateway

---

## 🚨 **Transações para Análise de Erros**

### 📊 **1. Transação: `/IWFND/ERROR_LOG`**

#### 🎯 **Finalidade:**
- 📝 **Logs completos** de todas as chamadas HTTP
- 🔍 **Rastreamento** de requisições por usuário e período
- 📋 **Detalhes técnicos** de erros ocorridos

#### 🔧 **Como Usar:**
1. **Acessar transação** `/IWFND/ERROR_LOG`
2. **Filtrar por**:
   - 👤 **Usuário** de comunicação
   - 📅 **Período** do erro
   - 🔍 **Tipo** de requisição

#### 📋 **Informações Disponíveis:**
- 📨 **Cabeçalhos HTTP** da requisição
- 📝 **Corpo da mensagem** (payload)
- 🚨 **Detalhes do erro** técnico
- 🔗 **Link para Application Log**

### 📊 **2. Transação: `/IWFND/TRAces`**

#### 🎯 **Finalidade:**
- 🎯 **Trace específico** por usuário
- 📊 **Logs detalhados** de performance
- 🔍 **Rastreamento** de payloads completos

#### ⚙️ **Configuração:**
| Parâmetro | Configuração | Descrição |
|-----------|-------------|-----------|
| **Trace Type** | `Full` | 📋 Log completo |
| **Payload Trace** | `✅ Ativo` | 📨 Rastreia payload |
| **Performance** | `✅ Ativo` | ⚡ Métricas performance |
| **HTTP Method** | `(vazio)` | 🌐 Todos os métodos |

#### 🔧 **Fluxo de Configuração:**
1. **Acessar** `/IWFND/TRAces`
2. **Configurar trace** para usuário específico
3. **Executar** requisições de teste
4. **Analisar** logs gerados

---

## 🧪 **Cenário Prático de Análise**

### 🔄 **Fluxo de Investigação de Erro:**

#### 1. **🚨 Cliente Reporta Erro:**
- "Recebi HTTP 400 ao acessar serviço"

#### 2. **🔍 Investigação no ERROR_LOG:**
```abap
Transação: /IWFND/ERROR_LOG
Filtros: 
  - Usuário: USUARIO_CLIENTE
  - Data: [data do erro]
  - Status: 400 Bad Request
```

#### 3. **📋 Análise dos Dados:**
- **Headers**: Cabeçalhos da requisição
- **Body**: Payload enviado
- **Error Details**: Mensagem técnica do erro
- **Application Log**: Logs detalhados da aplicação

#### 4. **🎯 Identificação da Causa:**
- **Exemplo**: "Recurso não encontrado na tabela SCARR"
- **Solução**: Verificar se ID existe ou ajustar requisição

---

## 🐛 **Debug no Gateway**

### 🔧 **Preparação do Debug:**

#### 1. **Acessar Código:**
- **Transação**: `SEGW`
- **Navegar**: `Service Implementation` → Método específico

#### 2. **Configurar Breakpoint:**
- 🎯 **Selecionar linha** para debug
- 👤 **Breakpoint externo** (para usuário externo)
- ✅ **Ativar debug** por usuário

#### 3. **Disparar Requisição:**
- 🌐 **Postman** ou cliente HTTP
- 🔄 **Executar** requisição que aciona o método

### 🔍 **Processo de Debug:**

#### ✅ **Ferramentas Disponíveis:**
- 🔍 **Step-by-step** execução
- 📊 **Inspeção de variáveis**
- 📝 **Análise de dados** de entrada/saída
- 🚨 **Identificação** de exceções

#### 📋 **Informações para Debug:**
| Elemento | O que Analisar |
|----------|----------------|
| **Variáveis de entrada** | 📨 Dados recebidos da requisição |
| **Estruturas internas** | 💾 Dados processados |
| **SQL Statements** | 🗄️ Consultas ao banco |
| **Condicionais** | 🎯 Fluxo do programa |

---

## 📊 **Tipos Comuns de Erros**

### 🚨 **Erros HTTP Mais Frequentes:**

| Status | Causa Provável | Ação |
|--------|----------------|------|
| **400 Bad Request** | 📝 Dados inválidos ou faltantes | Validar payload |
| **401 Unauthorized** | 🔐 Problema de autenticação | Verificar usuário/senha |
| **403 Forbidden** | 🚫 Token CSRF inválido | Obter novo token |
| **404 Not Found** | 🔍 Recurso não existe | Verificar chave/ID |
| **500 Internal Error** | 💥 Erro no servidor | Analisar logs/dumps |

### 🔧 **Erros Específicos do Gateway:**

#### 🎯 **CSRF Token Issues:**
```http
Erro: "CSRF token validation failed"
Solução: 
  1. GET com header "X-CSRF-Token: fetch"
  2. Usar token retornado em POST/PUT/DELETE
```

#### 🎯 **Problemas de Payload:**
```http
Erro: "Invalid JSON format"
Solução: Validar sintaxe JSON no Postman
```

#### 🎯 **Erros de Chave:**
```http
Erro: "Carrid é obrigatório"
Solução: Incluir chave na URL: /SCARRSet('ID')
```

---

## 🔄 **Fluxo Completo de Troubleshooting**

### 📋 **Checklist de Investigação:**

#### 1. **✅ Verificação Básica:**
- 🌐 Serviço está ativo? (`/IWFND/MAINT_SERVICE`)
- 🔐 Autenticação correta?
- 📨 Headers adequados?

#### 2. **🔍 Análise de Logs:**
- 📊 `ERROR_LOG` para detalhes do erro
- 📈 `TRACES` para rastreamento completo
- 📝 Application Log para detalhes técnicos

#### 3. **🐛 Debug do Código:**
- 🎯 Breakpoints nos métodos relevantes
- 🔍 Análise passo-a-passo
- 📊 Inspeção de dados

#### 4. **🛠️ Correção:**
- ✏️ Ajuste no código ABAP
- ⚙️ Configuração do serviço
- 📝 Documentação do problema

---

## 💡 **Melhores Práticas**

### 🛡️ **Prevenção de Erros:**
- ✅ **Validações robustas** nos métodos
- 📝 **Tratamento de exceções** específico
- 🔍 **Logs informativos** para debug
- 📊 **Monitoramento** contínuo

### 🔧 **Ferramentas Recomendadas:**
| Ferramenta | Finalidade |
|------------|-----------|
| **Postman** | 🧪 Testes de API |
| **JSON Formatter** | 📊 Visualização JSON |
| **SEGW** | 🔧 Desenvolvimento |
| **ERROR_LOG** | 🚨 Análise de erros |
| **TRACES** | 📈 Rastreamento |

### 📝 **Documentação:**
- 🗂️ **Manter histórico** de erros comuns
- 📋 **Procedimentos** de troubleshooting
- 👥 **Compartilhar soluções** com equipe

---
*🎯 **Debug e análise de erros dominados!** Agora você pode investigar e resolver problemas em serviços OData com confiança!*