# ➕ Aula: Implementação do Método POST (CREATE) para SCARR

## 📋 **Visão Geral da Aula**

### 🎯 **Objetivo**
Implementar o método **POST** (CREATE) para a entidade SCARR, permitindo a criação de novas companhias aéreas

---

## 🏗️ **Estrutura do Método CREATE**

### 📝 **Método a Implementar:**
- **Nome**: `scarset_create_entity`
- **Tipo**: POST HTTP
- **Função**: Criar novos registros na tabela SCARR

---

## 💻 **Implementação do Código**

### 🔧 **Código Completo - SCARR CREATE_ENTITY**

```abap
METHOD scarset_create_entity.

    DATA: ls_scarr TYPE zcl_zsilva_gw_mpc=>ts_scarr,
          lv_carrid TYPE s_carr_id.

    " 1. Ler dados da entidade recebida via POST
    io_data_provider->read_entry_data( IMPORTING es_data = ls_scarr ).

    " 2. Validar se o Carrid foi informado
    IF ls_scarr-carrid IS INITIAL.
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>invalid_input
            message = 'Carrid é obrigatório'.
    ENDIF.

    " 3. Verificar se o Carrid já existe na tabela
    SELECT SINGLE carrid FROM scarr
      INTO lv_carrid
      WHERE carrid = ls_scarr-carrid.
      
    IF sy-subrc = 0.
        " Carrid já existe - não permitir duplicação
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>resource_exists
            message = 'Companhia aérea já existe'.
    ENDIF.

    " 4. Inserir novo registro na tabela SCARR
    INSERT INTO scarr VALUES ls_scarr.
    
    IF sy-subrc <> 0.
        " Erro na inserção
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>internal_error
            message = 'Erro ao criar companhia aérea'.
    ENDIF.

    " 5. Retornar a entidade criada no response
    er_entity = ls_scarr.

ENDMETHOD.
```

---

## 🔍 **Análise Detalhada do Código**

### 1. **📨 Leitura dos Dados de Entrada**
```abap
io_data_provider->read_entry_data( IMPORTING es_data = ls_scarr ).
```
- **Função**: Lê os dados JSON recebidos no POST
- **Saída**: Preenche estrutura `ls_scarr` com dados da requisição

### 2. **🛡️ Validação de Campo Obrigatório**
```abap
IF ls_scarr-carrid IS INITIAL.
    RAISE EXCEPTION...
```
- **Valida**: Campo `Carrid` não pode ser vazio
- **Erro**: `invalid_input` - entrada inválida

### 3. **🔍 Verificação de Duplicidade**
```abap
SELECT SINGLE carrid FROM scarr...
IF sy-subrc = 0.
    RAISE EXCEPTION...
```
- **Consulta**: Verifica se `Carrid` já existe
- **Prevenção**: Evita chaves duplicadas
- **Erro**: `resource_exists` - recurso já existe

### 4. **💾 Inserção no Banco de Dados**
```abap
INSERT INTO scarr VALUES ls_scarr.
```
- **Ação**: Insere novo registro na tabela SCARR
- **Estrutura**: Usa dados mapeados automaticamente

### 5. **📤 Retorno da Resposta**
```abap
er_entity = ls_scarr.
```
- **Finalidade**: Retorna o objeto criado
- **Benefício**: Confirmação visual do registro criado

---

## ⚠️ **Tratamento de Erros Implementado**

### 🚨 **Tipos de Exceção Tratados:**

| Cenário de Erro | Tipo Exceção | Mensagem |
|-----------------|--------------|----------|
| **Carrid vazio** | `invalid_input` | "Carrid é obrigatório" |
| **Carrid duplicado** | `resource_exists` | "Companhia aérea já existe" |
| **Erro de inserção** | `internal_error` | "Erro ao criar companhia aérea" |

### 🛡️ **Validações de Negócio:**
- ✅ **Campo obrigatório**: Carrid deve ser informado
- ✅ **Unicidade**: Não permite Carrid duplicado
- ✅ **Integridade**: Trata erros de banco de dados

---

## 🔄 **Fluxo da Requisição POST**

### 📨 **Entrada (Request):**
```json
{
  "Carrid": "NZ",
  "CarrName": "Air New Zealand",
  "CurrCode": "NZD",
  "Url": "http://www.airnewzealand.com"
}
```

### 📤 **Saída (Response):**
```json
{
  "d": {
    "Carrid": "NZ",
    "CarrName": "Air New Zealand", 
    "CurrCode": "NZD",
    "Url": "http://www.airnewzealand.com"
  }
}
```

---

## 🎯 **Resumo da Implementação**

### ✅ **Funcionalidades Implementadas:**

| Recurso | Status | Descrição |
|---------|--------|-----------|
| **Leitura dados POST** | ✅ | `io_data_provider->read_entry_data` |
| **Validação obrigatória** | ✅ | Carrid não pode ser vazio |
| **Verificação duplicidade** | ✅ | SELECT antes do INSERT |
| **Inserção no banco** | ✅ | `INSERT INTO scarr` |
| **Tratamento de erros** | ✅ | Exceções específicas |
| **Retorno do objeto** | ✅ | Confirmação visual |

### 🔧 **Métodos Gateway Utilizados:**

| Componente | Finalidade |
|------------|-----------|
| **`io_data_provider`** | 📨 Acesso aos dados da requisição |
| **`read_entry_data()`** | 🔍 Leitura dos dados de entrada |
| **`er_entity`** | 📤 Retorno da entidade criada |

---

## 🚀 **Próximos Passos**

### 🔜 **Na Próxima Aula:**
- 📥 **Download e instalação** do Postman
- ⚙️ **Configuração** do ambiente de testes
- 🧪 **Teste prático** do método POST
- 🔍 **Validação** da criação de registros

### 🛠️ **Ferramenta para Testes:**
- **Postman**: 🌐 Cliente HTTP para testes de API
- **Funcionalidades**: Envio de requisições POST com JSON
- **Vantagens**: Interface amigável para desenvolvimento

---
*🎉 **Método POST implementado com sucesso!** Próximo passo: testar a criação de registros usando Postman!*