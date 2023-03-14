---
title: Compatibilidad con miniaturas para vídeos en pantallas as a Cloud Service
description: En esta página se describe cómo añadir compatibilidad con miniaturas para vídeos en Pantallas as a Cloud Service.
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# Compatibilidad con miniaturas para vídeos {#thumbnail-support-videos}

## Introducción {#introduction}

Un autor de contenido puede definir una miniatura para los vídeos, de modo que la imagen pueda utilizarse como marcador de posición y probar correctamente la reproducción y la segmentación del contenido, mientras el equipo correspondiente finaliza el vídeo real. También se puede utilizar la imagen en caso de que falle la reproducción del vídeo.

Añadir la compatibilidad con una imagen en miniatura en el componente de vídeo permite al cliente añadir correctamente un componente válido en el canal, con contenido real, y realizar cualquier configuración de segmentación antes de que se envíe el vídeo.

>[!NOTE]
>La imagen en miniatura, si se configura en el componente de vídeo, se reproduce en caso de que falle la reproducción del vídeo en el reproductor. Esto le permite enviar el mensaje deseado a la audiencia (reproduciendo contenido) en lugar de omitirlo por completo.

La compatibilidad con miniaturas le permite:

* Prepare una experiencia de canal cuando los vídeos aún no estén listos o cuando no desee probar necesariamente una descarga de recursos grande en los reproductores

* Establezca un mecanismo de reserva en caso de que haya problemas de reproducción en el dispositivo.

## Uso de miniaturas en vídeos {#using-thumbnails}

>[!IMPORTANT]
>**Requisitos previos**
>Antes de aprender a utilizar miniaturas para vídeos, asegúrese de aprender a crear representaciones de vídeo para canales en un proyecto as a Cloud Service de Screens. Consulte [aquí](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md) para obtener más información.

Siga los pasos a continuación para utilizar las miniaturas en los vídeos:

1. Vaya a un canal de Screens existente o cree un canal nuevo.

   >[!NOTE]
   >Para obtener información sobre cómo crear un canal y añadir contenido a un canal, consulte [Creación y administración de un canal en Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en).

1. Seleccione el canal y haga clic en **Editar** en la barra de acciones para abrir el editor.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. Añada o edite un componente de vídeo existente, como se muestra en la figura siguiente.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. Seleccione el vídeo y haga clic en el icono *llave* para abrir las propiedades del vídeo.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. El **Vídeo** se abre el cuadro de diálogo, donde verá el **Miniatura** zona de colocación.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. Arrastre y suelte una imagen desde el selector de recursos hasta el **Miniatura** zona de colocación y haga clic en **Listo**.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. Haga clic en **Previsualizar**.

1. Si se establece un vídeo en el componente, se reproducirá el vídeo. Si no es así, y la miniatura está configurada, la miniatura se reproducirá. De lo contrario, el componente se considera no configurado y se omitirá.

## Casos de uso admitidos al usar la miniatura en vídeos {#understand-use-case}

La miniatura en vídeos admite los siguientes casos de uso:

* Se omitirá un componente de vídeo sin configurar nada.

* Un componente de vídeo solo con el conjunto de miniaturas reproducirá la miniatura.

* Un componente de vídeo con el vídeo (si el vídeo tiene la representación correcta) y el conjunto de miniaturas reproducirán el vídeo.

* Un componente de vídeo con el conjunto de vídeos reproducirá la miniatura, en caso de error de reproducción, o simplemente pasará al siguiente elemento en caso de que la miniatura no esté configurada.
