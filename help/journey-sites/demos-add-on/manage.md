---
title: Administrar los sitios de muestra
description: Obtenga información sobre las herramientas disponibles para ayudarle a administrar los sitios de muestra y cómo eliminarlos.
exl-id: 988c6e09-c43e-415f-8d61-998c294c5a11
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 94%

---

# Administrar los sitios de muestra {#manage-demo-sites}

Obtenga información sobre las herramientas disponibles para ayudarle a administrar los sitios de muestra y cómo eliminarlos.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido del complemento de demostraciones de referencia de AEM, [Creación de un sitio,](create-site.md) ha creado un nuevo sitio de muestra basado en las plantillas del complemento de demostraciones de referencia. Ahora debería hacer lo siguiente:

* Comprender cómo acceder al entorno de creación de AEM.
* Saber cómo crear un sitio basado en una plantilla.
* Entender los conceptos básicos para navegar por la estructura del sitio y editar una página.

Si además [ha habilitado AEM Screens para su sitio de muestra,](screens.md) también puede hacer lo siguiente:

* Conocer los conceptos básicos de AEM Screens.
* Comprender el contenido de la demostración de We.Cafe.
* Saber cómo configurar AEM Screens para We.Cafe.

Ahora que tiene su propio sitio de muestra para explorar, este artículo describe las herramientas disponibles para administrar sus sitios de demostración y las formas de eliminarlos.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo administrar los sitios de muestra que ha creado. Después de leer, debería haber logrado lo siguiente:

* Obtenga información sobre cómo acceder a las utilidades de demostración de autoservicio.
* Conozca qué utilidades están disponibles para usted.
* Cómo eliminar un sitio de muestra o una plantilla existentes.

## Acceso a las utilidades de demostración de autoservicio {#accessing-utilities}

Ahora que tiene sus propios sitios de muestra, probablemente le gustaría saber cómo puede administrarlos. La canalización no solo implementó las plantillas de sitio para dar contenido a los sitios de muestra, sino también un conjunto de utilidades para administrar esos sitios.

1. En la barra de navegación global de AEM, seleccione **Herramientas** -> **Demostraciones de referencia** -> **Utilidades de demostración de referencia**.

   ![Utilidades de demostración de autoservicio](assets/demo-utilities.png)

1. Utilidades de demostración de referencia es una colección de funcionalidades útiles que le ayudarán a configurar y monitorizar su entorno de Adobe Experience Manager. La vista inicial es el **Tablero**, que sirve como comprobación de estado del entorno y su funcionalidad de demostración.

   ![Tablero](assets/dashboard.png)

Utilidades de demostración de autoservicio proporciona una serie de herramientas.

* **Eliminar sitios**: seleccione el sitio que desee eliminar en esta instancia de Adobe Experience Manager. Tenga en cuenta que esta es una acción destructiva y no se puede deshacer una vez iniciada.
* **Eliminar plantillas de sitio**: seleccione la plantilla de sitio que desee eliminar en esta instancia de Adobe Experience Manager. Antes de eliminar una plantilla de sitio, asegúrese de que todos los sitios que hacen referencia a la plantilla también se eliminen. Tenga en cuenta que esta es una acción destructiva y no se puede deshacer una vez iniciada.
* **Preparación de la caché del autor**: esto recupera varios recursos dentro de la instancia de Adobe Experience Manager, lo que acelera los tiempos de recuperación. Puede tardar varios segundos.
* **Aplicación de Android**: herramientas para instalar e iniciar la aplicación de Android de demostración. Cree un sitio basado en la **Aplicación WKND de una sola página** para rellenar esta página. Puede utilizarse desde un dispositivo Android, emulador o Bluestacks.
* **Preferencias de usuario**: desactivar los cuadros de diálogo emergentes del tutorial.
* **Configuración de GraphQL**: configure rápidamente el punto de conexión global de GraphQL.

## Eliminación de sitios y plantillas de muestra {#deleting}

 Después de probar un conjunto de funcionalidades de AEM, es posible que ya no necesite el sitio de muestra o incluso la plantilla en la que se basa. Es fácil eliminar los sitios de muestra y las plantillas de sitio.

1. Acceda a las **Utilidades de demostración de referencia** y toque o haga clic en **Eliminar sitios**.

   ![Eliminar sitios](assets/delete-sites.png)

1. Los sitios disponibles se presentan en una lista. Compruebe el sitio o sitios que desea eliminar y, a continuación, toque o haga clic en **Eliminar**.

   >[!CAUTION]
   >
   >La eliminación de sitios y plantillas es una acción destructiva y no se puede deshacer una vez iniciada.

1. Confirme la eliminación del sitio en el cuadro de diálogo.

   ![Confirmar eliminación del sitio](assets/confirm-site-delete.png)

1. AEM elimina el sitio o sitios seleccionados y muestra su progreso donde anteriormente había el botón **Eliminar**.

   ![Eliminar progreso](assets/delete-progress.png)

El sitio se ha eliminado.

Puede eliminar las plantillas del mismo modo bajo el encabezado **Eliminar plantillas de sitio** en **Utilidades de demostración de referencia**.

>[!CAUTION]
>
>Antes de eliminar una plantilla de sitio, asegúrese de que todos los sitios que hacen referencia a la plantilla también se eliminen.

## ¿Fin del recorrido? {#end-of-journey}

¡Felicitaciones! Ha completado el recorrido del complemento de demostraciones de referencia de AEM. Ahora debería hacer lo siguiente:

* Obtenga información básica sobre Cloud Manager y comprenda cómo las canalizaciones envían contenido y configuración a AEM.
* Aprenda a utilizar Cloud Manager para crear un nuevo programa.
* Obtenga información sobre cómo activar el complemento de demostraciones de referencia para el nuevo programa y poder ejecutar una canalización para implementar el contenido del complemento.
* Obtenga información sobre cómo acceder al entorno de creación de AEM para crear un sitio basado en una plantilla.
* Obtenga información sobre cómo acceder a las utilidades de demostración de autoservicio.
* Aprenda cómo eliminar un sitio o plantilla de muestra existente.

Ya está listo para explorar las capacidades de AEM usando sus propios sitios de muestra. Aun así, AEM es una herramienta potente y hay muchas opciones adicionales disponibles. Consulte algunos de los recursos adicionales disponibles en la [sección de Recursos adicionales](#additional-resources) para obtener más información acerca de las funciones que ha visto en este recorrido.

## Recursos adicionales {#additional-resources}

* [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=es): si desea obtener más información sobre las funciones de Cloud Manager, puede consultar directamente los documentos técnicos detallados.
* [Crear sitio](/help/sites-cloud/administering/site-creation/create-site.md): aprenda a utilizar AEM para crear un sitio mediante plantillas para definir el estilo y la estructura del sitio.
* [Convenciones de asignación de nombres a páginas de AEM](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices). AEM : Consulte esta página para comprender las convenciones y la organización de páginas de la.
* [Gestión básica de AEM](/help/sites-cloud/authoring/getting-started/basic-handling.md): consulte este documento si es nuevo en AEM para comprender conceptos básicos como la navegación y la organización de la consola.
* [Documentación técnica de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es): si ya tiene una base firme de AEM, puede consultar directamente los documentos técnicos detallados.
* [Plantillas de sitio](/help/sites-cloud/administering/site-creation/site-templates.md): si desea obtener más información acerca de la estructura de las plantillas de sitios y cómo se utilizan para crear sitios, consulte este documento.
