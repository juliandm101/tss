🛠️ Microsoft TSS (Troubleshooting Script/Session)
¿Qué es TSS?
TSS (Troubleshooting Script/Session) es una herramienta fundamental de diagnóstico de Microsoft utilizada por los ingenieros de soporte para la recopilación automatizada de datos (logs, trazas de red, información del sistema) necesarios para resolver problemas complejos.

Aunque su uso más conocido es en la depuración de aplicaciones como Microsoft Teams y Skype for Business, la filosofía del TSS se extiende a varios productos de Microsoft que requieren una visión profunda del estado del sistema en el momento en que ocurre un fallo o un comportamiento anómalo.

🎯 Propósito y Beneficios
El objetivo principal de TSS es asegurar que el soporte técnico reciba un conjunto de datos completo y preciso sin requerir que el usuario realice manualmente múltiples pasos de registro.

Característica

Descripción

Recolección Centralizada

Consolida varios tipos de registros y datos en un único archivo comprimido.

Precisión Temporal

Captura la actividad del sistema exactamente durante el período de la reproducción del problema.

Trazas de Red Detalladas

Incluye datos de red (como ETL, Netsh, o Wireshark logs) cruciales para problemas de conectividad o rendimiento.

Datos de Sistema

Recopila automáticamente detalles de configuración del sistema operativo, versiones de software y hardware relevante.

⚙️ Uso Básico (Flujo de Trabajo)
La herramienta TSS generalmente se ejecuta siguiendo estos pasos:

Inicio del Script: Un ingeniero de soporte de Microsoft proporciona un script (a menudo un archivo PowerShell o un ejecutable) configurado específicamente para el problema en cuestión.

Reproducción: El usuario inicia la herramienta TSS y luego inmediatamente reproduce el problema que está experimentando (por ejemplo, iniciar una llamada que falla o un error de aplicación).

Captura de Datos: Mientras el problema se reproduce, TSS registra la actividad del sistema, la red y la aplicación.

Finalización y Compresión: Una vez finalizada la reproducción, el usuario detiene la captura. TSS automáticamente comprime todos los logs y trazas generadas en un paquete .zip o .cab listo para ser enviado a Microsoft.

⚠️ Nota Importante sobre Privacidad
Dado que TSS recopila información detallada del sistema y trazas de red, es esencial:

Ejecutarlo solo bajo la guía del soporte técnico de Microsoft.

Asegurarse de comprender qué datos se están recopilando antes de iniciar la sesión.

Eliminar el paquete de logs una vez que el problema haya sido resuelto, para proteger la información del sistema.

💡 Tip:
Si estás documentando un procedimiento de soporte, siempre incluye la versión específica de TSS utilizada, ya que la herramienta recibe actualizaciones continuas.
