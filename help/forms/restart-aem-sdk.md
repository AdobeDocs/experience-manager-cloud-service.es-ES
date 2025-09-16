---
title: ¿Cómo reiniciar el SDK de AEM?
description: Prácticas recomendadas para reiniciar el SDK de AEM
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: ht
source-wordcount: '102'
ht-degree: 100%

---

# Reinicio del SDK de AEM

Si reinicia el SDK de AEM deteniendo los procesos de Java™, puede dar lugar a incoherencias en el entorno de desarrollo de AEM y producirse un error como:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/assets/restart-sdk-error.png)

## Solución

Para reiniciar el SDK de AEM, vaya a la ventana de comandos activa y pulse el comando `Ctrl + C` para reiniciar el SDK.

Se recomienda utilizar el comando “Ctrl + C” para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java™, puede generar incoherencias en el entorno de desarrollo de AEM.

## Consulte también

* [Configurar un entorno de desarrollo local para AEM Forms](/help/forms/setup-local-development-environment.md)

