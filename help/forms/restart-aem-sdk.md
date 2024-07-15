---
title: AEM ¿Cómo reiniciar el SDK de la?
description: AEM Prácticas recomendadas para reiniciar el SDK de la
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 62be3c6e98df9002cdfbeef50dd5475c4daa1576
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 27%

---

# AEM Reinicio del SDK de la

AEM AEM Si reinicia el SDK de la deteniendo los procesos de Java™, puede provocar incoherencias en el entorno de desarrollo de la y se producirá un error como el siguiente:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/assets/restart-sdk-error.png)

## Solución

AEM Para reiniciar el SDK de la, vaya a la ventana de comandos activa y pulse el comando `Ctrl + C` para reiniciar el SDK.

Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. AEM AEM El reinicio del SDK de la con métodos alternativos, como detener los procesos de Java™, puede generar incoherencias en el entorno de desarrollo de la.

## Ver también

* [Configurar un entorno de desarrollo local para AEM Forms](/help/forms/setup-local-development-environment.md)
* [Habilitar los componentes principales de los formularios adaptables](/help/forms/enable-adaptive-forms-core-components.md)
