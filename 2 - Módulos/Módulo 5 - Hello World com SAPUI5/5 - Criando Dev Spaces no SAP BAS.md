# 🛠️ Creating a Dev Space in SAP Business Application Studio

### **📌 Lesson Overview**
Learn how to create and configure your development environment (Dev Space) in SAP Business Application Studio to start building SAP Fiori applications.

---

## 1. 🚀 Accessing Business Application Studio

### **📍 Navigation Steps**
1.  **🌐 Go to:** `account.hanatrial.ondemand.com`
2.  **🔐 Login** with your BTP trial credentials
3.  **🎯 Click on:** **"Business Application Studio"** from the cockpit homepage

### **⚠️ First-Time Access**
*   **📋 Permission Prompts:** You may see authorization requests on first login
*   **✅ Accept** all required permissions
*   **🏠 Welcome Screen:** You'll land on the BAS homepage

---

## 2. 🏗️ Creating Your Dev Space

### **🎯 What is a Dev Space?**
*   **💻 Virtual Machine:** A Linux-based development environment
*   **🛠️ Development Container:** Where all your applications will run
*   **🔧 Isolated Workspace:** Separate environment for your projects

### **👣 Step-by-Step Creation**

1.  **➕ Click "Create Dev Space"**
2.  **✏️ Enter Name:** `dev-fiori-apps` (or your preferred name)
3.  **📋 Select Application Type:**

| Type | Description | Our Choice |
|------|-------------|------------|
| **SAP Fiori** | For Fiori applications | ✅ **SELECT THIS** |
| **Low Code/No Code** | Visual development | |
| **Full Stack Cloud** | Full stack applications | |
| **SAP HANA Native** | HANA database apps | |
| **SAP Mobile** | Mobile applications | |
| **Basic** | Minimal setup | |

---

## 3. ⚙️ Configuring Extensions

### **🔧 Recommended Extensions**
Select these extensions for Fiori development:

| Extension | Purpose | Required |
|-----------|---------|----------|
| **📦 HTML5 Application Template** | Fiori app templates | ✅ **YES** |
| **🚀 Launchpad Module** | Custom launchpad development | ✅ **YES** |
| **🎨 Basic Fiori Template** | Basic Fiori components | ✅ **YES** |
| **🔧 Application Studio Extension Development** | BAS customization | ✅ **YES** |
| **📊 CDS Tools** | Core Data Services | Optional |
| **☁️ CAP Tools** | Cloud Application Programming | Optional |
| **🗄️ Database Explorer** | Database management | Optional |

### **💡 Pro Tip**
*   **🎯 Trial Account:** You can select multiple extensions in trial
*   **🔄 Flexibility:** You can create different Dev Spaces for different project types

---

## 4. ⏳ Deployment & Setup

### **🔄 Creation Process**
1.  **🚀 Click "Create Dev Space"**
2.  **⏰ Wait 5-10 minutes** for provisioning
3.  **📊 Status:** Watch for **"Running"** status
4.  **💾 Storage:** ~4GB disk space allocated per Dev Space

### **⚡ Important Limits**
*   **🔢 Maximum:** **2 Dev Spaces** allowed in trial account
*   **⏰ Auto-Delete:** Inactive Dev Spaces are deleted after **30 days**
*   **💾 Storage:** 4GB maximum per Dev Space

---

## 5. 💾 Managing Your Code

### **📚 Version Control Strategy**
To prevent code loss, use these methods:

| Method | Description | Recommendation |
|--------|-------------|----------------|
| **🔗 Git Integration** | Connect to GitHub/GitLab | ✅ **HIGHLY RECOMMENDED** |
| **💾 Export Files** | Download projects as archives | Good for backups |
| **🔄 Local Versioning** | Sync with local machine | Additional safety |

### **🛠️ Setup Steps in BAS**
1.  **📁 Open Workspace:**
    *   Go to **File** → **Open Workspace**
    *   Select **`/home/user/projects/`** folder
    *   Click **"Open"**
2.  **🌳 Project Structure:** All projects will appear under the `projects` folder

---

## 6. 🎨 BAS Interface Overview

### **🖥️ Key Sections**
*   **👋 Welcome Page:** Quick start guides and templates
*   **🔗 Git Clone:** Import existing repositories
*   **💻 Terminal:** Linux command line access
*   **📁 File Explorer:** Navigate your project structure
*   **🔄 Workspace Management:** Switch between workspaces

### **🔧 Development Tools**
*   **⌨️ Terminal:** Full Linux command line access
*   **📦 NPM/Git:** Pre-installed development tools
*   **🎨 Fiori Tools:** Specialized Fiori development extensions

---

## 7. ✅ Next Steps & Best Practices

### **🎯 Immediate Actions**
1.  **📁 Set up workspace** in `/home/user/projects/`
2.  **🔗 Configure Git** for version control
3.  **📚 Explore templates** and samples

### **📝 Important Reminders**
*   **💾 Backup Regularly:** Use Git to avoid losing work
*   **🔄 Keep Active:** Log in periodically to prevent auto-deletion
*   **🔧 Customize:** Install additional extensions as needed

---

## 8. 🎉 Ready for Development!

### **✅ Current Status**
*   ✅ **Dev Space Created**
*   ✅ **Extensions Configured**
*   ✅ **Workspace Setup**
*   ✅ **Environment Ready**

### **🚀 What's Next?**
In the next lessons, we'll:
*   Configure remaining BAS settings
*   Start developing our first Fiori applications
*   Learn BAS-specific development workflows

---

### **📋 Summary Checklist**
- [x] **Logged into BTP Cockpit**
- [x] **Accessed Business Application Studio**
- [x] **Created Dev Space with Fiori template**
- [x] **Selected recommended extensions**
- [x] **Waited for Running status**
- [x] **Opened workspace in projects folder**
- [x] **Ready for next lesson!**

**Your development environment is now ready! 🎊**