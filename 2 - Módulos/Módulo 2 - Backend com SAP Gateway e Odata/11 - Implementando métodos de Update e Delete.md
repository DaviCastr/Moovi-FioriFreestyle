# 🔄 Aula: Implementação dos Métodos UPDATE e DELETE para SCARR

## 📋 **Visão Geral da Aula**

### 🎯 **Objetivo**
Implementar e testar os métodos **UPDATE** (PUT) e **DELETE** para a entidade SCARR, completando todas as operações CRUD

---

## ✏️ **Implementação do Método UPDATE**

### 📝 **Código Completo - SCARR UPDATE_ENTITY**

```abap
METHOD scarset_update_entity.

    DATA: ls_scarr TYPE zcl_zsilva_gw_mpc=>ts_scarr.

    " 1. Ler dados da entidade recebida via PUT
    io_data_provider->read_entry_data( IMPORTING es_data = ls_scarr ).

    " 2. Validar se o Carrid foi informado
    IF ls_scarr-carrid IS INITIAL.
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>invalid_input
            message = 'Carrid é obrigatório para atualização'.
    ENDIF.

    " 3. Realizar UPDATE na tabela SCARR
    UPDATE scarr FROM ls_scarr.
    
    IF sy-subrc <> 0.
        " Erro na atualização
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>internal_error
            message = 'Erro ao atualizar companhia aérea'.
    ENDIF.

    " 4. Retornar a entidade atualizada
    er_entity = ls_scarr.

ENDMETHOD.
```

### 🔍 **Análise do Código UPDATE:**

#### 1. **📨 Leitura dos Dados**
```abap
io_data_provider->read_entry_data( IMPORTING es_data = ls_scarr )
```
- Lê os dados JSON recebidos no PUT
- Preenche estrutura com dados para atualização

#### 2. **🛡️ Validação de Chave**
```abap
IF ls_scarr-carrid IS INITIAL.
    RAISE EXCEPTION...
```
- Valida se a chave (Carrid) foi informada
- Impede atualização sem identificação do registro

#### 3. **💾 Execução do UPDATE**
```abap
UPDATE scarr FROM ls_scarr.
```
- Atualiza registro diretamente na tabela
- Usa estrutura mapeada automaticamente

#### 4. **📤 Retorno da Entidade**
```abap
er_entity = ls_scarr.
```
- **Observação**: Embora retorne a entidade, o método UPDATE normalmente não devolve conteúdo na resposta

---

## 🗑️ **Implementação do Método DELETE**

### 📝 **Código Completo - SCARR DELETE_ENTITY**

```abap
METHOD scarset_delete_entity.

    DATA: lv_carrid TYPE s_carr_id.

    " 1. Obter chaves da requisição
    DATA(lt_keys) = io_tech_request_context->get_converted_keys( ).

    " 2. Ler a chave específica para Carrid
    READ TABLE lt_keys INTO DATA(ls_key) WITH KEY name = 'Carrid'.
    IF sy-subrc = 0.
        lv_carrid = ls_key-value.
    ELSE.
        " Retornar exceção se a chave não for fornecida
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>invalid_key
            message = 'Carrid é obrigatório para exclusão'.
    ENDIF.

    " 3. Realizar DELETE na tabela SCARR
    DELETE FROM scarr WHERE carrid = lv_carrid.
    
    IF sy-subrc <> 0.
        " Erro na exclusão
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>internal_error
            message = |Erro ao excluir companhia aérea { lv_carrid }|.
    ENDIF.

ENDMETHOD.
```

### 🔍 **Análise do Código DELETE:**

#### 1. **🔑 Obtenção das Chaves**
```abap
io_tech_request_context->get_converted_keys( )
```
- Obtém chaves da URL da requisição DELETE
- Diferente do UPDATE, não tem body

#### 2. **🛡️ Validação de Chave Obrigatória**
```abap
READ TABLE lt_keys INTO DATA(ls_key) WITH KEY name = 'Carrid'.
```
- Extrai chave Carrid da tabela de chaves
- Valida existência antes da exclusão

#### 3. **💾 Execução do DELETE**
```abap
DELETE FROM scarr WHERE carrid = lv_carrid.
```
- Exclui registro específico por chave
- Usa cláusula WHERE para precisão

---

## 🧪 **Testes no Postman**

### ⚙️ **Configuração Comum:**
- **Headers**:
  - `X-CSRF-Token: {token}` (obtido via GET com `fetch`)
  - `Content-Type: application/json`
- **Autenticação**: Basic Auth com usuário/senha SAP

### 🔄 **Teste UPDATE (PUT)**

#### 📍 **URL:**
```
https://servidor:porta/sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet('PR')
```

#### 📝 **Payload:**
```json
{
    "Carrid": "PR",
    "CarrName": "PR Airlines Modificado",
    "CurrCode": "BRL",
    "Url": "http://www.prairlines.com.br"
}
```

#### ✅ **Resposta Esperada:**
- **Status**: `204 No Content` ✅
- **Body**: Vazio (conforme padrão HTTP para UPDATE)
- **Confirmação**: Registro atualizado no banco

### 🗑️ **Teste DELETE**

#### 📍 **URL:**
```
https://servidor:porta/sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet('PR')
```

#### 📝 **Configuração:**
- **Método**: `DELETE`
- **Body**: Vazio (não necessário)

#### ✅ **Resposta Esperada:**
- **Status**: `204 No Content` ✅
- **Body**: Vazio
- **Confirmação**: Registro excluído do banco

---

## 🚨 **Testes de Validação de Erros**

### 🧪 **UPDATE sem Chave:**

#### 📝 **URL Inválida:**
```
https://servidor:porta/sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet
```
(Sem especificar qual registro atualizar)

#### ✅ **Resposta Esperada:**
- **Status**: `400 Bad Request` ⚠️
- **Mensagem**: "Carrid é obrigatório para atualização"

### 🧪 **DELETE sem Chave:**

#### 📝 **URL Inválida:**
```
https://servidor:porta/sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet
```
(Sem especificar qual registro excluir)

#### ✅ **Resposta Esperada:**
- **Status**: `400 Bad Request` ⚠️
- **Mensagem**: "Carrid é obrigatório para exclusão"

---

## 📊 **Resumo das Operações CRUD Completas**

| Operação | Método HTTP | URL Pattern | Status Sucesso | Body Resposta |
|----------|-------------|-------------|----------------|---------------|
| **CREATE** | POST | `/SCARRSet` | `201 Created` | ✅ Objeto criado |
| **READ** | GET | `/SCARRSet` ou `/SCARRSet('ID')` | `200 OK` | ✅ Dados |
| **UPDATE** | PUT | `/SCARRSet('ID')` | `204 No Content` | ❌ Vazio |
| **DELETE** | DELETE | `/SCARRSet('ID')` | `204 No Content` | ❌ Vazio |

---

## 🛡️ **Tratamento de Erros Consolidado**

### 🚨 **Cenários de Erro Tratados:**

| Cenário | Método | Status | Mensagem |
|---------|--------|--------|----------|
| **Chave não informada** | UPDATE/DELETE | 400 | "Carrid é obrigatório" |
| **Erro de banco** | Todos | 500 | "Erro interno" |
| **Registro não encontrado** | GET/DELETE | 404 | "Recurso não encontrado" |
| **Token CSRF inválido** | POST/PUT/DELETE | 403 | "CSRF token validation failed" |

---

## 🔄 **Fluxo Completo CRUD**

### 📋 **Operações na Entidade SCARR:**
1. **CREATE** → POST para criar nova companhia aérea
2. **READ** → GET para listar/buscar companhias
3. **UPDATE** → PUT para modificar dados existentes
4. **DELETE** → DELETE para remover companhia

### ✅ **Status HTTP Corretos:**
- **201**: Criação bem-sucedida
- **200**: Consulta bem-sucedida
- **204**: Atualização/Exclusão bem-sucedida
- **400**: Erro de validação
- **404**: Recurso não encontrado
- **500**: Erro interno

---
*🎉 **CRUD completo implementado!** Todas as operações CREATE, READ, UPDATE e DELETE estão funcionando para a entidade SCARR!*


