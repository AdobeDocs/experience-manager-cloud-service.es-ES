---
title: AEM Repo Tool
description: La herramienta AEM Repo Tool es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor de AEM a través de la línea de comandos comparable a FTP.
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---

# AEM Repo Tool {#aem-repo-tool}

La herramienta AEM Repo Tool es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor de AEM a través de la línea de comandos comparable a FTP. La herramienta AEM Repo Tool es similar al [complemento Jackrabbit FileVault Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin), pero es más rápida, tiene dependencias mínimas y es un script bash simple.

Esta herramienta simplifica la transferencia de archivos para el desarrollador y también se puede integrar en Eclipse e IntelliJ para hacer el desarrollo aún más eficiente.

## Información general {#overview}

Para una ruta determinada dentro de una estructura de `jcr_root` FileVault en el sistema de archivos, la herramienta AEM Repo crea un paquete con un solo filtro para todo el subárbol y lo inserta en el servidor (similar a FTP `put`), lo recupera del servidor ( `get`) o compara las diferencias ( `status` y `diff`).

La herramienta no admite varias rutas de filtro o `filter.xml` de FileVault.

>[!CAUTION]
>
>La herramienta AEM Repo siempre sobrescribe todo el archivo o directorio especificado.

## Descarga y documentación {#download-and-documentation}

La herramienta [AEM Repo Tool está disponible en GitHub a través de este enlace](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) junto con instrucciones detalladas de instalación y uso.

Si desea descargar el origen de la herramienta AEM Repo Tool, consulte el proyecto de GitHub vinculado a continuación.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto de herramientas en GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
