---
title: Uso de conjuntos de reglas para transformar direcciones URL
description: Obtenga información sobre cómo implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritas en un lenguaje de script (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones.
contentOwner: Rick Brough
feature: Rulesets,Troubleshooting,Upload
role: User
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: ad2b36ffa178d787f50d33ce3393a76811467323
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 0%

---

# Uso de conjuntos de reglas para transformar direcciones URL {#using-rulesets-to-transform-urls}

Puede implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritas en un lenguaje de script (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones. Cada regla consta de al menos una condición y una acción. Una regla evalúa los datos XML con respecto a las condiciones y, si se cumple una condición, toma la acción adecuada. Algunos ejemplos de conjuntos de reglas son los siguientes:

* Agregar un sufijo de tipo MIME. Muchos servicios y sitios web requieren sufijos de imagen, como la adición de `.jpg` a una dirección URL.
* Creación de una ruta de carpeta a la URL con fines de optimización del motor de búsqueda.

  Consulte [Cómo admite Adobe Dynamic Media Classic el SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Añadir metadatos a la URL con fines de SEO (optimización del motor de búsqueda).

  Consulte [Cómo admite Adobe Dynamic Media Classic el SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Configuración de la disposición de contenido para almacenar en déclencheur una descarga.
* Simplifique las direcciones URL de plantilla del servicio de imágenes para la personalización. Por ejemplo, gire `rgb{XX,YY,ZZ}` en el archivo RTF-ready `\redXX\greenYY\blueZZ`

* Solicite la codificación de ciertos caracteres, como `$`, `{`, y `}`y ciertos caracteres que se van a descodificar en ImageServer. Por ejemplo, Facebook no funciona bien con direcciones URL que contienen caracteres especiales.

  Consulte [Eliminación de caracteres especiales de las direcciones URL](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

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

Consulte también [Uso de la imagen &quot;recurso&quot; en lugar de &quot;es&quot; en un conjunto de reglas](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

## Implementar conjuntos de reglas XML {#deploy-xml-rule-sets}

1. Abra el [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta.

   El Adobe proporcionó sus credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con Atención al cliente.

1. Cargue el archivo del conjunto de reglas haciendo lo siguiente:

   * En la barra de navegación global, seleccione **[!UICONTROL Cargar]**.
   * En el **[!UICONTROL Cargar]** página, cerca de la esquina superior izquierda, seleccione **[!UICONTROL Examinar]**.
   * En el **[!UICONTROL Abrir]** , busque el archivo del conjunto de reglas (XML).
   * Seleccione el archivo y luego seleccione **[!UICONTROL Abrir]**.
   * En el lado derecho del **[!UICONTROL Cargar]** , seleccione una carpeta de destino para el archivo del conjunto de reglas.
   * Cerca de la parte inferior de la página, asegúrese de que la opción Publicar después de cargar está activada.
   * En la esquina inferior derecha de la página, seleccione **[!UICONTROL Cargar envío]**.
   * En la barra de navegación global, seleccione **[!UICONTROL Trabajos]** para comprobar el estado del trabajo de carga. Si la variable **[!UICONTROL Estado]** en la columna **[!UICONTROL Trabajo]** La página indica Carga completada. Continúe con los pasos siguientes.

1. En la barra de navegación cerca de la parte superior de la página, vaya a **[!UICONTROL Configurar]** > **[!UICONTROL Ajustes de aplicación]** > **[!UICONTROL Ajustes de publicación]** > **[!UICONTROL Servidor de imágenes]**.
1. En el **[!UICONTROL Servidor de imágenes]** , debajo de la **[!UICONTROL Administración de catálogos]** grupo, localizar **[!UICONTROL Ruta del archivo de definición de conjunto de reglas]**, luego seleccione **[!UICONTROL Seleccionar]**.
1. En el **[!UICONTROL Seleccionar archivo de definición de conjunto de reglas (XML)]** , busque el archivo de conjunto de reglas y, en la esquina inferior derecha de la página, seleccione **[!UICONTROL Seleccionar]**.
1. En la esquina inferior derecha de la página Configuración, seleccione **[!UICONTROL Cerrar]**.
1. Ejecute un trabajo de publicación del servidor de imágenes.

   Las condiciones del conjunto de reglas se aplican a las solicitudes a los servidores de imágenes de Dynamic Media activos.

   Si cambia el archivo del conjunto de reglas, los cambios se aplican inmediatamente al volver a cargar y publicar el archivo del conjunto de reglas actualizado.
