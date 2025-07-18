---
title: Importar formularios de metadatos de [!DNL Admin View] a [!DNL Assets View]
description: Este artículo describe cómo importar el formulario de metadatos de  [!DNL Admin View] a [!DNL Assets View]
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 5fb4fe97-486a-4a91-af60-a7182efcc2f9
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---

# Importar formularios de metadatos de [!DNL Admin View] a [!DNL Assets View] {#import-metadata-forms-from-admin-view-to-assets-view}

[!DNL Adobe Experience Manager Assets] le permite importar formularios de metadatos y sus asociaciones de carpetas de [!DNL Admin View] a [!DNL Assets View].

## Antes de empezar{#prerequisites-for-importing-metadata-forms-to-assets-view}

Asegúrese de tener derechos de administrador para importar los formularios de metadatos y sus asociaciones de carpetas de [!DNL Admin View] a [!DNL Assets View].

## Importar formularios de metadatos a [!DNL Assets View]{#import-metadata-forms-to-assets-view}

Como administrador, ejecute los siguientes pasos para importar los formularios de metadatos disponibles en [!DNL Admin View] a [!DNL Assets View]:

1. Vaya a la página de inicio de [!DNL Assets View] y haga clic en **[!UICONTROL Metadatos Forms]** en **[!UICONTROL Configuración]** para abrir la página de **[!UICONTROL Metadatos Forms]** que muestra la lista de formularios de metadatos disponibles en [!DNL Assets View].

   ![página de formularios de metadatos](/help/assets/assets/metadata-forms-page.png)

1. Seleccione **[!UICONTROL Importar]**, se mostrará un mensaje de procesamiento (por ejemplo, *Procesando 2 formularios de metadatos... Espere un momento.*) mientras la importación está en curso. Una vez completado el procesamiento, se muestra la tabla **[!UICONTROL Importar formularios de metadatos]**, que incluye una lista de los formularios de metadatos disponibles en [!DNL Admin View]. La fila de la tabla incluye el nombre del formulario de metadatos (bajo **[!UICONTROL Nombre]**), las carpetas asociadas a ese formulario (bajo **[!UICONTROL Asociación de carpetas]**) y una opción para obtener una vista previa de ![vista previa](/help/assets/assets/Preview.svg) del formulario antes de importarlo.

   ![Importar página de Forms de metadatos](/help/assets/assets/import-metadata-forms-page.png)

   >[!NOTE]
   > 
   > En **[!UICONTROL Importar Forms de metadatos]**, la tabla **[!UICONTROL Duplicar]** junto al nombre de un formulario muestra que el formulario ya se ha aplicado a una carpeta de [!DNL Assets View]. La importación de ese formulario duplicado anula el formulario existente aplicado a la carpeta. Para evitar esta anulación, cambie el nombre del formulario antes de importarlo. Haga clic en el nombre del formulario para cambiarle el nombre.

1. Haga clic en ![seleccionar carpeta](/help/assets/assets/x.svg) junto al nombre de una carpeta (en [!UICONTROL Asociación de carpetas]) para quitar la asociación de carpetas con el formulario.
1. Haga clic en ![seleccionar carpeta](/help/assets/assets/add-to-folder.svg) para seleccionar una carpeta y asignarle el formulario de metadatos correspondiente.
1. Haga clic en el círculo rojo para ver los detalles sobre los componentes de metadatos o las asignaciones no compatibles en el formulario que se excluyen de la importación.

   ![Importar página de Forms de metadatos](/help/assets/assets/unsupported-import-elements.png)

1. Seleccione uno o varios formularios de la tabla y haga clic en **[!UICONTROL Iniciar importación]** para importar los formularios de metadatos y sus carpetas asociadas en [!DNL Assets View]. Se muestra un mensaje de procesamiento (por ejemplo, *Importando 3 formularios de metadatos. Espere un momento.*). Una vez completada la importación, un mensaje confirma que los formularios se han importado correctamente y la página **[!UICONTROL Metadatos de Forms]** (de [!DNL Assets View]) muestra tanto los formularios importados recientemente como los existentes disponibles en [!DNL Assets View]. Puede hacer lo siguiente en esta página:

   * Haga clic en el encabezado de columna para ordenar la tabla por [!UICONTROL Nombre], [!UICONTROL Modificado] o [!UICONTROL Autor].
   * Seleccione el formulario importado y haga clic en **[!UICONTROL Quitar de las carpetas]**; a continuación, compruebe el nombre de la carpeta en la ruta de acceso de la carpeta para confirmar que se ha transferido correctamente.

     ![comprobar página de formularios de metadatos](/help/assets/assets/confirm-ported-folder.png)
   * Seleccione el formulario importado y haga clic en **[!UICONTROL Editar]** para ver todas las configuraciones admitidas del formulario de metadatos. Consulte [Configuración de Forms de metadatos](https://experienceleague.adobe.com/es/docs/experience-manager-assets-essentials/help/metadata#metadata-forms) para obtener más información sobre los formularios de metadatos, sus componentes y campos.

   ![comprobar página de formularios de metadatos](/help/assets/assets/verify-metadata-forms-page.png)

## Verificar los formularios de metadatos importados{#Verify-the-imported-metadata-forms}

Después de importar los formularios de metadatos de [!DNL Admin View] a [!DNL Assets View], siga estos pasos para comprobar la importación:

1. Vaya a cualquiera de las carpetas asociadas del formulario de metadatos importado.
1. Vaya a la página de detalles de un [recurso](/help/assets/navigate-assets-view.md#preview-assets) y compruebe que los componentes de metadatos, los campos de componente y los valores de campo admitidos estén sincronizados desde [!DNL Admin View]. Consulte el artículo [Metadatos en Assets Essentials](https://experienceleague.adobe.com/es/docs/experience-manager-assets-essentials/help/metadata) para obtener más información sobre los componentes de metadatos, los campos de componente y los valores de campo.

   >[!NOTE]
   >
   > En [[!DNL Assets View] página de detalles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/assets-view/metadata-assets-view#metadata-forms) o [[!DNL Admin View] página de propiedades](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/assets/administer/metadata-schemas), los cambios en los valores de las propiedades de metadatos se sincronizan automáticamente entre las dos interfaces. Sin embargo, los cambios estructurales del formulario, como agregar o quitar campos u otras modificaciones, no se sincronizan.
