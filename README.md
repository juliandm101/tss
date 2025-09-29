# Microsoft TSS (Troubleshooting Script Set)

## 📌 Introducción
**TSS (Troubleshooting Script Set)** es una herramienta oficial de Microsoft que reúne un conjunto de scripts diseñados para recopilar información de diagnóstico de forma estandarizada en **Windows** y **Azure**.  
Se utiliza principalmente para ayudar en la resolución de problemas de soporte técnico, ya que automatiza la recolección de **logs, configuraciones y datos del sistema**.

---

## ⚙️ Características principales
- 📄 **Recolección de logs** del sistema, eventos y configuraciones.  
- 🛠️ Compatible con **Windows Server y Windows Client**.  
- ☁️ Soporte para escenarios **on-premises** y **Azure**.  
- ⏱️ Ahorra tiempo al centralizar la recopilación de información para el soporte de Microsoft.  
- 🔒 Diseñado con foco en **seguridad y privacidad**: recolecta solo la información necesaria.

---

## 🚀 Instalación y uso
1. Descargar el paquete desde el [repositorio oficial de Microsoft](https://learn.microsoft.com/en-us/troubleshoot/windows-client/windows-client-others/tss).  
2. Ejecutar **PowerShell como administrador**.  
3. Importar y lanzar el script:  

```powershell
.\tss.ps1
