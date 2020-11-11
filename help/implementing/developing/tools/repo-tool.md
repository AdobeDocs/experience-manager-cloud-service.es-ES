---
title: Herramienta Repo AEM
description: La herramienta Repo de AEM es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor AEM a través de la línea de comandos comparable a FTP.
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# Herramienta Repo AEM {#aem-repo-tool}

La herramienta Repo de AEM es una solución sencilla para transferir contenido JCR entre el sistema de archivos local y el servidor AEM a través de la línea de comandos comparable a FTP. La herramienta Repo de AEM es similar al complemento [](https://jackrabbit.apache.org/filevault-package-maven-plugin)Jackrabbit FileVault Maven, pero es más rápida, tiene dependencias mínimas y es un script bash simple.

Esta herramienta simplifica la transferencia de archivos para el desarrollador y también se puede integrar en Eclipse e IntelliJ para hacer el desarrollo aún más eficiente.

## Información general {#overview}

Para una ruta determinada dentro de una estructura `jcr_root` FileVault en el sistema de archivos, la herramienta Repo de AEM crea un paquete con un único filtro para todo el subárbol y lo envía al servidor (similar a FTP `put`), lo recoge del servidor ( `get`) o compara las diferencias ( `status` y `diff`).

La herramienta no admite varias rutas de filtro ni las de FileVault `filter.xml`.

>[!CAUTION]
>
>Tenga en cuenta que la herramienta Repo AEM siempre sobrescribirá el archivo o directorio especificado.

## Descargar y documentación {#download-and-documentation}

La herramienta [AEM Repo está disponible en GitHub a través de este enlace](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) junto con instrucciones detalladas de instalación y uso.

Si desea descargar la fuente de la herramienta Repo AEM, consulte el proyecto GitHub que se encuentra a continuación.

CÓDIGO DE GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto de herramientas en GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)
