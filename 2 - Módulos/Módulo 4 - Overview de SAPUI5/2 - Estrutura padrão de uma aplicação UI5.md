# 🏗️ SAP UI5 Application Structure - Complete Guide

## 🎯 **Lesson Overview**

### **Objective:**
Understand the standard folder structure and MVC architecture of SAP UI5 applications for effective Fiori development

---

## 🏛️ **MVC Architecture in SAP UI5**

### 📋 **Three-Layer Architecture:**

| Layer | Responsibility | Technology |
|-------|----------------|------------|
| **Model** | Data management & structure | OData, JSON, XML |
| **View** | User interface presentation | XML, HTML, JavaScript |
| **Controller** | Business logic & event handling | JavaScript |

### 🔄 **Data Flow:**
```
View (UI) ↔ Controller (Logic) ↔ Model (Data)
```

### 💡 **MVC Benefits:**
- ✅ **Separation of concerns** - Clean code organization
- ✅ **Reusability** - Components can be reused
- ✅ **Maintainability** - Easier to update and debug
- ✅ **Team collaboration** - Parallel development

---

## 📁 **Standard SAP UI5 Folder Structure**

### 🗂️ **Complete Project Structure:**
```
my-ui5-app/
├── 📁 webapp/
│   ├── 📁 controller/          # JavaScript controllers
│   ├── 📁 css/                # Custom styles
│   ├── 📁 i18n/              # Internationalization
│   ├── 📁 localService/      # Mock data for development
│   ├── 📁 model/            # Data models & formatters
│   ├── 📁 view/             # XML views
│   ├── 📄 Component.js      # Application bootstrap
│   ├── 📄 manifest.json     # Application configuration
│   └── 📄 index.html        # Entry point (standalone)
├── 📄 package.json          # Node.js dependencies
├── 📄 ui5.yaml             # Development configuration
└── 📄 .env                 # Environment variables
```

---

## 🔧 **Detailed Folder Explanations**

### 🎮 **1. Controller Folder (`/controller/`)**

#### **Purpose:**
- Contains **JavaScript files** with application logic
- Handles **user interactions** and events
- Manages **data flow** between Model and View

#### **Example Structure:**
```javascript
// Main.controller.js
sap.ui.define([
    "sap/ui/core/mvc/Controller",
    "sap/m/MessageToast"
], function(Controller, MessageToast) {
    "use strict";
    
    return Controller.extend("my.app.controller.Main", {
        onInit: function() {
            // Initialization logic
        },
        
        onButtonPress: function(oEvent) {
            MessageToast.show("Button clicked!");
        },
        
        onNavigation: function() {
            // Navigation logic
        }
    });
});
```

#### **Best Practices:**
- One controller per view
- Keep controllers focused and lightweight
- Use meaningful method names

### 🎨 **2. CSS Folder (`/css/`)**

#### **Purpose:**
- **Custom styling** beyond standard Fiori theme
- **Brand-specific** modifications
- **Responsive design** adjustments

#### **Example Usage:**
```css
/* custom.css */
.myCustomButton {
    background-color: #0070f3;
    border-radius: 8px;
}

.myCustomHeader {
    font-family: 'Segoe UI', sans-serif;
    font-size: 1.5rem;
}
```

### 🌍 **3. i18n Folder (`/i18n/`)**

#### **Purpose:**
- **Internationalization** files for multiple languages
- **Text translations** and localization
- **Maintains consistency** across languages

#### **File Structure:**
```
i18n/
├── i18n.properties        # Default language (English)
├── i18n_pt.properties    # Portuguese
├── i18n_es.properties    # Spanish
└── i18n_de.properties    # German
```

#### **Example Content:**
```properties
# i18n.properties
welcomeMessage=Welcome to our Application
submitButton=Submit Form
errorTitle=Error Occurred

# i18n_pt.properties
welcomeMessage=Bem-vindo ao nosso Aplicativo
submitButton=Enviar Formulário
errorTitle=Erro Ocorrido
```

#### **Usage in Views:**
```xml
<!-- In XML View -->
<Button text="{i18n>submitButton}" />
<Text text="{i18n>welcomeMessage}" />
```

### 🧪 **4. LocalService Folder (`/localService/`)**

#### **Purpose:**
- **Mock data** for development without backend
- **Parallel development** - frontend/backend teams
- **Testing** scenarios and edge cases

#### **Typical Contents:**
```
localService/
├── metadata.xml          # OData service metadata
└── mockdata/
    ├── Products.json
    ├── Customers.json
    └── Orders.json
```

### 📊 **5. Model Folder (`/model/`)**

#### **Purpose:**
- **Data models** (JSON, XML, OData)
- **Custom formatters** for data display
- **Data validation** and transformation logic

#### **Example Formatter:**
```javascript
// formatter.js
sap.ui.define([], function() {
    "use strict";
    
    return {
        formatCurrency: function(value) {
            if (!value) return "";
            return new Intl.NumberFormat('en-US', {
                style: 'currency',
                currency: 'USD'
            }).format(value);
        },
        
        formatStatus: function(status) {
            const statusMap = {
                'A': 'Active',
                'I': 'Inactive',
                'P': 'Pending'
            };
            return statusMap[status] || status;
        }
    };
});
```

### 🖼️ **6. View Folder (`/view/`)**

#### **Purpose:**
- **XML files** defining the user interface
- **UI controls** and layout definitions
- **Data binding** declarations

#### **Example XML View:**
```xml
<!-- Main.view.xml -->
<mvc:View
    controllerName="my.app.controller.Main"
    xmlns:mvc="sap.ui.core.mvc"
    xmlns="sap.m">
    
    <Page title="{i18n>welcomeMessage}">
        <content>
            <Button 
                text="{i18n>submitButton}"
                press="onButtonPress"
                class="myCustomButton"/>
                
            <List items="{/Products}">
                <items>
                    <StandardListItem
                        title="{Name}"
                        description="{Category}"
                        info="{Price}"/>
                </items>
            </List>
        </content>
    </Page>
</mvc:View>
```

---

## ⚙️ **Configuration Files**

### 🚀 **1. Component.js**

#### **Purpose:**
- **Application bootstrap** and initialization
- **Metadata** definition
- **Lifecycle management**

#### **Key Features:**
```javascript
sap.ui.define([
    "sap/ui/core/UIComponent"
], function(UIComponent) {
    "use strict";
    
    return UIComponent.extend("my.app.Component", {
        metadata: {
            manifest: "json"
        },
        
        init: function() {
            UIComponent.prototype.init.apply(this, arguments);
            this.getRouter().initialize();
        }
    });
});
```

### 📋 **2. manifest.json**

#### **Purpose:**
- **Central configuration** file
- **Application metadata** and settings
- **Data source** definitions
- **Routing** configuration

#### **Key Sections:**
```json
{
    "sap.app": {
        "id": "my.application",
        "type": "application",
        "title": "My Fiori App",
        "description": "A custom Fiori application"
    },
    "sap.ui5": {
        "models": {
            "i18n": {
                "type": "sap.ui.model.resource.ResourceModel",
                "settings": {
                    "bundleName": "my.app.i18n.i18n"
                }
            },
            "": {
                "type": "sap.ui.model.odata.v2.ODataModel",
                "settings": {
                    "serviceUrl": "/sap/opu/odata/sap/MY_SERVICE/"
                }
            }
        },
        "routing": {
            "config": {
                "routerClass": "sap.m.routing.Router"
            },
            "routes": [
                {
                    "name": "main",
                    "pattern": "",
                    "target": "main"
                }
            ]
        }
    }
}
```

### 📦 **3. package.json**

#### **Purpose:**
- **Node.js dependencies**
- **Build scripts** and commands
- **Development tools** configuration

#### **Example:**
```json
{
    "name": "my-ui5-app",
    "version": "1.0.0",
    "scripts": {
        "start": "ui5 serve",
        "build": "ui5 build",
        "deploy": "ui5 build --dest ./dist"
    },
    "devDependencies": {
        "@ui5/cli": "^2.0.0",
        "@ui5/webcomponents": "^1.0.0"
    }
}
```

### ⚙️ **4. ui5.yaml**

#### **Purpose:**
- **UI5-specific configuration**
- **Development server** settings
- **Proxy configuration** for backend calls

#### **Example:**
```yaml
specVersion: '2.1'
metadata:
  name: my.ui5.app
type: application
server:
  customMiddleware:
    - name: ui5-middleware-simpleproxy
      afterMiddleware: compression
      configuration:
        baseUri: "https://my-backend-system.com"
```

---

## 🎯 **Development Workflow**

### 🔄 **Typical Development Process:**

1. **Setup** - Create project structure using templates
2. **Configure** - Update manifest.json with app details
3. **Develop Views** - Create XML views in `/view/` folder
4. **Add Logic** - Implement controllers in `/controller/`
5. **Style** - Customize appearance in `/css/`
6. **Internationalize** - Add translations in `/i18n/`
7. **Test** - Use mock data from `/localService/`
8. **Deploy** - Build and deploy to SAP system

### 💡 **Pro Tips:**

#### **For Fiori Launchpad:**
- Use **Component.js** as entry point
- Configure in **SAP Fiori Launchpad designer**
- Follow **Fiori design guidelines**

#### **For Standalone Apps:**
- Use **index.html** as entry point
- Can run outside Fiori Launchpad
- Good for external users or mobile apps

#### **Best Practices:**
- Keep **controllers thin** - move logic to models
- Use **data binding** instead of manual DOM manipulation
- Follow **consistent naming conventions**
- Use **i18n** from day one for text strings

---

## 🚀 **Ready for Development!**

### ✅ **What You Now Understand:**
- SAP UI5 **MVC architecture** and data flow
- Complete **folder structure** and purposes
- **Configuration files** and their roles
- **Development workflow** and best practices

### 🎯 **Next Steps:**
You're now ready to start **building real SAP UI5 applications** using this structured approach. In the next lessons, you'll create your first application using this architecture!

---
*🏗️ **SAP UI5 structure mastered! Ready to build professional Fiori applications!** 🚀*