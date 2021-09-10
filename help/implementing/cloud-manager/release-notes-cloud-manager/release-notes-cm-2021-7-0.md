---
title: Notas de la versión para Cloud Manager en AEM as a Cloud Service Versión 2021.7.0
description: Notas de la versión para Cloud Manager en AEM as a Cloud Service Versión 2021.7.0
feature: Release Information
source-git-commit: a707968483dc1196628b737ad207bfefe63ca94b
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 4%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2021.7.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.7.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.7.0 es el 15 de julio de 2021.
La próxima versión está planificada para el 12 de agosto de 2021.

### Novedades {#what-is-new}

* Los clientes ahora pueden utilizar Azul 8 y 11 JDK para sus procesos de compilación de Cloud Manager y pueden seleccionar usar uno de estos JDK para complementos Maven compatibles con las cadenas de herramientas *o* para toda la ejecución del proceso Maven.

* La dirección IP de salida saliente ahora se registrará en el archivo de registro de paso de compilación.

* Los entornos de fase y producción que ejecutan versiones antiguas de AEM ahora informarán de un estado de **Actualización disponible**.

* El número máximo de certificados SSL admitidos ha aumentado a 20 por programa.

* El número máximo de dominios que se pueden configurar ha aumentado a 500 por entorno.

* Los botones **Administrar Git** se han cambiado a **Información de Git de acceso** y el cuadro de diálogo se ha actualizado visualmente.

* La versión del tipo de archivo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 28.

### Corrección de errores {#bug-fixes}

* En algunos casos, Vista previa no era una opción disponible al enlazar una Lista de permitidos IP a un entorno.

* La navegación manual a la página de detalles de ejecución para una ejecución no existente no mostraba un error, solo una pantalla de carga interminable.

* El mensaje de error que se muestra cuando se alcanza el número máximo de certificados SSL no es útil.

* En algunas circunstancias, podría haber una discrepancia en la versión de la versión mostrada en la tarjeta de canalización de la página **Información general**.

* El asistente Agregar programa indicó incorrectamente que el nombre no se puede cambiar después de la creación.

### Problemas conocidos {#known-issues}

Los clientes que cambien a utilizar Azul JDKs deben tener en cuenta que no todas las aplicaciones existentes se compilarán sin error en Azul JDK. Se recomienda realizar pruebas locales antes de cambiar.

