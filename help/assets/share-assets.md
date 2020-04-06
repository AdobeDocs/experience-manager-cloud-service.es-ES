---
title: Compartir recursos, carpetas y colecciones como vínculo
description: En este artículo se describe cómo compartir recursos, carpetas y colecciones dentro de Experience Manager Assets como un hipervínculo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Uso compartido y distribución de recursos administrados en Experience Manager {#share-assets-from-aem}

Recursos Adobe Experience Manager (AEM) le permite compartir recursos, carpetas y colecciones con miembros de su organización y entidades externas, incluidos socios y proveedores. Puede utilizar los siguientes métodos para compartir recursos de Experience Manager Assets como un servicio de nube:

* Compartir como vínculo
* Descargar recursos
* Compartir mediante la aplicación de escritorio de AEM
* Compartir mediante Adobe Asset Link
* (Próxima funcionalidad) Compartir con Brand Portal

## Compartir recursos como un vínculo {#sharelink}

Para generar la URL de los recursos que desea compartir con los usuarios, utilice el cuadro de diálogo Uso compartido de vínculos. Los usuarios con privilegios de administrador o con permisos de lectura en la `/var/dam/share` ubicación pueden realizar la vista de los vínculos compartidos con ellos. El uso compartido de recursos a través de un vínculo es una forma práctica de poner los recursos a disposición de terceros externos sin que estos tengan que iniciar sesión en Recursos AEM en primer lugar.

>[!NOTE]
>
>* Necesita el permiso Editar ACL en la carpeta o el recurso que desea compartir como vínculo.
>* Antes de compartir un vínculo con los usuarios, asegúrese de que el servicio de correo de CQ de día está configurado. De lo contrario, se producirá un error.


1. En la interfaz de usuario de Recursos, seleccione el recurso que desea compartir como vínculo.
1. En la barra de herramientas, toque o haga clic en el vínculo **[!UICONTROL Compartir]**.

   Se crea automáticamente un vínculo de recurso en el campo **[!UICONTROL Compartir vínculo]** . Copie este vínculo y compártalo con los usuarios. El tiempo de caducidad predeterminado para el vínculo es un día.

   Como alternativa, realice los pasos 3 a 7 de este procedimiento para agregar destinatarios de correo electrónico, configurar la caducidad del vínculo y enviarlo desde el cuadro de diálogo.

   >[!NOTE]
   >
   >Si un recurso compartido se mueve a una ubicación diferente, su vínculo deja de funcionar. Vuelva a crear el vínculo y a compartirlo con los usuarios.

1. Desde la consola web, abra la configuración **[!UICONTROL Day CQ Link Externalizer]** y modifique las siguientes propiedades en el campo **[!UICONTROL Dominios]** con los valores mencionados en relación con cada uno de ellos:

   * local
   * author
   * instancias de publicación
   Para las propiedades local y de autor, proporcione la URL para la instancia local y de autor respectivamente. Tanto las propiedades locales como las de autor tienen el mismo valor si se ejecuta una única instancia de autor de AEM. Para la publicación, especifique la URL de la instancia de publicación.

1. En el apartado de la dirección de correo electrónico del cuadro de diálogo **[!UICONTROL Uso compartido de vínculos]**, escriba el ID de correo electrónico del usuario con el que desea compartir el vínculo. También puede compartir el vínculo con varios usuarios.

   Si el usuario es miembro de su organización, seleccione el ID de correo electrónico del usuario en los ID de correo electrónico sugeridos que aparecen en la lista debajo del área de escritura. Para un usuario externo, escriba el ID de correo electrónico completo y selecciónelo en la lista.

   Para habilitar el envío de mensajes de correo electrónico a los usuarios, configure los detalles del servidor SMTP en [Día del servicio](/help/assets/configure-asset-sharing.md#configmailservice)de correo de CQ.

   >[!NOTE]
   >
   >Si introduce un ID de correo electrónico de un usuario que no es miembro de su organización, las palabras &quot;Usuario externo&quot; llevan el prefijo &quot;ID de correo electrónico del usuario.

1. En el **[!UICONTROL cuadro Asunto]** , introduzca un asunto para el recurso que desea compartir.
1. En el cuadro **[!UICONTROL Mensaje]** , escriba un mensaje opcional.
1. En el campo **[!UICONTROL Caducidad]** , especifique una fecha y hora de caducidad para el vínculo mediante el selector de fechas. De forma predeterminada, la fecha de caducidad se establece para una semana a partir de la fecha en que comparta el vínculo.
1. Para permitir que los usuarios descarguen la imagen original junto con las representaciones, seleccione **[!UICONTROL Permitir la descarga del archivo]** original.

   >[!NOTE]
   >
   >De forma predeterminada, los usuarios solo pueden descargar las representaciones del recurso que se comparten como vínculo.

1. Haga clic en **[!UICONTROL Compartir]**. Un mensaje confirma que el vínculo se comparte con los usuarios a través de un correo electrónico.
1. Para vista del recurso compartido, toque o haga clic en el vínculo del correo electrónico que se envía al usuario. El recurso compartido se muestra en la página de **[!UICONTROL Adobe Marketing Cloud]** .

   Para cambiar a la vista de lista, toque o haga clic en el icono de diseño de la barra de herramientas.

1. Para generar una vista previa del recurso, pulse o haga clic en el recurso compartido. Para cerrar la vista previa y volver a la página de **[!UICONTROL Experience Cloud]**, pulse o haga clic en **[!UICONTROL Atrás]** en la barra de herramientas. Si ha compartido una carpeta, pulse o haga clic en **[!UICONTROL Carpeta principal]** para regresar a la carpeta principal.

   >[!NOTE]
   >
   >AEM admite la generación de previsualizaciones de recursos de estos tipos MIME: JPG, PNG, GIF, BMP, INDD, PDF y PPT. Solo puede descargar los recursos de los otros tipos MIME.

1. Para descargar el recurso compartido, toque o haga clic en **[!UICONTROL Seleccionar]** en la barra de herramientas, toque o haga clic en el recurso y, a continuación, toque o haga clic en **[!UICONTROL Descargar]** desde la barra de herramientas.
1. Para vista de los recursos compartidos como vínculos, vaya a la interfaz de usuario de Recursos y toque o haga clic en el icono de GlobalNav. Elija **[!UICONTROL Navegación]** en la lista para mostrar el panel Navegación.
1. En el panel Navegación, seleccione **[!UICONTROL Vínculos compartidos]** para mostrar una lista de recursos compartidos.
1. Para dejar de compartir un recurso, selecciónelo y toque o haga clic en **[!UICONTROL Dejar de compartir]** en la barra de herramientas.

Un mensaje confirma que se ha dejado de compartir el recurso. Además, la entrada del recurso se elimina de la lista.

## Descargar y compartir recursos {#download-and-share-assets}

Los usuarios pueden descargar algunos recursos y compartirlos fuera de Experience Manager. Para obtener más información, consulte [cómo buscar recursos](/help/assets/search-assets.md), [cómo descargar recursos](/help/assets/download-assets-from-aem.md)y [cómo descargar colecciones](manage-collections.md#download-a-collection)

## Uso compartido de recursos con profesionales creativos {#share-with-creatives}

Los especialistas en marketing y los usuarios de la línea de negocios pueden compartir fácilmente los recursos aprobados con sus profesionales creativos mediante:

* **Aplicación** de escritorio de AEM: La aplicación funciona en Windows y Mac. Consulte Descripción general [de la aplicación de](https://docs.adobe.com/content/help/es-ES/experience-manager-desktop-app/using/introduction.translate.html)escritorio. Para saber cómo cualquier usuario de escritorio autorizado puede acceder fácilmente a los recursos compartidos, consulte [Examinar, buscar y previsualización de recursos](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Los usuarios de escritorio pueden crear nuevos recursos y compartirlos con sus homólogos que sean usuarios de AEM, por ejemplo, cargando nuevas imágenes. Consulte [Carga de recursos mediante la aplicación](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)de escritorio.

* **Adobe Asset Link**: Los profesionales creativos pueden buscar y utilizar recursos directamente desde Adobe InDesign, Adobe Illustrator y Adobe Photoshop.

### Best practices and troubleshooting {#bestpractices}

* Es posible que las carpetas de recursos o las colecciones que contengan un espacio en blanco en su nombre no se compartan.
* Si los usuarios no pueden descargar los recursos compartidos, compruebe con el administrador de AEM cuáles son los límites [de](/help/assets/configure-asset-sharing.md#maxdatasize) descarga.
* Si no puede enviar correos electrónicos con vínculos a recursos compartidos o si los demás usuarios no pueden recibir su correo electrónico, consulte con el administrador de AEM si el servicio [de](/help/assets/configure-asset-sharing.md#configmailservice) correo electrónico está configurado o no.
* Si no puede compartir recursos con la funcionalidad de uso compartido de vínculos, asegúrese de que dispone de los permisos adecuados. Consulte [Uso compartido de recursos](#sharelink).

<!--
Add content or link about how to share using BP, DA, AAL, etc.
-->
