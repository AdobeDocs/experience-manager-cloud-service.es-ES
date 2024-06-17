---
title: Automatización de contenidos para la integración de Creative Cloud
description: Generación de variaciones de recursos mediante la integración de Creative Cloud
contentOwner: AG
feature: Upload, Asset Processing, Publishing, Asset Compute Microservices
role: User, Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 5%

---

# Generar variaciones de recursos mediante [!DNL Adobe Creative Cloud] integración {#content-automation}

El complemento de automatización de contenido se integra [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] y [!DNL Adobe Creative Cloud] API para procesar sus recursos de forma creativa a escala. [!DNL Experience Manager] utiliza basado en la nube [microservicios de recursos](/help/assets/asset-microservices-overview.md) para usar el [!DNL Adobe Creative Cloud] y automatizar la creación de recursos y la gestión de medios.

Para editar recursos en [!DNL Adobe Photoshop] y [!DNL Adobe Lightroom], no es necesario que descargue recursos de [!DNL Experience Manager Assets], edítelos y vuelva a cargarlos. Puede crear y configurar un perfil de procesamiento en [!DNL Experience Manager], aplique el perfil a una carpeta y cargue los recursos en la carpeta. Los recursos cargados se vuelven a procesar según los perfiles de procesamiento y se obtienen variaciones de estos recursos. El procesamiento masivo, consistente y sin esfuerzo, ahorra esfuerzos manuales y aumenta la velocidad de contenido, sin necesidad de habilidades creativas excepcionales. Además, los desarrolladores y socios pueden ampliar los microservicios de recursos con acceso directo a estas API e incluir lógica personalizada.

Los usuarios pueden crear perfiles de procesamiento para automatizar las siguientes operaciones creativas en sus recursos:

* **Tono automático**: Utiliza inteligencia artificial para analizar el contenido de la imagen y realiza correcciones de luz y color de forma inteligente en función de los atributos únicos de la imagen.

* **Montar en vertical automáticamente**: utiliza inteligencia artificial para analizar el contenido de la imagen y corregir la perspectiva sesgada en las imágenes. Por ejemplo, para crear horizontes de nivel.

  ![tono automático](/help/assets/assets/content-automation-autotone.png)

  *Imagen: el tono automático y el enderezado automático pueden ayudar a mejorar las imágenes distorsionadas.*

* **Ajustes preestablecidos de Lightroom**: aplica un aspecto definido por el usuario a las imágenes para lograr un aspecto coherente mediante ajustes preestablecidos personalizados.

  ![Ajuste preestablecido de Lightroom](/help/assets/assets/content-automation-lrpresets.png)

  *Imagen: ajuste preestablecido de Adobe Lightroom para mejorar la calidad de la imagen de forma coherente en muchas imágenes.*

* **Recorte de imágenes**: utiliza inteligencia artificial para crear selección alrededor de objetos salientes y eliminar fondo con un solo comando.

  ![Quitar el fondo y cortar una imagen de una foto](/help/assets/assets/content-automation-backgroundremove.png)

* **Máscara de imagen**: utiliza inteligencia artificial para crear máscaras alrededor de objetos salientes con un solo comando.

  ![Enmascarar una imagen mediante IA](/help/assets/assets/content-automation-mask.png)

* **Acciones de Photoshop**: aplica una serie de [!DNL Adobe Photoshop] las tareas a un archivo o a un lote de archivos.

  ![Acciones de Photoshop](/help/assets/assets/content-automation-psactions.png)

* **Sustitución de objetos inteligentes**: realiza una personalización a escala permitiéndole intercambiar imágenes al tiempo que conserva todos los efectos y ajustes aplicados dentro de un archivo PSD.

  ![Reemplace los objetos inteligentemente](/help/assets/assets/content-automation-objectreplace.png)

## AEM Habilitar la automatización de contenido para programa as a Cloud Service {#enable-content-automation}

AEM Para habilitar el complemento de automatización de contenido para el programa as a Cloud Service de la mediante Cloud Manager:

1. Póngase en contacto con el representante de cuentas para obtener una licencia del complemento de automatización de contenido.
1. Acceda a Cloud Manager y cambie a su organización mediante el selector de organización.
1. Clic **[!UICONTROL Agregar programa]** y especifique un nombre de programa.
1. Haga clic en **[!UICONTROL Continuar]**.
1. Expandir **[!UICONTROL Assets]** y seleccione **[!UICONTROL Automatización de contenido]**.
1. Haga clic en **[!UICONTROL Crear]**.
1. Ejecute la canalización en [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

AEM Si necesita agregar el complemento de automatización de contenido a un programa as a Cloud Service de existente en Cloud Manager:

1. Haga clic en ... en la tarjeta de programa.

1. Seleccionar **[!UICONTROL Editar programa]** y luego seleccione **[!UICONTROL Soluciones y complementos]** pestaña.

1. Expandir **[!UICONTROL Assets]** y seleccione **[!UICONTROL Automatización de contenido]**.
1. Haga clic en **[!UICONTROL Actualizar]**.
1. Ejecute la canalización en [implementar los cambios en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## Utilice un perfil de procesamiento para editar sus recursos creativos de forma masiva {#process-assets}

Para utilizar perfiles de procesamiento para crear variaciones automáticamente, siga estos pasos:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de procesamiento]**.

1. Seleccionar **[!UICONTROL Crear]** y especifique un **[!UICONTROL Nombre]**.

1. Seleccione el **[!UICONTROL Creative]** pestaña, especifique la carpeta de salida, seleccione **[!UICONTROL Añadir nuevo]** para añadir una configuración creativa.

1. Proporcionar **[!UICONTROL Nombre de representación]** (o nombre de salida), **[!UICONTROL Extensión]** (o tipo de archivo), seleccione **[!UICONTROL Calidad]** (o parámetros de salida), seleccione **[!UICONTROL Incluye]** y **[!UICONTROL Excluye]** Listas de tipo MIME (o filtro de recursos de entrada) y seleccione la operación creativa necesaria.

   ![[!UICONTROL Creative] pestaña en [!UICONTROL Perfil de procesamiento]](assets/creative-processing-profile.png)

1. Algunas operaciones requieren parámetros adicionales (recurso). Proporcione valores para estos parámetros adicionales, si es necesario.

1. Añada más operaciones creativas como parte del mismo perfil de procesamiento o guarde el perfil.

1. Aplicar el perfil de procesamiento a una carpeta. En la carpeta de **[!UICONTROL Propiedades]** página, seleccione **[!UICONTROL Procesamiento de recursos]** y seleccione el perfil de procesamiento que desea aplicar.

Después de aplicar el perfil de procesamiento a una carpeta DAM, todos los recursos cargados o actualizados en esta carpeta ejecutan las operaciones definidas, además del procesamiento estándar. Las subcarpetas heredan los mismos perfiles que se aplican a las carpetas principales. Los usuarios pueden anular esta herencia.

Para procesar los recursos existentes, seleccione los recursos y seleccione **[!UICONTROL Reprocesar]** y, a continuación, seleccione el perfil de procesamiento necesario.

## Sugerencias y limitaciones {#limitations-best-practices}

* [!DNL Experience Manager] limita el procesamiento de recursos a 300 solicitudes por minuto por entorno y 700 solicitudes por minuto por organización.
* El tamaño de archivo está limitado a 4 GB para [!DNL Adobe Photoshop] Operaciones de API y 1 GB para [!DNL Adobe Lightroom] operaciones.

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
>* [Configuración y uso de microservicios de recursos a través de perfiles de procesamiento](/help/assets/asset-microservices-configure-and-use.md).
>* [Integrar [!DNL Experience Manager] con [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [Ingesta y procesamiento de recursos con microservicios de recursos: información general](/help/assets/asset-microservices-overview.md).
