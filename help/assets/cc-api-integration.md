---
title: Automatización de contenido para la integración de Creative Cloud
description: Generar variaciones de los recursos mediante la integración del Creative Cloud
contentOwner: AG
feature: Cargar,Procesamiento de recursos,Publicación,Microservicios de Asset compute,Flujo de trabajo
role: Business Practitioner,Administrator
source-git-commit: 05f2bfac12d37b8ef9940e3381c709891cabe236
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Generar variaciones de recursos mediante la integración [!DNL Adobe Creative Cloud] {#content-automation}

El complemento de automatización de contenido integra Experience Manager Assets como Cloud Service y las API de Adobe Creative Cloud para procesar creativamente sus recursos a escala. Experience Manager utiliza [asset microservices](/help/assets/asset-microservices-overview.md) basados en la nube para aprovechar las funciones de Adobe Creative Cloud y automatizar la creación de recursos y la gestión de medios.

Para editar recursos en [!DNL Adobe Photoshop] y [!DNL Adobe Lightroom], no es necesario descargar, editar ni cargar en [!DNL Experience Manager Assets]. Simplemente cree y configure un perfil de procesamiento, aplique el perfil a una carpeta y cargue los recursos en la carpeta . Los recursos cargados en la carpeta se procesan para crear distintas variaciones de ese recurso. El procesamiento masivo y la edición consistentes y sencilla de recursos ahorraron esfuerzos manuales y aumentan la velocidad de contenido. Además, los desarrolladores y socios pueden ampliar los microservicios de recursos con acceso directo a estas API e incluir lógica personalizada.

Los usuarios pueden crear perfiles de procesamiento para automatizar las siguientes operaciones creativas en sus recursos:

**Tono** automático: Utiliza la inteligencia artificial para analizar el contenido de la imagen y realiza de forma inteligente correcciones de luz y color basadas en los atributos únicos de la imagen.
**Auto-vertical**: Utiliza inteligencia artificial para analizar el contenido de la imagen y corregir la perspectiva sesgada en las imágenes. Por ejemplo, para crear horizontes de nivel.
**Ajustes preestablecidos** de Lightroom: Aplica un aspecto definido por el usuario a las imágenes para lograr un aspecto uniforme mediante ajustes preestablecidos personalizados.
**Recorte de imagen**: Utiliza la inteligencia artificial para crear la selección alrededor de los objetos salientes y eliminar el fondo con un solo comando.
**Máscara** de imagen: Utiliza inteligencia artificial para crear máscara alrededor de objetos salientes con un solo comando.
**Acciones** de Photoshop: Aplica una serie de tareas (en Photoshop) a un archivo o a un lote de archivos.
**Sustitución** de objetos inteligentes: Realiza una personalización a escala, permitiéndole intercambiar imágenes manteniendo al mismo tiempo todos los efectos y ajustes aplicados dentro de un archivo PSD.

## Uso de un perfil de procesamiento para procesar recursos {#process-assets}

Para utilizar perfiles de procesamiento para crear variaciones automáticamente, siga estos pasos:

1. Póngase en contacto con el servicio de atención al cliente de Adobe para adquirir la licencia.
1. Vaya a Herramientas > Recursos > Perfiles de procesamiento.
1. Seleccione Crear y especifique un Nombre.
1. Seleccione la pestaña Creative . Especifique la carpeta de salida, seleccione [!UICONTROL Agregar nuevo] para agregar configuraciones creativas. Proporcione Nombre de representación (o nombre de salida), Extensión (o tipo de archivo), seleccione Calidad (o parámetros de salida), seleccione Incluye y excluye listas de tipo MIME (o filtro de recursos de entrada) y seleccione la operación creativa necesaria.
1. Para algunas operaciones, se requiere un parámetro adicional (recurso). Proporcione valores para estos parámetros adicionales si se solicita.

1. Agregue más operaciones creativas como parte del mismo perfil de procesamiento o guarde el perfil.

1. Aplique el perfil de procesamiento a una carpeta. Seleccione Propiedades de la carpeta, Procesamiento de recursos y seleccione el perfil de procesamiento creado.

Una vez que el perfil de procesamiento se aplica a una carpeta DAM, todos los recursos cargados o actualizados en esta carpeta (o en subcarpetas, a menos que se sobrescriban) ejecutan las operaciones definidas además del procesamiento estándar.

Para procesar los recursos existentes manualmente, seleccione los recursos y la opción **[!UICONTROL Reprocesar]** y, a continuación, seleccione el perfil de procesamiento necesario.

## Sugerencias y limitaciones {#limitations-best-practices}

* [!DNL Experience Manager] limita el procesamiento de recursos a 300 solicitudes por minuto por entorno y a 700 solicitudes por minuto por organización.
* El tamaño del archivo está limitado a 4 GB para operaciones de API [!DNL Adobe Photoshop] y a 1 GB para operaciones [!DNL Adobe Lightroom].

>[!MORELIKETHIS]
>
>* [Configure y utilice microservicios de recursos mediante perfiles](/help/assets/asset-microservices-configure-and-use.md) de procesamiento.
>* [ [!DNL Experience Manager] Integración con [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).

