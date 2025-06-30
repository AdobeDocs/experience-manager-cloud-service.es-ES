---
title: Automatización de contenido para la integración con Creative Cloud
description: Generación de variaciones de recursos mediante la integración de Creative Cloud
contentOwner: AG
feature: Upload, Asset Processing, Publishing, Asset Compute Microservices
role: User, Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 5%

---

# Generar variaciones de recursos mediante la integración de [!DNL Adobe Creative Cloud] {#content-automation}

El complemento de automatización de contenido se integra con [!DNL Adobe Experience Manager Assets] como una API de [!DNL Cloud Service] y [!DNL Adobe Creative Cloud] para procesar de forma creativa los recursos a escala. [!DNL Experience Manager] usa [microservicios de recursos](/help/assets/asset-microservices-overview.md) basados en la nube para usar las características de [!DNL Adobe Creative Cloud] y automatizar la creación de recursos y la administración de medios.

Para editar recursos en [!DNL Adobe Photoshop] y [!DNL Adobe Lightroom], no es necesario que descargue recursos de [!DNL Experience Manager Assets], ni que los edite y vuelva a cargarlos. Puede crear y configurar un perfil de procesamiento en [!DNL Experience Manager], aplicar el perfil a una carpeta y cargar los recursos en la carpeta. Los recursos cargados se vuelven a procesar según los perfiles de procesamiento y se obtienen variaciones de estos recursos. El procesamiento masivo, consistente y sin esfuerzo, ahorra esfuerzos manuales y aumenta la velocidad de contenido, sin necesidad de habilidades creativas excepcionales. Además, los desarrolladores y socios pueden ampliar los microservicios de recursos con acceso directo a estas API e incluir lógica personalizada.

Los usuarios pueden crear perfiles de procesamiento para automatizar las siguientes operaciones creativas en sus recursos:

* **Tono automático**: utiliza inteligencia artificial para analizar el contenido de la imagen y realiza de forma inteligente correcciones de color y luz basándose en los atributos únicos de la imagen.

* **Auto-vertical**: Utiliza inteligencia artificial para analizar el contenido de la imagen y corregir la perspectiva sesgada en las imágenes. Por ejemplo, para crear horizontes de nivel.

  ![tono automático](/help/assets/assets/content-automation-autotone.png)

  *Imagen: el tono automático y el enderezado automático pueden ayudar a mejorar las imágenes distorsionadas.*

* **Ajustes preestablecidos de Lightroom**: aplica un aspecto definido por el usuario a las imágenes para lograr un aspecto coherente mediante ajustes preestablecidos personalizados.

  ![Ajuste preestablecido de Lightroom](/help/assets/assets/content-automation-lrpresets.png)

  *Imagen: ajuste preestablecido de Adobe Lightroom para mejorar la calidad de la imagen de forma uniforme en muchas imágenes.*

* **Recorte de imágenes**: utiliza inteligencia artificial para crear la selección alrededor de objetos salientes y quitar el fondo con un solo comando.

  ![Quitar el fondo y cortar una imagen de una fotografía](/help/assets/assets/content-automation-backgroundremove.png)

* **Máscara de imagen**: Utiliza inteligencia artificial para crear máscaras alrededor de objetos destacados con un solo comando.

  ![Enmascarar una imagen con IA](/help/assets/assets/content-automation-mask.png)

* **Acciones de Photoshop**: Aplica una serie de [!DNL Adobe Photoshop] tareas a un archivo o a un lote de archivos.

  ![Acciones de Photoshop](/help/assets/assets/content-automation-psactions.png)

* **Sustitución de objetos inteligentes**: realiza personalización a escala permitiéndole intercambiar imágenes mientras mantiene todos los efectos y ajustes aplicados dentro de un archivo PSD.

  ![Reemplazar objetos de forma inteligente](/help/assets/assets/content-automation-objectreplace.png)

## Habilitar la automatización de contenido para el programa AEM as a Cloud Service {#enable-content-automation}

Para habilitar el complemento de automatización de contenido para el programa de AEM as a Cloud Service mediante Cloud Manager:

1. Póngase en contacto con el representante de cuentas para obtener una licencia del complemento de automatización de contenido.
1. Acceda a Cloud Manager y cambie a su organización mediante el selector de organización.
1. Haga clic en **[!UICONTROL Agregar programa]** y especifique un nombre de programa.
1. Haga clic en **[!UICONTROL Continuar]**.
1. Expanda **[!UICONTROL Assets]** y seleccione **[!UICONTROL Automatización de contenido]**.
1. Haga clic en **[!UICONTROL Crear]**.
1. Ejecute la canalización para [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=es).

Si necesita agregar el complemento de automatización de contenido a un programa de AEM as a Cloud Service existente en Cloud Manager:

1. Haga clic en ... en la tarjeta de programa.

1. Seleccione **[!UICONTROL Editar programa]** y, a continuación, seleccione la ficha **[!UICONTROL Soluciones y complementos]**.

1. Expanda **[!UICONTROL Assets]** y seleccione **[!UICONTROL Automatización de contenido]**.
1. Haga clic en **[!UICONTROL Actualizar]**.
1. Ejecute la canalización para [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=es).

## Utilice un perfil de procesamiento para editar sus recursos creativos de forma masiva {#process-assets}

Para utilizar perfiles de procesamiento para crear variaciones automáticamente, siga estos pasos:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de procesamiento]**.

1. Seleccione **[!UICONTROL Crear]** y especifique un **[!UICONTROL Nombre]**.

1. Seleccione la ficha **[!UICONTROL Creative]**, especifique la carpeta de salida, seleccione **[!UICONTROL Agregar nuevo]** para agregar una configuración creativa.

1. Proporcione **[!UICONTROL Nombre de representación]** (o nombre de salida), **[!UICONTROL Extensión]** (o tipo de archivo), seleccione **[!UICONTROL Calidad]** (o parámetros de salida), seleccione **[!UICONTROL Incluye]** y **[!UICONTROL Excluye]** listas de tipo MIME (o filtro de recursos de entrada) y seleccione la operación creativa necesaria.

   Pestaña ![[!UICONTROL Creative] en [!UICONTROL Perfil de procesamiento]](assets/creative-processing-profile.png)

1. Algunas operaciones requieren parámetros adicionales (recurso). Proporcione valores para estos parámetros adicionales, si es necesario.

1. Añada más operaciones creativas como parte del mismo perfil de procesamiento o guarde el perfil.

1. Aplicar el perfil de procesamiento a una carpeta. En la página **[!UICONTROL Propiedades]** de una carpeta, seleccione **[!UICONTROL Procesamiento de recursos]** y el perfil de procesamiento que desee aplicar.

Después de aplicar el perfil de procesamiento a una carpeta DAM, todos los recursos cargados o actualizados en esta carpeta ejecutan las operaciones definidas, además del procesamiento estándar. Las subcarpetas heredan los mismos perfiles que se aplican a las carpetas principales. Los usuarios pueden anular esta herencia.

Para procesar los recursos existentes, selecciónelos, seleccione la opción **[!UICONTROL Volver a procesar]** y, a continuación, seleccione el perfil de procesamiento necesario.

## Sugerencias y limitaciones {#limitations-best-practices}

* [!DNL Experience Manager] limita el procesamiento de recursos a 300 solicitudes por minuto por entorno y a 700 solicitudes por minuto por organización.
* El tamaño de archivo está limitado a 4 GB para [!DNL Adobe Photoshop] operaciones de API y a 1 GB para [!DNL Adobe Lightroom] operaciones.
* Las representaciones de PDF de documentos de Microsoft Office (&quot;.docx&quot;, &quot;.doc&quot;, &quot;.ppt&quot;, &quot;.pptx&quot;, &quot;.xls&quot;, &quot;.xlsx&quot;) están limitadas a archivos de 100 MB o menos.
* La transcodificación de vídeo está limitada a archivos de entrada de 15 GB o menos.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Configurar y usar microservicios de recursos a través de perfiles de procesamiento](/help/assets/asset-microservices-configure-and-use.md).
>* [Integrar [!DNL Experience Manager] con [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [Ingesta y procesamiento de recursos con microservicios de recursos: información general](/help/assets/asset-microservices-overview.md).
