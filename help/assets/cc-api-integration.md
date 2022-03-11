---
title: Automatización de contenido para la integración de Creative Cloud
description: Generar variaciones de los recursos mediante la integración del Creative Cloud
contentOwner: AG
feature: Upload,Asset Processing,Publishing,Asset Compute Microservices,Workflow
role: User,Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Generar variaciones de recursos utilizando [!DNL Adobe Creative Cloud] integración {#content-automation}

El complemento de automatización de contenido se integra [!DNL Adobe Experience Manager Assets] como [!DNL Cloud Service] y [!DNL Adobe Creative Cloud] API para procesar creativamente sus recursos a escala. [!DNL Experience Manager] utiliza basados en la nube [microservicios de recursos](/help/assets/asset-microservices-overview.md) para usar la variable [!DNL Adobe Creative Cloud] y automatice la creación de recursos y la gestión de medios.

Para editar recursos en [!DNL Adobe Photoshop] y [!DNL Adobe Lightroom], no tiene que descargar recursos de [!DNL Experience Manager Assets], edite y cárguelos de nuevo. Puede crear y configurar un perfil de procesamiento en [!DNL Experience Manager], aplique el perfil a una carpeta y cargue los recursos en la carpeta . Los recursos cargados se vuelven a procesar en función de los perfiles de procesamiento y se obtienen variaciones de estos recursos. El procesamiento masivo consistente y sin esfuerzo ahorra esfuerzos manuales y aumenta la velocidad de contenido, también sin necesidad de contar con excelentes habilidades creativas. Además, los desarrolladores y los socios pueden ampliar los microservicios de recursos con acceso directo a estas API e incluir lógica personalizada.

Los usuarios pueden crear perfiles de procesamiento para automatizar las siguientes operaciones creativas en sus recursos:

* **Tono automático**: Utiliza la inteligencia artificial para analizar el contenido de la imagen y realiza de forma inteligente correcciones de luz y color basadas en los atributos únicos de la imagen.

* **Auto-vertical**: Utiliza inteligencia artificial para analizar el contenido de la imagen y corregir la perspectiva sesgada en las imágenes. Por ejemplo, para crear horizontes de nivel.

   ![tono automático](/help/assets/assets/content-automation-autotone.png)

   *Figura: El tono automático y el enderezamiento automático pueden ayudar a mejorar las imágenes distorsionadas.*

* **Ajustes preestablecidos de Lightroom**: Aplica un aspecto definido por el usuario a las imágenes para lograr un aspecto uniforme mediante ajustes preestablecidos personalizados.

   ![Ajuste preestablecido de Lightroom](/help/assets/assets/content-automation-lrpresets.png)

   *Figura: Ajuste preestablecido de Adobe Lightroom para mejorar la calidad de la imagen de una manera uniforme para muchas imágenes.*

* **Recorte de imagen**: Utiliza inteligencia artificial para crear una selección alrededor de los objetos salientes y eliminar el fondo con un solo comando.

   ![Quitar fondo y cortar una imagen de una foto](/help/assets/assets/content-automation-backgroundremove.png)

* **Máscara de imagen**: Utiliza inteligencia artificial para crear máscaras alrededor de objetos salientes con un solo comando.

   ![Enmascarar una imagen mediante IA](/help/assets/assets/content-automation-mask.png)

* **Acciones de Photoshop**: Aplica una serie de [!DNL Adobe Photoshop] tareas a un archivo o a un lote de archivos.

   ![Acciones de Photoshop](/help/assets/assets/content-automation-psactions.png)

* **Sustitución de objeto inteligente**: Personaliza a escala permitiéndole intercambiar imágenes manteniendo al mismo tiempo todos los efectos y ajustes aplicados dentro de un archivo PSD.

   ![Reemplazar objetos de forma inteligente](/help/assets/assets/content-automation-objectreplace.png)

## Utilice un perfil de procesamiento para editar los recursos creativos de forma masiva {#process-assets}

Para utilizar perfiles de procesamiento para crear variaciones automáticamente, siga estos pasos:

1. Contacto [Asistencia al cliente de Adobe](https://experienceleague.adobe.com/#support) para recibir la licencia.

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Perfiles de procesamiento]**.

1. Select **[!UICONTROL Crear]** y especifique un **[!UICONTROL Nombre]**.

1. Seleccione el **[!UICONTROL Creative]** , especifique la carpeta de salida, seleccione **[!UICONTROL Agregar nuevo]** para agregar una configuración creativa.

1. Proporcionar **[!UICONTROL Nombre de representación]** (o nombre de salida), **[!UICONTROL Extensión]** (o tipo de archivo), seleccione **[!UICONTROL Calidad]** (o parámetros de salida), seleccione **[!UICONTROL Incluye]** y **[!UICONTROL Excluye]** listas de tipo MIME (o filtro de recursos de entrada) y seleccione la operación creativa necesaria.

   ![[!UICONTROL Creative] en [!UICONTROL Perfil de procesamiento]](assets/creative-processing-profile.png)

1. Algunas operaciones requieren parámetros adicionales (recurso). Proporcione valores para estos parámetros adicionales, si es necesario.

1. Agregue más operaciones creativas como parte del mismo perfil de procesamiento o guarde el perfil.

1. Aplique el perfil de procesamiento a una carpeta. En una carpeta **[!UICONTROL Propiedades]** página, seleccione **[!UICONTROL Procesamiento de recursos]** y seleccione el perfil de procesamiento que desee aplicar.

Después de aplicar el perfil de procesamiento a una carpeta DAM, todos los recursos cargados o actualizados en esta carpeta ejecutan las operaciones definidas además del procesamiento estándar. Las subcarpetas heredan los mismos perfiles que se aplican a las carpetas principales. Los usuarios pueden anular esta herencia.

Para procesar los recursos existentes, seleccione los recursos y seleccione **[!UICONTROL Volver a procesar]** y, a continuación, seleccione el perfil de procesamiento necesario.

## Sugerencias y limitaciones {#limitations-best-practices}

* [!DNL Experience Manager] limita el procesamiento de recursos a 300 solicitudes por minuto por entorno y a 700 solicitudes por minuto por organización.
* El tamaño del archivo está limitado a 4 GB para [!DNL Adobe Photoshop] Operaciones de API y 1 GB para [!DNL Adobe Lightroom] operaciones.

>[!MORELIKETHIS]
>
>* [Configuración y uso de microservicios de recursos mediante perfiles de procesamiento](/help/assets/asset-microservices-configure-and-use.md).
>* [ [!DNL Experience Manager] Integrar con [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [Ingesta y procesamiento de recursos con microservicios de recursos: Información general](/help/assets/asset-microservices-overview.md).

