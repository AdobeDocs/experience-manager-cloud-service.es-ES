---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.7.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2021.7.0
feature: Release Information
exl-id: 7ef738a5-4657-482d-848b-e95e4fb816f9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 4%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.7.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.7.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic en [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.7.0 es el 15 de julio de 2021.


### Novedades {#what-is-new}

* Los clientes ahora pueden utilizar Azul 8 y 11 JDK para sus procesos de construcción de Cloud Manager y pueden seleccionar utilizar uno de estos JDK para complementos Maven compatibles con las cadenas de herramientas *o* la ejecución completa del proceso Maven.

* La dirección IP de salida saliente ahora se registrará en el archivo de registro de paso de compilación.

* Los entornos de fase y producción que ejecutan versiones antiguas de AEM ahora informarán del estado de **Actualización disponible**.

* El número máximo de certificados SSL admitidos ha aumentado a 20 por programa.

* El número máximo de dominios que se pueden configurar ha aumentado a 500 por entorno.

* La variable **Administrar Git** se ha cambiado **Acceder a información de Git** y el cuadro de diálogo se ha actualizado visualmente.

* La versión del tipo de archivo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 28.

### Correcciones de errores {#bug-fixes}

* En algunos casos, Vista previa no era una opción disponible al enlazar una Lista de permitidos IP a un entorno.

* La navegación manual a la página de detalles de ejecución para una ejecución no existente no mostraba un error, solo una pantalla de carga interminable.

* El mensaje de error que se muestra cuando se alcanza el número máximo de certificados SSL no es útil.

* En algunas circunstancias, podría haber una discrepancia en la versión de la canalización que se muestra en la tarjeta de la canalización en la **Información general** página.

* El asistente Agregar programa indicó incorrectamente que el nombre no se puede cambiar después de la creación.

### Problemas conocidos {#known-issues}

Los clientes que cambien a utilizar Azul JDKs deben tener en cuenta que no todas las aplicaciones existentes se compilarán sin error en Azul JDK. Se recomienda realizar pruebas locales antes de cambiar.
