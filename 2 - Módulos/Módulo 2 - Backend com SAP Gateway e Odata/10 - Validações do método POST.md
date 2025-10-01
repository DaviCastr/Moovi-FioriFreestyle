# 🧪 Aula: Testes do Método POST com Postman e Validações

## 📋 **Visão Geral da Aula**

### 🎯 **Objetivo**
Testar o método POST implementado usando **Postman** e validar todas as funcionalidades de criação de registros

---

## 🛠️ **Configuração do Postman**

### 📥 **Download e Instalação**
- 🌐 **URL Oficial**: `www.postman.com/downloads`
- 💻 **Sistemas**: Windows, Mac, Linux
- 📦 **Tamanho**: ~150 MB

### ⚙️ **Configuração Inicial**
- 🔓 **Skip account creation** - uso local sem conta
- 🏠 **Interface principal**: Collections, Environments, etc.

---

## 🔗 **Configuração do Serviço OData no Postman**

### 🌐 **URL Base do Serviço**
```
https://servidor:porta/sap/opu/odata/sap/Z{USUARIO}_GW_SRV/SCARRSet
```

### 🔐 **Configuração de Autenticação**
| Parâmetro | Valor | Descrição |
|-----------|-------|-----------|
| **Type** | `Basic Auth` | 🔐 Autenticação básica |
| **Username** | Usuário SAP | 👤 Mesmo do ambiente |
| **Password** | Senha SAP | 🔒 Mesma do ambiente |

### 📝 **Headers Configurados**
| Header | Valor | Finalidade |
|--------|-------|------------|
| **Accept** | `application/json` | 📨 Receber resposta em JSON |
| **Content-Type** | `application/json` | 📤 Enviar dados em JSON |

---

## 🧪 **Teste 1: Requisição GET (Baseline)**

### 🔧 **Configuração:**
- **Método**: `GET`
- **URL**: `/SCARRSet`
- **Headers**: Accept e Content-Type como JSON

### ✅ **Resultado Esperado:**
- **Status**: `200 OK`
- **Resposta**: Lista de companhias aéreas em JSON
- **Confirmação**: Serviço está acessível

---

## 🧪 **Teste 2: Requisição POST (Criação)**

### 📝 **Payload JSON para Criação:**
```json
{
    "Carrid": "PR",
    "CarrName": "PR Airlines",
    "CurrCode": "BRL",
    "Url": "http://www.prairlines.com"
}
```

### ⚠️ **Problema de Segurança - CSRF Token**
- **Erro**: `CSRF token validation failed`
- **Causa**: Requisições POST precisam de token de segurança
- **Solução**: Obter token CSRF do servidor

---

## 🔐 **Solução CSRF Token**

### 🔄 **Processo em 2 Passos:**

#### **Passo 1: Obter Token CSRF**
```http
GET /SCARRSet
Headers:
X-CSRF-Token: fetch
```

#### **Passo 2: Usar Token no POST**
```http
POST /SCARRSet
Headers:
X-CSRF-Token: {token_obtido}
Content-Type: application/json
```

### 📋 **Fluxo Completo:**
1. **Configurar header** `X-CSRF-Token: fetch` no GET
2. **Executar GET** - token é retornado nos headers de resposta
3. **Copiar token** do header de resposta
4. **Configurar POST** com token obtido
5. **Executar POST** - criação bem-sucedida

---

## ✅ **Teste de Criação Bem-Sucedida**

### 🎯 **Requisição POST Válida:**
- **Método**: `POST`
- **Headers**: 
  - `X-CSRF-Token: {token}`
  - `Content-Type: application/json`
- **Body**: JSON com dados da nova companhia

### 📈 **Resposta de Sucesso:**
- **Status**: `201 Created` ✅
- **Body**: Retorna o objeto criado
- **Confirmação**: Registro inserido no banco

---

## 🚨 **Testes de Validação de Erros**

### 🧪 **Teste 3: Duplicidade de Chave**

#### 📝 **Payload:**
```json
{
    "Carrid": "PR",  // Já existe!
    "CarrName": "Outra PR",
    "CurrCode": "BRL",
    "Url": "http://www.outrapr.com"
}
```

#### ✅ **Resultado Esperado:**
- **Status**: `400 Bad Request` ⚠️
- **Mensagem**: "Companhia aérea já existe"
- **Validação**: Prevenção de duplicatas funcionando

### 🧪 **Teste 4: Campo Obrigatório Faltando**

#### 📝 **Payload Inválido:**
```json
{
    "Carrid": "",  // Vazio!
    "CarrName": "Sem ID",
    "CurrCode": "USD",
    "Url": "http://www.semid.com"
}
```

#### ✅ **Resultado Esperado:**
- **Status**: `400 Bad Request` ⚠️
- **Mensagem**: "Carrid é obrigatório"
- **Validação**: Campos obrigatórios sendo verificados

---

## 📊 **Resumo dos Testes Realizados**

| Teste | Método | Payload | Status Esperado | Validação |
|-------|--------|---------|----------------|-----------|
| **GET Baseline** | GET | - | 200 OK | ✅ Serviço acessível |
| **POST Sucesso** | POST | JSON válido | 201 Created | ✅ Criação funcionando |
| **POST Duplicado** | POST | Chave existente | 400 Bad Request | ✅ Prevenção duplicatas |
| **POST Inválido** | POST | Campo vazio | 400 Bad Request | ✅ Validação obrigatórios |

---

## 🔧 **Configurações Avançadas do Postman**

### 💾 **Salvar Configurações:**
- **Collections**: Agrupar requisições relacionadas
- **Environments**: Variáveis para diferentes ambientes
- **Tests**: Scripts de validação automática

### ⚡ **Dicas de Produtividade:**
- **Variables**: `${baseUrl}` para URL base
- **Tests**: Validar status code automaticamente
- **Pre-request**: Scripts para obter tokens automaticamente

---

## 🎯 **Validações Implementadas no Backend**

### 🛡️ **Camadas de Validação:**

#### 1. **Validação de Dados Obrigatórios**
```abap
IF ls_scarr-carrid IS INITIAL.
    RAISE EXCEPTION...
```

#### 2. **Validação de Unicidade**
```abap
SELECT SINGLE carrid FROM scarr...
IF sy-subrc = 0.
    RAISE EXCEPTION...
```

#### 3. **Validação de Integridade**
```abap
INSERT INTO scarr VALUES ls_scarr.
IF sy-subrc <> 0.
    RAISE EXCEPTION...
```

---

## 📝 **Logs e Debug**

### 🔍 **Ferramentas de Análise:**
- **Transação ST22**: ABAP Dump Analysis
- **Transação SLG0**: Application Logs
- **Gateway Client**: Logs de requisições

### 🐛 **Identificação de Erros:**
- **HTTP 400**: Erro de validação de negócio
- **HTTP 401**: Problema de autenticação
- **HTTP 403**: Token CSRF inválido
- **HTTP 500**: Erro interno do servidor

---
*🎉 **Testes do método POST concluídos com sucesso!** Todas as validações estão funcionando corretamente!*