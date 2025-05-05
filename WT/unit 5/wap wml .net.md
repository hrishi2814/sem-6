# **Concepts of WAP, WML, and .NET Framework**

## **1. WAP (Wireless Application Protocol)**
### **Overview**
- A **communication protocol** designed for mobile devices to access internet services.
- Enables lightweight web browsing on early mobile phones (pre-smartphone era).

### **Key Features**
✔ Designed for low-bandwidth, high-latency networks  
✔ Uses **WML** (Wireless Markup Language) instead of HTML  
✔ Supports limited graphics and text-based content  

### **WAP Architecture**
1. **Mobile Device** → Sends WAP request  
2. **WAP Gateway** → Translates WAP ↔ HTTP  
3. **Web Server** → Returns WML content  

### **Decline**
- Phased out with the rise of **3G/4G and smartphones** (HTML5 replaced WML).

---

## **2. WML (Wireless Markup Language)**
### **Overview**
- An **XML-based markup language** for WAP devices (like HTML for mobile).
- Designed for small screens and limited resources.

### **Key Features**
✔ **Card-based navigation** (Pages are called "cards" in a "deck")  
✔ Minimalist design (text-focused, limited images)  
✔ No JavaScript/CSS support  

### **Example WML Code**
```xml
<wml>
  <card id="home" title="Welcome">
    <p>Hello, Mobile User!</p>
    <do type="accept" label="Next">
      <go href="#nextCard"/>
    </do>
  </card>
</wml>
```

### **Legacy**
- Obsolete today (modern mobile sites use **responsive HTML5**).

---

## **3. .NET Framework**
### **Overview**
- A **Microsoft-developed platform** for building Windows applications and web services.
- Supports multiple languages (C#, VB.NET, F#).

### **Key Components**
| Component | Purpose |
|-----------|---------|
| **CLR (Common Language Runtime)** | Executes .NET code, manages memory |
| **FCL (Framework Class Library)** | Prebuilt classes for I/O, databases, etc. |
| **ASP.NET** | Web framework for dynamic sites |
| **WinForms/WPF** | Desktop app development |
| **ADO.NET** | Database connectivity |

### **Advantages**
✅ **Language interoperability** (C#, VB.NET, etc.)  
✅ **Automatic memory management** (Garbage Collection)  
✅ **Security & Scalability**  
✅ **Unified API** for web/desktop/mobile  

### **Example: C# in .NET**
```csharp
using System;

class Program {
  static void Main() {
    Console.WriteLine("Hello, .NET!"); 
  }
}
```

### **Evolution**
- **.NET Core** (Cross-platform successor) → Now called **.NET 5+**.

---

## **Comparison Table**
| Concept | Purpose | Status |
|---------|---------|--------|
| **WAP** | Mobile internet access | Obsolete |
| **WML** | Mobile-friendly markup | Obsolete |
| **.NET** | Windows/web development | Active (.NET 6+) |

---

## **Summary**
- **WAP/WML** → Early mobile web tech (replaced by HTML5/4G).  
- **.NET Framework** → Robust platform for Windows apps (evolved into .NET 6+).  

