
# 🔗 Referências

**SCARR - GET_ENTITY**

[https://github.com/moovi-education/fiori-freestyle-gateway/blob/main/scarr_metodos/scarrset_get_entity.txt](https://github.com/moovi-education/fiori-freestyle-gateway/blob/main/scarr_metodos/scarrset_get_entity.txt)

**SCARR - GET_ENTITYSET**

[https://github.com/moovi-education/fiori-freestyle-gateway/blob/main/scarr_metodos/scarrset_get_entityset.txt](https://github.com/moovi-education/fiori-freestyle-gateway/blob/main/scarr_metodos/scarrset_get_entityset.txt)

**SPFLI - GET_ENTITY**

[https://github.com/moovi-education/fiori-freestyle-gateway/blob/main/spfli_metodos/spfliset_get_entity.txt](https://github.com/moovi-education/fiori-freestyle-gateway/blob/main/spfli_metodos/spfliset_get_entity.txt)

**SPFLI - GET_ENTITYSET**

[https://github.com/moovi-education/fiori-freestyle-gateway/blob/main/spfli_metodos/spfliset_get_entityset.txt](https://github.com/moovi-education/fiori-freestyle-gateway/blob/main/spfli_metodos/spfliset_get_entityset.txt)

# 💻 Aula: Implementação dos Métodos de Seleção - Códigos Completos

## 📋 **Visão Geral dos Métodos GET**

### 🎯 **Métodos Implementados**
| Método | Entidade | Descrição |
|--------|----------|-----------|
| **GET_ENTITY** 🎯 | SCARR | Busca registro único por Carrid |
| **GET_ENTITYSET** 📋 | SCARR | Lista com filtros e ordenação |
| **GET_ENTITY** 🎯 | SPFLI | Busca registro por Carrid + Connid |
| **GET_ENTITYSET** 📋 | SPFLI | Lista com filtros múltiplos |

---

## ✈️ **SCARR - GET_ENTITY (Registro Único)**

### 📝 **Código Completo:**
```abap
METHOD scarset_get_entity.

    DATA: lv_carrid TYPE s_carr_id.

    " Obter as chaves da requisição
    DATA(lt_keys) = io_tech_request_context->get_converted_keys( ).

    " Ler a chave específica para Carrid
    READ TABLE lt_keys INTO DATA(ls_key) WITH KEY name = 'Carrid'.
    IF sy-subrc = 0.
        lv_carrid = ls_key-value.
    ELSE.
        " Retornar exceção se a chave não for fornecida
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>invalid_key.
    ENDIF.

    " Selecionar o registro único da SCARR
    SELECT SINGLE * FROM scarr
      INTO CORRESPONDING FIELDS OF er_entity
      WHERE carrid = lv_carrid.

    IF sy-subrc <> 0.
        " Retornar exceção se nenhum registro for encontrado
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>resource_not_found.
    ENDIF.

ENDMETHOD.
```

### 🔧 **Lógica Explicada:**
1. **📨 Obtém chaves** da requisição usando `get_converted_keys()`
2. **🔍 Busca chave Carrid** na tabela de chaves
3. **🚨 Valida existência** da chave obrigatória
4. **🎯 Seleciona registro único** com `SELECT SINGLE`
5. **⚠️ Trata registro não encontrado** com exceção

---

## ✈️ **SCARR - GET_ENTITYSET (Lista de Registros)**

### 📝 **Código Completo:**
```abap
METHOD scarset_get_entityset.

    DATA: lt_filter     TYPE /iwbep/t_mgw_select_option,
          lt_range      TYPE /iwbep/t_mgw_select_option,
          lr_filter     TYPE REF TO /iwbep/if_mgw_req_filter,
          lt_scarr      TYPE TABLE OF scarr,
          lt_orderby    TYPE /iwbep/t_mgw_ordering,
          lt_entityset  TYPE zcl_zsilva_gw_mpc=>tt_scarr.

    " Obter instância do filtro
    lr_filter = io_tech_request_context->get_filter( ).
    
    " Obter as opções de filtro
    lr_filter->get_filter_select_options( IMPORTING et_filter_select_options = lt_filter ).

    " Obter parâmetros de ordenação
    io_tech_request_context->get_orderby( IMPORTING et_orderby = lt_orderby ).

    " Converter filtros para ranges
    DATA(lo_filter) = io_tech_request_context->get_filter( ).
    lo_filter->get_converted_values( CHANGING ct_filter_select_options = lt_range ).

    " Selecionar dados da tabela SCARR
    SELECT *
      FROM scarr
      INTO TABLE lt_entityset.

    " Aplicar filtros se existirem
    IF lt_range IS NOT INITIAL.
        " Filtrar a tabela interna com base nos ranges
        DELETE lt_entityset WHERE (lt_range).
    ENDIF.

    " Aplicar ordenação se solicitada
    IF lt_orderby IS NOT INITIAL.
        " Ordenar a tabela interna com base nos parâmetros de ordenação
        SORT lt_entityset BY (lt_orderby).
    ENDIF.

    " Retornar a entidade
    et_entityset = lt_entityset.

ENDMETHOD.
```

### 🔧 **Lógica Explicada:**
1. **⚡ Obtém filtros** usando `get_filter()->get_filter_select_options()`
2. **📊 Obtém ordenação** com `get_orderby()`
3. **🔄 Converte filtros** para formato de ranges
4. **📋 Seleciona todos os dados** da SCARR
5. **🎛️ Aplica filtros dinamicamente** na tabela interna
6. **📈 Ordena resultados** conforme parâmetros
7. **📤 Retorna dados** processados

---

## 🛫 **SPFLI - GET_ENTITY (Registro Único)**

### 📝 **Código Completo:**
```abap
METHOD spfliset_get_entity.

    DATA: lv_carrid TYPE s_carr_id,
          lv_connid TYPE s_conn_id.

    " Obter as chaves da requisição
    DATA(lt_keys) = io_tech_request_context->get_converted_keys( ).

    " Ler a chave para Carrid
    READ TABLE lt_keys INTO DATA(ls_key_carrid) WITH KEY name = 'Carrid'.
    IF sy-subrc = 0.
        lv_carrid = ls_key_carrid-value.
    ELSE.
        " Retornar exceção se a chave Carrid não for fornecida
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>invalid_key.
    ENDIF.

    " Ler a chave para Connid
    READ TABLE lt_keys INTO DATA(ls_key_connid) WITH KEY name = 'Connid'.
    IF sy-subrc = 0.
        lv_connid = ls_key_connid-value.
    ELSE.
        " Retornar exceção se a chave Connid não for fornecida
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>invalid_key.
    ENDIF.

    " Selecionar o registro único da SPFLI
    SELECT SINGLE *
      FROM spfli
      INTO CORRESPONDING FIELDS OF er_entity
      WHERE carrid = lv_carrid
        AND connid = lv_connid.

    IF sy-subrc <> 0.
        " Retornar exceção se nenhum registro for encontrado
        RAISE EXCEPTION TYPE /iwbep/cx_mgw_tech_exception
          EXPORTING
            textid = /iwbep/cx_mgw_tech_exception=>resource_not_found.
    ENDIF.

ENDMETHOD.
```

### 🔧 **Lógica Explicada:**
1. **🔑 Obtém chave Carrid** e valida existência
2. **🔑 Obtém chave Connid** e valida existência
3. **🚨 Valida AMBAS chaves** obrigatórias
4. **🎯 Seleciona registro único** com chave composta
5. **⚠️ Trata registro não encontrado** com exceção

---

## 🛫 **SPFLI - GET_ENTITYSET (Lista de Registros)**

### 📝 **Código Completo:**
```abap
METHOD spfliset_get_entityset.

    DATA: lt_filter        TYPE /iwbep/t_mgw_select_option,
          lt_range_carrid  TYPE RANGE OF s_carr_id,
          lt_range_connid  TYPE RANGE OF s_conn_id,
          lr_filter        TYPE REF TO /iwbep/if_mgw_req_filter,
          lt_entityset     TYPE zcl_zsilva_gw_mpc=>tt_spfli,
          lt_orderby       TYPE /iwbep/t_mgw_ordering.

    " Obter instância do filtro
    lr_filter = io_tech_request_context->get_filter( ).
    
    " Obter as opções de filtro
    lr_filter->get_filter_select_options( IMPORTING et_filter_select_options = lt_filter ).

    " Obter parâmetros de ordenação
    io_tech_request_context->get_orderby( IMPORTING et_orderby = lt_orderby ).

    " Processar filtros para Carrid
    LOOP AT lt_filter INTO DATA(ls_filter) WHERE property = 'Carrid'.
        APPEND LINES OF ls_filter-select_options TO lt_range_carrid.
    ENDLOOP.

    " Processar filtros para Connid
    LOOP AT lt_filter INTO DATA(ls_filter_conn) WHERE property = 'Connid'.
        APPEND LINES OF ls_filter_conn-select_options TO lt_range_connid.
    ENDLOOP.

    " Selecionar dados da tabela SPFLI com filtros
    IF lt_range_carrid IS NOT INITIAL OR lt_range_connid IS NOT INITIAL.
        " Se há filtros, aplicar na seleção
        SELECT *
          FROM spfli
          INTO TABLE lt_entityset
          WHERE carrid IN lt_range_carrid
            AND connid IN lt_range_connid.
    ELSE.
        " Se não há filtros, selecionar todos os registros
        SELECT *
          FROM spfli
          INTO TABLE lt_entityset.
    ENDIF.

    " Aplicar ordenação se solicitada
    IF lt_orderby IS NOT INITIAL.
        " Ordenar a tabela interna com base nos parâmetros de ordenação
        SORT lt_entityset BY (lt_orderby).
    ENDIF.

    " Retornar a entidade
    et_entityset = lt_entityset.

ENDMETHOD.
```

### 🔧 **Lógica Explicada:**
1. **⚡ Obtém filtros** da requisição
2. **🔍 Processa filtros para Carrid** criando ranges
3. **🔍 Processa filtros para Connid** criando ranges
4. **📊 Seleção inteligente**: com ou sem filtros
5. **🎛️ Aplica filtros diretamente no SELECT** para performance
6. **📈 Ordena resultados** conforme parâmetros
7. **📤 Retorna dados** processados

---

## ⚙️ **Componentes Técnicos Utilizados**

### 🔧 **Classes e Métodos do Gateway**

| Componente | Finalidade |
|------------|-----------|
| **`io_tech_request_context`** | 📨 Contexto completo da requisição |
| **`get_converted_keys()`** | 🔑 Obtém e converte chaves |
| **`get_filter()`** | ⚡ Acessa filtros da requisição |
| **`get_orderby()`** | 📊 Obtém parâmetros de ordenação |
| **`/iwbep/cx_mgw_tech_exception`** | 🚨 Exceções técnicas padronizadas |

### 🛡️ **Tratamento de Erros**
- ✅ **Validação de chaves** obrigatórias
- 🚨 **Exceções específicas** para cada cenário de erro
- 📝 **Mensagens claras** para o consumidor do serviço

---

## 🎯 **Resumo da Implementação**

### ✅ **Funcionalidades Implementadas:**

| Recurso | SCARR | SPFLI |
|---------|-------|-------|
| **Busca por chave** | ✅ Carrid | ✅ Carrid + Connid |
| **Listagem completa** | ✅ | ✅ |
| **Filtros dinâmicos** | ✅ | ✅ Múltiplos |
| **Ordenação** | ✅ | ✅ |
| **Validações** | ✅ | ✅ Dupla validação |
| **Tratamento de erros** | ✅ | ✅ |

### 🔧 **Padrões de Codificação:**
- 🏗️ **Estrutura consistente** entre métodos
- 📝 **Comentários explicativos**
- 🛡️ **Tratamento robusto** de erros
- ⚡ **Performance otimizada** com filtros no SELECT

---
*🎉 **Códigos completos implementados!** Próximo passo: ativar o serviço e testar todas as funcionalidades!*