---
title: Publicación y cancelación de la publicación de formularios y documentos
seo-title: Publishing and unpublishing forms and documents
description: Puede programar la publicación y cancelación de la publicación de formularios. Los formularios publicados se replican en la instancia de publicación.
seo-description: You can schedule publishing and unpublishing of forms. Published forms are replicated on the publish instance.
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 0%

---


# Publicación y cancelación de la publicación de formularios y documentos{#publishing-and-unpublishing-forms-and-documents}

[!DNL AEM Forms] permite crear, publicar y cancelar la publicación de formularios fácilmente. La variable [!DNL AEM Forms] el servidor proporciona dos instancias: Autor y publicación. La instancia de autor se utiliza para crear y administrar recursos y recursos de formulario. La instancia de publicación sirve para mantener los recursos y recursos relacionados disponibles para los usuarios finales.

## Recursos admitidos   {#supported-assets-nbsp}

[!DNL AEM Forms] admiten los siguientes tipos de recursos:

* Formularios adaptables
* Documentos adaptables
* Fragmentos de formulario adaptable
* Temas
* Plantillas de formulario <!-- (XFA forms) -->
* PDF forms
* Documento (documentos PDF planos)
* Conjuntos de formularios
* Recurso (imágenes, esquemas y hojas de estilo)

Inicialmente, todos los recursos están disponibles solo en la instancia de autor. Un administrador o un autor de formularios pueden publicar todos los recursos excepto los recursos.

Al seleccionar un formulario y publicarlo, también se publican sus recursos y recursos relacionados. Sin embargo, los recursos dependientes no se publican. En este contexto, los recursos y recursos relacionados son recursos que un recurso publicado utiliza o a los que hace referencia. Los recursos dependientes son recursos que hacen referencia a un recurso publicado.

Su Forms adaptable puede utilizar algunas configuraciones, configuraciones y personalizaciones que no se publican automáticamente. Se recomienda publicar o activar estos recursos antes de publicar un formulario adaptable.

* Plantillas de formulario adaptable editables
* Configuraciones de Cloud Service para los modelos de datos de Adobe Sign, Typekit, reCAPTCHA y Form
* Otras configuraciones de Cloud Services solo se activan si el usuario tiene permisos de administración.
* Personalizaciones. Entre ellas se incluyen, entre otras:

   * Presentaciones personalizadas
   * Aspectos personalizados
   * Archivo CSS: tomado como entrada en el cuadro de diálogo Propiedades del contenedor de formulario adaptable
   * Categoría de biblioteca de cliente: se toma como entrada en el cuadro de diálogo Propiedades del contenedor de formulario adaptable
   * Cualquier otra biblioteca de cliente que se pueda incluir como parte de la plantilla de formulario adaptable.
   * Rutas de diseño

## Estados de los recursos {#asset-states}

Un recurso puede tener los siguientes estados:

* **Sin publicar:** Un recurso que nunca se ha publicado (el estado sin publicar solo es aplicable a los recursos de Forms). Los recursos de Gestión de correspondencia no tienen un estado No publicado).
* **Publicado**: Un recurso que se ha publicado y está disponible en la instancia de publicación
* **Modificado**: Un recurso que se modifica después de publicarse

## Publicar un recurso {#publish-an-asset}

1. Inicie sesión en la [!DNL AEM Forms] servidor.
1. Utilice una de las siguientes opciones para seleccionar y publicar un recurso.

   1. Mover el puntero sobre un recurso y tocar **[!UICONTROL Publicación]** ![aem6forms_global](assets/aem6forms_globe.pngasset.png).
   1. Realice una de las siguientes acciones y, a continuación, pulse Publicar :

      * Si está en la vista de tarjeta, pulse **[!UICONTROL Introducir selección]** ![aem6forms_check-círculo](assets/aem6forms_check-circle.png)y pulse el recurso. El recurso está seleccionado.
      * Si está en la vista de lista, seleccione la casilla de verificación de un recurso. El recurso está seleccionado.
      * Pulse un recurso para mostrar sus detalles.
      * Mostrar las propiedades de un recurso tocando Ver propiedades ![viewproperties](assets/viewproperties.png).

      >[!NOTE]
      >
      >No seleccione varios recursos. No se pueden publicar varios recursos a la vez.


1. Cuando se inicia el proceso de publicación, aparece un cuadro de diálogo de confirmación con todos los recursos y recursos relacionados. En el cuadro de diálogo que contiene recursos relacionados, pulse **[!UICONTROL Publicación]**. El recurso se publica y aparece el cuadro de diálogo de éxito Publicar recursos .

   >[!NOTE]
   >
   >Para Forms adaptable, junto con los recursos relacionados, también se muestra el nombre de la página Formulario adaptable .

   ![Un cuadro de diálogo de confirmación con todos los recursos y recursos relacionados](assets/p4.png)

   Cuadro de diálogo de confirmación con todos los recursos y recursos relacionados.

   >[!NOTE]
   >
   >En Forms Manager, si el usuario no tiene permiso para publicar los recursos de la lista, la acción Publicar está desactivada. Un recurso que requiere permisos adicionales se muestra en rojo.

   Una vez publicado un recurso, las propiedades de metadatos del recurso se copian en la instancia Publicar y el estado del recurso se cambia a Publicado. El estado de los recursos dependientes publicados también se cambia a Publicado.

   <!-- After publishing an asset, you can use the Forms Portal to display all the assets on a web page. For more information, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md).-->

## Publicar todos los recursos de gestión de correspondencia {#publish-all-the-correspondence-management-assets}

[!DNL AEM Forms] permite publicar todos los recursos de la gestión de correspondencia en un servidor de una sola vez. Los recursos publicados incluyen todos los recursos de Gestión de correspondencia y las dependencias relacionadas.

Complete los siguientes pasos para publicar todos los recursos de Gestión de correspondencia en un servidor:

1. Inicie sesión en la [!DNL AEM Forms] servidor.
1. Toque **Adobe Experience Manager** en la barra de navegación global.
1. Toque ![herramientas](assets/tools.png)y, a continuación, toque **Forms**.
1. Toque **Publicar recursos de gestión de correspondencia**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   Aparecerá la página Publicar todos los recursos de gestión de correspondencia y se mostrará la información sobre la última vez que se intentó el proceso de Publicar recursos de gestión de correspondencia.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. Toque **Publicación** y, en el mensaje de confirmación, pulse **OK**.

   Una vez completado un proceso por lotes, puede ver los detalles de la última ejecución. Esto incluye información como el inicio de sesión del administrador y si el lote se ejecuta correctamente o no.

   >[!NOTE]
   >
   >El proceso de publicación no se puede cancelar una vez iniciado. Además, mientras la operación Publicar está en curso, no cree, elimine, modifique ni publique ningún recurso ni inicie la operación Exportar todos los recursos de gestión de correspondencia.

## Automatizar la publicación y cancelación de publicaciones para Forms y documentos {#automate-publishing-and-unpublishing-for-forms-amp-documents}

[!DNL AEM Forms] permite programar la publicación y cancelación de publicaciones de recursos para Forms y documentos. Puede especificar la programación en el Editor de metadatos. Para obtener más información sobre la administración de metadatos de formulario, consulte [Administración de metadatos de formulario.](manage-form-metadata.md)

Siga estos pasos para programar la fecha y la hora de publicación y cancelación de la publicación de Forms &amp; Documents assets:

1. Seleccione un recurso y pulse **[!UICONTROL Ver propiedades]**. Se abre la página Propiedades de metadatos .
1. En la página Propiedades de metadatos , pulse **[!UICONTROL Avanzadas]** y, a continuación, toque **[!UICONTROL Editar]** ![illustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. En el **[!UICONTROL Publicar a tiempo]** y **[!UICONTROL Hora de publicación desactivada]** seleccione la fecha y la hora.\
   Toque **[!UICONTROL Listo]** ![aem6forms_check](assets/aem6forms_check.png).

## Cancelar la publicación de un recurso {#unpublish-an-asset}

1. Seleccione un recurso que se publique y pulse **[!UICONTROL Cancelar la publicación]** ![cancelar la publicación](assets/unpublish.png).
1. Utilice una de las siguientes opciones para seleccionar y cancelar la publicación de un recurso.

   1. Mover el puntero sobre un recurso y tocar **[!UICONTROL Cancelar la publicación]** ![cancelar la publicación](assets/unpublish.png).
   1. Realice una de las siguientes acciones y, a continuación, pulse Cancelar publicación:

      * Si está en la vista de tarjeta, pulse **[!UICONTROL Introducir selección]** ![aem6forms_check-círculo](assets/aem6forms_check-circle.png)y pulse el recurso. El recurso está seleccionado.

      * Si está en la vista de lista, pase el ratón sobre un recurso y pulse ![selectassetcheckmark](assets/selectassetcheckmark.png) . El recurso está seleccionado.

      * Pulse un recurso para mostrar sus detalles.
      * Mostrar las propiedades de un recurso tocando Ver propiedades ![viewproperties](assets/viewproperties.png).

1. Cuando se inicia el proceso de cancelación de la publicación, aparece un cuadro de diálogo de confirmación. Toque **[!UICONTROL Cancelar la publicación]**.

   >[!NOTE]
   >
   >Solo se cancela la publicación del recurso seleccionado, y sus recursos secundarios y referenciados, si los hay, no se cancelan.

## Revertir un recurso o una carta a la versión publicada anteriormente {#revert-an-asset-or-letter-to-the-previously-published-version}

Cada vez que publica un recurso o una carta después de editarlo, se crea una versión del recurso o la carta. Puede revertir un recurso o una carta a una versión publicada anteriormente. Puede que tenga que hacerlo si algo sale mal con la versión actual del recurso o documento.

>[!NOTE]
>
>No revierta una carta a un estado de última publicación si se elimina del sistema cualquier recurso dependiente utilizado en esa carta publicada.

1. Seleccione un recurso y pulse **[!UICONTROL Revertir a la versión publicada anteriormente]** ![reverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png).
1. Antes de revertir el recurso, aparece un cuadro de diálogo de confirmación. Toque **[!UICONTROL Revertir]**.

   El recurso o la carta se devuelven a su versión publicada anteriormente.

## Eliminación de un recurso {#delete-an-asset}

>[!NOTE]
>
>Al eliminar un recurso, éste se elimina de la instancia de publicación. Al eliminar un recurso, también se elimina su historial de versiones, excepto la versión base.

1. Seleccione un recurso y pulse **[!UICONTROL Eliminar]** ![delete](assets/delete.png).

   >[!NOTE]
   >
   >La opción Eliminar también está disponible cuando se muestran los detalles del recurso tocando un recurso o mostrando las propiedades de un recurso tocando Ver propiedades ![viewproperties](assets/viewproperties.png).

1. Antes de eliminar el recurso, aparece un cuadro de diálogo de confirmación. Toque **[!UICONTROL Eliminar]**.

   >[!NOTE]
   >
   >Solo se elimina el recurso seleccionado, y los recursos dependientes y no se eliminan. Para comprobar las referencias de un recurso, pulse ![referencias](assets/references.png) y, a continuación, seleccione un recurso.
   >
   >
   >Si el recurso que intenta eliminar es un recurso secundario de otro recurso, no se elimina. Para eliminar un recurso de este tipo, elimine las referencias de este recurso de otros recursos y vuelva a intentarlo.

## Forms adaptable protegido {#protected-adaptive-forms}

Puede habilitar la autenticación para los formularios a los que deben acceder los usuarios seleccionados. Cuando se habilita la autenticación en los formularios, los usuarios ven una pantalla de inicio de sesión antes de acceder a ellos. Solo los usuarios con credenciales autorizadas pueden acceder a los formularios.

Para habilitar la autenticación para los formularios:

1. En el explorador, abra configMgr en la instancia de publicación.\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. En la Configuración de la consola web de Adobe Experience Manager, haga clic en **Servicio de autenticación Apache Sling** para configurarlo.
1. En el cuadro de diálogo Servicio de autenticación Apache Sling que aparece, utilice la variable **+** para agregar rutas.\
   Cuando se agrega una ruta, el servicio de autenticación se activa para los formularios de esa ruta.
