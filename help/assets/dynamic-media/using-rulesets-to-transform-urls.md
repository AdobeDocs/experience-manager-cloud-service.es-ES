---
title: Usar conjuntos de reglas para transformar direcciones URL
description: Aprenda a implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritos en un lenguaje de secuencias de comandos (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones.
role: User
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---

# Usar conjuntos de reglas para transformar direcciones URL {#using-rulesets-to-transform-urls}

Puede implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritos en un lenguaje de secuencias de comandos (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones. Cada regla consta de al menos una condición y una acción. Una regla evalúa los datos XML comparándolos con las condiciones y, si se cumple una condición, toma la acción adecuada. Algunos ejemplos de conjuntos de reglas son los siguientes:

* Añadir un sufijo de tipo MIME. Muchos servicios y sitios web requieren sufijos de imagen, como agregar `.jpg` a una dirección URL.
* Creación de una ruta de carpeta a la dirección URL con fines de SEO (Optimización del motor de búsqueda).

   Consulte [Compatibilidad de Adobe Dynamic Media Classic con SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Añadir metadatos a la dirección URL con fines de SEO (Optimización del motor de búsqueda).

   Consulte [Compatibilidad de Adobe Dynamic Media Classic con SEO](/help/assets/dynamic-media/assets/s7_seo.pdf).

* Configuración de la disposición de contenido para almacenar en déclencheur una descarga.
* Simplifique las URL de plantilla de Image Serving para la personalización. Por ejemplo, girar `rgb{XX,YY,ZZ}` en la lista RTF `\redXX\greenYY\blueZZ`

* Solicite ciertos caracteres para codificarlos, como `$`, `{`y `}`, y ciertos caracteres que se van a decodificar en ImageServer. Por ejemplo, Facebook no funciona bien con las direcciones URL que contienen caracteres especiales.

   Consulte [Eliminación de caracteres especiales de las direcciones URL](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

En el contexto de Dynamic Media, los sitios web que utilizan un sistema basado en XML para administrar la información de recursos pueden cargar archivos XML a Dynamic Media. Puede designar uno de estos archivos como archivo del conjunto de reglas de procesamiento previo para servir recursos de Dynamic Media. Este archivo reestructura el formato de protocolo de URL estándar para satisfacer la lógica de la empresa de los sistemas integrados con Dynamic Media. Se especifica un archivo XML para que sirva como ruta de archivo de definiciones de conjuntos de reglas.

>[!CAUTION]
>
>Tenga cuidado al utilizar conjuntos de reglas; pueden evitar que el contenido de Dynamic Media se muestre en el sitio web.

Hay disponibles conjuntos de reglas de ejemplo que pueden ayudarle a crear su propio conjunto de reglas.
Consulte [Referencia del conjunto de reglas](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Al igual que con la creación de todos los conjuntos de reglas, asegúrese de que el archivo XML sea válido antes de cargarlo mediante un programa de validador XML como xmlvalid.
Consulte también [Resolución de problemas de conjuntos de reglas](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

Además, asegúrese de probar primero el conjunto de reglas en un entorno de ensayo que no afecte al entorno de producción activo.
Los entornos de producción y los entornos de ensayo generalmente requieren diferentes inicios de sesión.

Consulte la [Aplicación de escritorio de Adobe Dynamic Media Classic para obtener información de inicio de sesión](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Consulte también [Uso de la imagen &quot;asset&quot; en lugar de la imagen &quot;is&quot; en un conjunto de reglas](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

## Implementar conjuntos de reglas XML {#deploy-xml-rule-sets}

1. Abra el [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta.

   Adobe proporcionó las credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con el Servicio de atención al cliente.

1. Cargue el archivo del conjunto de reglas haciendo lo siguiente:

   * En la barra de navegación global, seleccione **[!UICONTROL Cargar]**.
   * En el **[!UICONTROL Cargar]** página, cerca de la esquina superior izquierda, seleccione **[!UICONTROL Examinar]**.
   * En el **[!UICONTROL Apertura]** , busque el archivo del conjunto de reglas (XML).
   * Seleccione el archivo y, a continuación, seleccione **[!UICONTROL Apertura]**.
   * En el lado derecho del **[!UICONTROL Cargar]** seleccione una carpeta de destino para el archivo del conjunto de reglas.
   * Cerca de la parte inferior de la página, asegúrese de que Publicar después de la carga está marcada.
   * En la esquina inferior derecha de la página, seleccione **[!UICONTROL Enviar carga]**.
   * En la barra de navegación global, seleccione **[!UICONTROL Trabajos]** para comprobar el estado del trabajo de carga. Cuando la variable **[!UICONTROL Estado]** en la columna **[!UICONTROL Trabajo]** La página indica Cargar finalizado y continúe con los pasos siguientes.

1. En la barra de navegación cerca de la parte superior de la página, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración de publicación]** > **[!UICONTROL Servidor de imágenes]**.
1. En el **[!UICONTROL Publicación en el servidor de imágenes]** en el **[!UICONTROL Administración de catálogos]** grupo, localizar **[!UICONTROL Ruta del archivo de definición de conjunto de reglas]** y, a continuación, seleccione **[!UICONTROL Select]**.
1. En el **[!UICONTROL Seleccionar archivo de definición de conjunto de reglas (XML)]** , busque el archivo del conjunto de reglas y, a continuación, en la esquina inferior derecha de la página, seleccione **[!UICONTROL Select]**.
1. En la esquina inferior derecha de la página Configuración, seleccione **[!UICONTROL Cerrar]**.
1. Ejecute un trabajo de publicación de Image Server.

   Las condiciones del conjunto de reglas se aplican en las solicitudes a los servidores de imágenes de Dynamic Media activos.

   Si cambia el archivo del conjunto de reglas, los cambios se aplican inmediatamente cuando vuelve a cargar y publicar el archivo del conjunto de reglas actualizado.
