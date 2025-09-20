---
title: Introdução
description: Subplataforma principal
source: https://moovi.curseduca.pro/m/lessons/fiori-freestyle-1734443760098
created: "2025-09-17"
tags:
  - hover-notes
  - curseduca
---

## 🔌 Backend with SAP Gateway and OData
This module covers how to build the backend using **SAP NetWeaver Gateway** with **OData services**.  

---

### 📑 Agenda
- 🌐 Introduction to SAP Gateway  
- 🏗️ Architecture of SAP Gateway  
- ❓ What is SAP Gateway?  

---

### ❓ What is SAP Gateway?
- A **set of components (add-on)** of **SAP NetWeaver**.  
- Allows interfaces with **REST architecture** via the **OData protocol**.  

**Key Components:**  
- ⚙️ `GW_CORE`  
- 🏛️ `IW_FND`  
- 🔌 `IW_BEP`  
- 🗄️ `IW_HDB`  
- 📤 `IW_PGW`  
- 📡 `IW_GIL`  
- 🔎 `IW_SPI`  

---

### 🏗️ SAP Gateway Architecture
- Installed as **add-ons in the SAP NetWeaver environment**.  
- Composed of **two main layers**:  

#### 1️⃣ OData Runtime
- 📦 **Components**: `GW_CORE`, `IW_FND`  
- Provides: OData functionalities, foundation services, metadata, monitoring, tracing, and security.  

#### 2️⃣ Design Time & Service Provider Runtime
- 📦 **Components**: `IW_BEP`, `IW_HDB`, `IW_PGW`, `IW_GIL`, `IW_SPI`  
- Enables connection with the **SAP Business Suite** (S/4HANA or ECC).  
- Provides adapters for HANA, Analytics, Workflow, CRM, FI, MM, HCM, PLM, etc.  

---

### 🧩 SAP Gateway Architecture (Detailed – v7.2)
**SAP NetWeaver Gateway Tier**  
- 🔧 Core: `IW_FND`, `GW_CORE`  
- 📚 OData Library & Runtime: Metadata Repository, Events, Supportability, Monitoring & Tracing  
- 👤 Consumers interact here  

**SAP Business Suite Tier**  
- 🛠️ Development Tools & Service Builder  
- 🔌 Service Provider Implementation: `IW_BEP`  
- 🔗 Data Connectivity: BAPI, RFC, BOL, SPI, HANA, Analytics  
- 📊 Connects with ERP, CRM, SRM, BW, HANA  

---

### 🌀 SAP Gateway Component Evolution
- **Up to v7.31**  
  - Core: `GW_CORE`, `IW_FND`  
  - Backend Enablement: `IW_BEP`  

- **As of v7.40+**  
  - 🔄 Unified into: `SAP_GWFND`  
  - Simplifies architecture by consolidating **core + backend enablement**  

---

### 🌍 SAP Gateway Macro View
- Acts as **middleware**:  
  - 📥 Receives HTTP requests  
  - 📤 Exposes **OData services**  
  - 🖥️ Clients consume via HTTP  

---

### 🔀 Communication Flow
- **Separate Gateway Scenario**  
  - 🌐 HTTP request → Gateway  
  - 🔗 Gateway → Backend ERP (via **RFC**)  

- **Integrated Scenario**  
  - Gateway + ERP in a single environment  
  - ✅ Simplifies communication  
