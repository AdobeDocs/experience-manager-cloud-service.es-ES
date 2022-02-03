---
title: Administrar los sitios de demostración
description: Obtenga información sobre las herramientas disponibles para ayudarle a administrar sus sitios de demostración y cómo eliminarlos.
source-git-commit: df9b777e24e56ed0329895f833f50b45ecf2defa
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---


# Administrar los sitios de demostración {#manage-demo-sites}

Obtenga información sobre las herramientas disponibles para ayudarle a administrar sus sitios de demostración y cómo eliminarlos.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido del complemento de las demostraciones de referencia de AEM, [Crear sitio,](create-site.md) ha creado un nuevo sitio de demostración basado en las plantillas del complemento Demostración de referencia. Ahora debería:

* Obtenga información sobre cómo acceder al entorno de creación de AEM.
* Obtenga información sobre cómo crear un sitio basado en una plantilla.
* Comprender los conceptos básicos para navegar por la estructura del sitio y editar una página.

Si también [AEM Screens habilitado para su sitio de demostración,](screens.md) también debe:

* Conozca los conceptos básicos de AEM Screens.
* Comprender el contenido de la demostración de We.Cafe.
* Obtenga información sobre cómo configurar AEM Screens para We.Cafe.

Ahora que tiene su propio sitio de demostración para explorar, este artículo describe las herramientas disponibles para ayudarle a administrar sus sitios de demostración y cómo eliminarlos.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo puede administrar los sitios de demostración que ha creado. Después de leer, debe:

* Obtenga información sobre cómo acceder a las utilidades de demostración de autoservicio.
* Conozca qué utilidades están disponibles para usted.
* Cómo eliminar un sitio de demostración o una plantilla existentes.

## Acceso a las utilidades de demostración de autoservicio {#accessing-utilities}

Ahora que tiene sus propios sitios de demostración, probablemente le gustaría saber cómo puede administrarlos. La canalización no solo implementó las plantillas de sitio para dar contenido a los sitios de demostración, sino que también implementó un conjunto de utilidades para administrar esos sitios.

1. En la barra de navegación global de AEM, seleccione **Herramientas** -> **Demostraciones de referencia** -> **Utilidades de demostración de referencia**.

   ![Utilidades de demostración de autoservicio](assets/demo-utilities.png)

1. Reference Demo Utilities (Utilidades de demostración de referencia) es una colección de funcionalidades útiles que ayudarán a configurar y supervisar su entorno de Adobe Experience Manager. La vista inicial es la **Panel**, que sirve como comprobación de estado del entorno y su funcionalidad de demostración.

   ![Tablero](assets/dashboard.png)

Self-Service Demo Utilities proporciona una serie de herramientas.

* **Eliminar sitios** - Seleccione el sitio que desee eliminar en esta instancia de Adobe Experience Manager. Tenga en cuenta que esta es una acción destructiva y no se puede deshacer una vez iniciada.
* **Eliminar plantillas de sitio** - Seleccione la plantilla de sitio que desee eliminar en esta instancia de Adobe Experience Manager. Antes de eliminar una plantilla de sitio, asegúrese de que todos los sitios que hacen referencia a la plantilla también se eliminen. Tenga en cuenta que esta es una acción destructiva y no se puede deshacer una vez iniciada.
* **Caché de autor principal** : Esto recupera varios recursos dentro de la instancia de Adobe Experience Manager, lo que acelera los tiempos de recuperación. Puede tardar varios segundos.
* **Aplicación de Android** : Herramientas para instalar e iniciar la aplicación de Android de demostración. Cree un sitio basado en la variable **Aplicación de página única WKND** para rellenar esta página. Utilice desde un dispositivo Android, emulador o Bluestacks.
* **Preferencias de usuario** - Desactivar los cuadros de diálogo emergentes de tutorial.
* **Configuración de GraphQL** : configure rápidamente el extremo global de GraphQL.

## Eliminación de sitios y plantillas de demostración {#deleting}

Después de probar un conjunto de funcionalidades de AEM, es posible que ya no necesite el sitio de demostración o incluso la plantilla en la que se basa. Es fácil eliminar los sitios de demostración y las plantillas de sitio.

1. Acceda a la **Utilidades de demostración de referencia** y toque o haga clic en **Eliminar sitios**.

   ![Eliminar sitios](assets/delete-sites.png)

1. Los sitios disponibles se presentan en una lista. Compruebe el sitio o sitios que desea eliminar y, a continuación, toque o haga clic en **Eliminar**.

   >[!CAUTION]
   >
   >La eliminación de sitios y plantillas es una acción destructiva y no se puede deshacer una vez iniciada.

1. Confirme la eliminación del sitio en el cuadro de diálogo.

   ![Confirmar eliminación del sitio](assets/confirm-site-delete.png)

1. AEM elimina el sitio o sitios seleccionados y muestra su progreso donde el **Eliminar** anteriormente.

   ![Eliminar progreso](assets/delete-progress.png)

El sitio se ha eliminado.

Puede eliminar las plantillas del mismo modo en el encabezado **Eliminar plantillas de sitio** en el **Utilidades de demostración de referencia**.

>[!CAUTION]
>
>Antes de eliminar una plantilla de sitio, asegúrese de que todos los sitios que hacen referencia a la plantilla también se eliminen.

## ¿Fin del Recorrido? {#end-of-journey}

Felicitaciones! ¡Ha completado el recorrido de Complementos de las Demostraciones de Referencia de AEM! Ahora debería:

* Obtenga información básica sobre Cloud Manager y comprenda cómo las canalizaciones ofrecen contenido y configuración a AEM.
* Obtenga información sobre cómo utilizar Cloud Manager para crear un nuevo programa.
* Obtenga información sobre cómo activar el complemento Demostraciones de referencia para el nuevo programa y puede ejecutar una canalización para implementar el contenido del complemento.
* Obtenga información sobre cómo acceder al entorno de creación de AEM para crear un sitio basado en una plantilla.
* Obtenga información sobre cómo acceder a las utilidades de demostración de autoservicio.
* Obtenga información sobre cómo eliminar un sitio o plantilla de demostración existente.

Ya está listo para explorar las capacidades de AEM usando sus propios sitios de demostración. Sin embargo, AEM es una herramienta potente y hay muchas opciones adicionales disponibles. Consulte algunos de los recursos adicionales disponibles en la [Sección Recursos adicionales](#additional-resources) para obtener más información sobre las funciones que ha visto en este recorrido.

## Recursos adicionales {#additional-resources}

* [Documentación de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) : Si desea obtener más información sobre las funciones de Cloud Manager, puede consultar directamente los documentos técnicos detallados.
* [Crear sitio](/help/sites-cloud/administering/site-creation/create-site.md) - Aprenda a utilizar AEM para crear un sitio mediante plantillas de sitio para definir el estilo y la estructura del sitio.
* [AEM convenciones de nomenclatura de páginas.](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#page-name-restrictions-and-best-practices) - Consulte esta página para comprender las convenciones y la organización de AEM páginas.
* [Gestión básica de AEM](/help/sites-cloud/authoring/getting-started/basic-handling.md) : Explore este documento si es nuevo en AEM para comprender conceptos básicos como la navegación y la organización de la consola.
* [AEM documentación técnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=es) - Si ya tiene una comprensión firme de AEM, puede que desee consultar directamente los documentos técnicos detallados.
* [Plantillas de sitio](/help/sites-cloud/administering/site-creation/site-templates.md) - Si desea obtener más información sobre la estructura de las plantillas de sitio y cómo se utilizan para crear sitios, consulte este documento.
