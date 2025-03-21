---
title: Uso de conjuntos de reglas para transformar direcciones URL
description: Obtenga información sobre cómo implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritas en un lenguaje de script (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones.
contentOwner: Rick Brough
feature: Rulesets,Troubleshooting,Upload,Best Practices
role: User
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 2%

---

# Uso de conjuntos de reglas para transformar direcciones URL {#using-rulesets-to-transform-urls}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

Puede implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritas en un lenguaje de script (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones. Cada regla consta de al menos una condición y una acción. Una regla evalúa los datos XML con respecto a las condiciones y, si se cumple una condición, toma la acción adecuada. Algunos ejemplos de conjuntos de reglas son los siguientes:

* Agregar un sufijo de tipo MIME. Muchos servicios y sitios web requieren sufijos de imagen, como agregar `.jpg` a una dirección URL.
* Creación de una ruta de carpeta a la URL con fines de optimización del motor de búsqueda.

  Ver [Cómo Adobe Dynamic Media Classic admite SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Añadir metadatos a la URL con fines de SEO (optimización del motor de búsqueda).

  Ver [Cómo Adobe Dynamic Media Classic admite SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Configuración de la disposición de contenido para almacenar en déclencheur una descarga.
* Simplifique las direcciones URL de plantilla del servicio de imágenes para la personalización. Por ejemplo, convierta `rgb{XX,YY,ZZ}` en el `\redXX\greenYY\blueZZ` listo para RTF

* Solicite la codificación de ciertos caracteres, como `$`, `{` y `}`, y de ciertos caracteres, para su descodificación hacia ImageServer. Por ejemplo, Facebook no funciona bien con direcciones URL que contienen caracteres especiales.

  Consulte [Quitar caracteres especiales de las direcciones URL](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

En el contexto de Dynamic Media, los sitios web que utilizan un sistema basado en XML para administrar la información de los recursos pueden cargar archivos XML en Dynamic Media. Puede designar uno de estos archivos como el archivo del conjunto de reglas de preprocesamiento para el servicio de recursos de Dynamic Media. Este archivo reestructura el formato de protocolo de URL estándar para satisfacer la lógica empresarial de los sistemas que se integran con Dynamic Media. Especifique un archivo XML que sirva como ruta de acceso del archivo de definiciones del conjunto de reglas.

>[!CAUTION]
>
>Tenga cuidado al utilizar conjuntos de reglas; pueden evitar que el contenido de Dynamic Media se muestre en el sitio web.

Hay disponibles conjuntos de reglas de ejemplo que pueden ayudarle a crear su propio conjunto de reglas.
Consulte [Referencia del conjunto de reglas](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Al igual que con toda la creación de conjuntos de reglas, asegúrese de que el archivo XML es válido antes de cargarlo mediante un programa de validación XML como xmlvalid.
Consulte también [Solucionar problemas de conjuntos de reglas](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Además, asegúrese de probar primero el conjunto de reglas en un entorno de ensayo que no afecte al entorno de producción en directo.
Los entornos de producción y los entornos de ensayo suelen requerir distintos inicios de sesión.

Consulte la [aplicación de escritorio de Adobe Dynamic Media Classic para obtener información de inicio de sesión](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Vea también [Uso de la imagen &#39;asset&#39; en lugar de &#39;is&#39; en un conjunto de reglas](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

## Implementar conjuntos de reglas XML {#deploy-xml-rule-sets}

1. Abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en su cuenta.

   Adobe proporcionó sus credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con Atención al cliente.

1. Cargue el archivo del conjunto de reglas haciendo lo siguiente:

   * En la barra de navegación global, seleccione **[!UICONTROL Cargar]**.
   * En la página **[!UICONTROL Cargar]**, cerca de la esquina superior izquierda, seleccione **[!UICONTROL Examinar]**.
   * En el cuadro de diálogo **[!UICONTROL Abrir]**, busque el archivo de conjunto de reglas (XML).
   * Seleccione el archivo y luego seleccione **[!UICONTROL Abrir]**.
   * En el lado derecho de la página **[!UICONTROL Cargar]**, seleccione una carpeta de destino para el archivo del conjunto de reglas.
   * Cerca de la parte inferior de la página, asegúrese de que la opción Publicar después de cargar está activada.
   * En la esquina inferior derecha de la página, seleccione **[!UICONTROL Cargar envío]**.
   * En la barra de navegación global, seleccione **[!UICONTROL Jobs]** para comprobar el estado del trabajo de carga. Cuando la columna **[!UICONTROL Estado]** de la página **[!UICONTROL Trabajo]** indique Carga finalizada, continúe con los siguientes pasos.

1. En la barra de navegación cerca de la parte superior de la página, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de aplicación]** > **[!UICONTROL Configuración de publicación]** > **[!UICONTROL Servidor de imágenes]**.
1. En la página **[!UICONTROL Servidor de imágenes: publicar]**, en el grupo **[!UICONTROL Administración de catálogos]**, busque **[!UICONTROL Ruta del archivo de definición de conjunto de reglas]** y, a continuación, seleccione **[!UICONTROL Seleccionar]**.
1. En la página **[!UICONTROL Seleccionar archivo de definición de conjunto de reglas (XML)]**, busque el archivo de conjunto de reglas y, en la esquina inferior derecha de la página, seleccione **[!UICONTROL Seleccionar]**.
1. En la esquina inferior derecha de la página Configuración, seleccione **[!UICONTROL Cerrar]**.
1. Ejecute un trabajo de publicación del servidor de imágenes.

   Las condiciones del conjunto de reglas se aplican a las solicitudes enviadas a los servidores de imágenes de Dynamic Media activos.

   Si cambia el archivo del conjunto de reglas, los cambios se aplican inmediatamente al volver a cargar y publicar el archivo del conjunto de reglas actualizado.
