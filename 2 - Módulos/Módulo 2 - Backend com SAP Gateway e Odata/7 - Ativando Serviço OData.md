# 🌐 Aula: Ativação e Teste do Serviço OData

## 📋 **Visão Geral da Aula**

### 🎯 **Objetivo**
Ativar o serviço OData no Gateway e realizar testes dos métodos implementados

---

## 🚀 **Ativação do Serviço OData**

### 1. **Acessar Transação de Ativação**
- **Transação**: `/IWFND/MAINT_SERVICE`
- 📍 **Caminho**: Tela inicial do SAP

### 2. **Inserir Novo Serviço**
- 🖱️ **Botão**: "Add Service"
- ⚙️ **Configurações**:

| Parâmetro | Valor | Descrição |
|-----------|-------|-----------|
| **System Alias** | `LOCAL` | 🌐 Sistema local |
| **Technical Service Name** | `Z{USUARIO}_GW_SRV` | 🔧 Nome do serviço técnico |

### 3. **Configurações do Serviço**
- **Technical Model Name**: `Z{USUARIO}_GW_MDL` (gerado automaticamente)
- **Package**: `ZFIORI_F` 📦
- **ICF Node**: `Standard Mode` ✅
- **Authentication**: Padrão (usuário/senha) 🔐

### 4. **Confirmação e Salvamento**
- ✅ **Salvar em transport request** específica
- 📝 **Serviço criado com sucesso** - metadados carregados

---

## 🔍 **Verificação do Serviço Ativo**

### 📊 **Status no Catálogo**
- ✅ **Ícone verde** = Serviço ativo
- 🌐 **System Alias**: `LOCAL`
- 🔗 **ICF Node**: Ativo e publicado

### 🔎 **Localizar Serviço**
- **Filtrar por**: `Z{USUARIO}_GW_SRV`
- ✅ **Status**: Ativo e operacional

---

## 🧪 **Testes do Serviço OData**

### 🛠️ **Gateway Client - Ferramenta de Teste**

#### 📍 **Acesso**: 
- 🖱️ **Botão**: "Gateway Client" na tela do serviço

#### 🔧 **Configuração Base**:
```
URL Base: /sap/opu/odata/sap/Z{USUARIO}_GW_SRV
```

### 📋 **Testes Realizados**

#### 1. **Metadata do Serviço** 📜
```
GET /sap/opu/odata/sap/ZPSILVA_GW_SRV?$format=xml
```
**✅ Resultado**: 
- Lista entidades SCARRSet e SPFLISet
- URLs HTTP de publicação
- Informações para desenvolvimento frontend

#### 2. **Lista SCARR (GET_ENTITYSET)** ✈️
```
GET /sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet?$format=json
```
**✅ Resultado**: 
- Lista completa de companhias aéreas
- Formato JSON legível
- Campos: Carrid, CarrName, CurrCode, Url

#### 3. **Registro Único SCARR (GET_ENTITY)** 🎯
```
GET /sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet('AA')?$format=json
```
**✅ Resultado**: 
- Companhia específica (American Airlines)
- Chave 'AA' funcionando corretamente

#### 4. **Navegação para SPFLI** 🔗
```
GET /sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet('AA')/ToSpfliNav?$format=json
```
**✅ Resultado**: 
- Rotas da American Airlines (SPFLI)
- Navegação funcionando via association
- Relacionamento 1:N operacional

---

## 🌐 **Teste via Navegador Web**

### 🔗 **URLs para Teste Direto**

#### 📜 **Metadata**:
```
http://servidor:porta/sap/opu/odata/sap/ZPSILVA_GW_SRV
```

#### 📋 **Lista SCARR (XML)**:
```
http://servidor:porta/sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet
```

#### 📋 **Lista SCARR (JSON)**:
```
http://servidor:porta/sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet?$format=json
```

### 🔐 **Autenticação**:
- 👤 **Usuário/Senha**: Mesmo do ambiente SAP
- 🛡️ **Autenticação básica** HTTP

---

## 📊 **Estrutura dos Dados Retornados**

### ✈️ **Exemplo SCARRSet (JSON)**:
```json
{
  "d": {
    "results": [
      {
        "__metadata": {
          "uri": "http://servidor/sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet('AA')",
          "type": "ZPSILVA_GW_SRV.SCARR"
        },
        "Carrid": "AA",
        "CarrName": "American Airlines",
        "CurrCode": "USD",
        "Url": "http://www.aa.com",
        "ToSpfliNav": {
          "__deferred": {
            "uri": "http://servidor/sap/opu/odata/sap/ZPSILVA_GW_SRV/SCARRSet('AA')/ToSpfliNav"
          }
        }
      }
    ]
  }
}
```

### 🔗 **Propriedade de Navegação**:
- **ToSpfliNav**: 🔗 Link para rotas relacionadas
- 📍 **Implementada** via association SCARR→SPFLI

---

## 🎯 **Resumo do Serviço Ativo**

### ✅ **Funcionalidades Testadas e Validadas:**

| Funcionalidade | Status | Método |
|----------------|--------|---------|
| **Metadata** | ✅ | GET |
| **Lista SCARR** | ✅ | GET_ENTITYSET |
| **Registro único SCARR** | ✅ | GET_ENTITY |
| **Navegação SCARR→SPFLI** | ✅ | GET via association |
| **Formato XML** | ✅ | $format=xml |
| **Formato JSON** | ✅ | $format=json |

### 🌐 **Endpoints Disponíveis**:
```
/sap/opu/odata/sap/Z{USUARIO}_GW_SRV/SCARRSet
/sap/opu/odata/sap/Z{USUARIO}_GW_SRV/SCARRSet('{key}')
/sap/opu/odata/sap/Z{USUERIO}_GW_SRV/SCARRSet('{key}')/ToSpfliNav
/sap/opu/odata/sap/Z{USUARIO}_GW_SRV/SPFLISet
/sap/opu/odata/sap/Z{USUARIO}_GW_SRV/SPFLISet('{key1}','{key2}')
```

---

## 💡 **Próximos Passos**

### 🚀 **Melhorias para Próximas Aulas:**
- 🔧 **Extensão Chrome** para visualização JSON formatada
- 💻 **Implementação métodos CREATE/UPDATE/DELETE**
- 🧪 **Testes avançados** com filtros e ordenação
- 📱 **Consumo por aplicação Fiori**

### 🛠️ **Ferramentas Recomendadas:**
- 🌐 **JSON Formatter** (extensão Chrome)
- 🔧 **Postman** para testes avançados
- 📊 **SAP Gateway Client** para testes internos

---
*🎉 **Serviço OData ativo e testado com sucesso!** Próximo passo: implementar operações de escrita (CREATE, UPDATE, DELETE)!*