---
title: AEM Repo Tool
description: La herramienta AEM Repo es una solución sencilla para transferir contenido JCR entre su sistema de archivos local y el servidor de AEM a través de la línea de comandos comparable a FTP.
exl-id: fb887ba3-e40b-4ab1-b142-0748c6d9f18e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 2%

---

# Herramienta AEM Repositorio {#aem-repo-tool}

La herramienta AEM Repo es una solución sencilla para transferir contenido JCR entre su sistema de archivos local y el servidor de AEM a través de la línea de comandos comparable a FTP. La herramienta Repositorio de AEM es similar a la [Complemento Jackrabbit FileVault Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin), pero es más rápido, tiene dependencias mínimas y es un script bash simple.

Esta herramienta simplifica la transferencia de archivos para el desarrollador y también se puede integrar en Eclipse e IntelliJ para que el desarrollo sea aún más eficiente.

## Información general {#overview}

Para una ruta determinada dentro de un `jcr_root` Estructura de FileVault en el sistema de archivos, la herramienta AEM Repo crea un paquete con un filtro único para todo el subárbol y lo empuja al servidor (similar a FTP) `put`), lo recupera del servidor ( `get`) o compara las diferencias ( `status` y `diff`).

La herramienta no admite varias rutas de filtro ni las de FileVault `filter.xml`.

>[!CAUTION]
>
>Tenga en cuenta que la herramienta AEM Repositorio siempre sobrescribirá todo el archivo o directorio especificado.

## Descargar y documentación {#download-and-documentation}

La variable [AEM herramienta Repositorio está disponible en GitHub a través de este enlace](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) junto con instrucciones detalladas de instalación y uso.

Si desea descargar la fuente de la herramienta de cesión temporal AEM, consulte el proyecto de GitHub que se muestra a continuación.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir un proyecto de herramientas en GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
