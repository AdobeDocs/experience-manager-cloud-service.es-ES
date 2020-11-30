---
title: Uso de conjuntos de reglas para transformar direcciones URL
description: Puede implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritos en un lenguaje de secuencias de comandos (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones.
translation-type: tm+mt
source-git-commit: 1713cddf713afc24103a841a7dbae923941f6322
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 5%

---


# Uso de conjuntos de reglas para transformar direcciones URL {#using-rulesets-to-transform-urls}

Puede implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritos en un lenguaje de secuencias de comandos (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones. Cada regla consta de al menos una condición y una acción. Una regla evalúa los datos XML según las condiciones y, si se cumple una condición, toma la acción adecuada. Algunos ejemplos de conjuntos de reglas son:

* Añadiendo un sufijo de tipo MIME. Muchos servicios y sitios web requieren sufijos de imagen, como agregar `.jpg` a una dirección URL.
* Creación de una ruta de carpeta a la dirección URL para fines de optimización de motores de búsqueda (SEO).

   Consulte [Compatibilidad de Adobe Scene7 Publishing System con SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Añadir metadatos a la dirección URL para fines de optimización de motores de búsqueda (SEO).

   Consulte [Compatibilidad de Adobe Scene7 Publishing System con SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Configuración de la disposición del contenido para activar una descarga.
* Simplifique las direcciones URL de plantilla del servicio de imágenes para su personalización. Por ejemplo, convierta `rgb{XX,YY,ZZ}` en RTF listo `\redXX\greenYY\blueZZ`

* Solicite que ciertos caracteres se codifiquen como `$`, `{`, y `}`, y que determinados caracteres se descodifiquen en ImageServer. Por ejemplo, Facebook no funciona bien con las direcciones URL que contienen caracteres especiales.

   Consulte [Eliminación de caracteres especiales de las direcciones URL](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

En el contexto de Dynamic Media, los sitios web que utilizan un sistema basado en XML para administrar la información de recursos pueden cargar archivos XML a Dynamic Media. Puede designar uno de estos archivos como archivo de conjunto de reglas de preprocesamiento para proporcionar recursos de Dynamic Media. Este archivo reestructura el formato de protocolo de URL estándar para satisfacer la lógica empresarial de los sistemas integrados con Dynamic Media. Especifique un archivo XML que sirva como ruta de archivo de definiciones de conjunto de reglas.

>[!CAUTION]
>
>Tenga precaución al utilizar conjuntos de reglas; pueden evitar que el contenido de Dynamic Media se muestre en el sitio web.

Hay disponibles conjuntos de reglas de ejemplo que pueden ayudarle a crear su propio conjunto de reglas.
Consulte Referencia [de conjunto](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html)de reglas.

Al igual que con la creación de todos los conjuntos de reglas, asegúrese de que el archivo XML sea válido antes de cargarlo mediante un programa de validador XML como xmlvalid.
Consulte también [Resolución de problemas de conjuntos](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)de reglas.

Además, asegúrese de probar primero el conjunto de reglas en un entorno de ensayo que no afecte al entorno de producción activo.
Los entornos de producción y los entornos de ensayo generalmente requieren inicios de sesión diferentes.

* **Página de inicio de sesión de entorno** de ensayo NA: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **Página de inicio de sesión del entorno** de ensayo de EMEA: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **Página de inicio de sesión del entorno** de ensayo de JAPAC: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/)

Consulte también [Uso de la imagen &#39;asset&#39; en lugar de &#39;is&#39; en un conjunto](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)de reglas.

**Para implementar conjuntos de reglas XML:**

1. Inicie sesión en su cuenta de Dynamic Media Classic:

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Adobe proporcionó las credenciales y el inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con el servicio de asistencia técnica.

1. Cargue el archivo del conjunto de reglas haciendo lo siguiente:

   * En la barra de navegación global, haga clic en **[!UICONTROL Cargar]**.
   * En la página **[!UICONTROL Cargar]** , cerca de la esquina superior izquierda, haga clic en **[!UICONTROL Examinar]**.
   * En el cuadro de diálogo **[!UICONTROL Abrir]** , busque el archivo del conjunto de reglas (XML).
   * Seleccione el archivo y haga clic en **[!UICONTROL Abrir]**.
   * On the right side of the **[!UICONTROL Upload]** page, select a destination folder for the rule set file.
   * Cerca de la parte inferior de la página, asegúrese de que está activada la opción **[!UICONTROL Publicar después de cargar]** .
   * En la esquina inferior derecha de la página, haga clic en **[!UICONTROL Enviar carga]**.
   * En la barra de navegación global, haga clic en **[!UICONTROL Trabajos]** para comprobar el estado del trabajo de carga. Cuando la columna **[!UICONTROL Estado]** de la página **[!UICONTROL Trabajo]** indique Carga finalizada, continúe con los pasos siguientes.

1. En la barra de navegación situada cerca de la parte superior de la página, haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Ajustes de publicación > Servidor]** de imágenes.
1. En la página **[!UICONTROL Publicación del servidor de imágenes]**, en el grupo **[!UICONTROL Administración de catálogos]**, busque **[!UICONTROL Ruta del archivo de definición de conjunto de reglas]** y haga clic en **[!UICONTROL Seleccionar]**.
1. En la página **[!UICONTROL Seleccionar archivo de definición de conjunto de reglas (XML)]**, busque el archivo de conjunto de reglas y, en la esquina inferior derecha de la página, haga clic en **[!UICONTROL Seleccionar]**.
1. In the lower-right corner of the Setup page, click **[!UICONTROL Close]**.
1. Ejecute un trabajo de publicación de Image Server.

   Las condiciones del conjunto de reglas se aplican en las solicitudes a los servidores de imágenes de Dynamic Media activos.

   Si realiza cambios en el archivo del conjunto de reglas, los cambios se aplican inmediatamente al volver a cargar y publicar el archivo del conjunto de reglas actualizado.

