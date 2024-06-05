---
title: AEM Repo Tool
description: AEM AEM La Herramienta de Repo es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor de la a través de una línea de comandos comparable a la de FTP.
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---

# AEM Repo Tool {#aem-repo-tool}

AEM AEM La Herramienta de Repo es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor de la a través de una línea de comandos comparable a la de FTP. AEM La herramienta de repo de datos es similar a la de la variable [Complemento Jackrabbit FileVault Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin), pero es más rápido, tiene dependencias mínimas y es un script bash simple.

Esta herramienta simplifica la transferencia de archivos para el desarrollador y también se puede integrar en Eclipse e IntelliJ para hacer el desarrollo aún más eficiente.

## Información general {#overview}

Para una ruta determinada dentro de un `jcr_root` AEM Estructura FileVault en el sistema de archivos, la herramienta de repositorio de datos crea un paquete con un solo filtro para todo el subárbol y lo envía al servidor (similar al FTP) `put`), lo recupera del servidor ( `get`) o compara las diferencias ( `status` y `diff`).

La herramienta no admite varias rutas de filtro ni de FileVault `filter.xml`.

>[!CAUTION]
>
>AEM La herramienta de repositorio de datos siempre sobrescribe todo el archivo o directorio especificado.

## Descarga y documentación {#download-and-documentation}

El [AEM La herramienta de repo está disponible en GitHub a través de este vínculo](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) junto con instrucciones detalladas de instalación y uso.

AEM Si desea descargar la fuente de la herramienta de repo de, consulte el proyecto de GitHub vinculado a continuación.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto de herramientas en GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
