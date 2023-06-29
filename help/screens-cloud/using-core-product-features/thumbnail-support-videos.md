---
title: Compatibilidad con miniaturas para vídeos en pantallas as a Cloud Service
description: En esta página se describe cómo añadir compatibilidad con miniaturas para vídeos en Pantallas as a Cloud Service.
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# Compatibilidad con miniaturas para vídeos {#thumbnail-support-videos}

## Introducción {#introduction}

Un autor de contenido puede definir una miniatura para los vídeos, de modo que la imagen se utilice como marcador de posición y pruebe correctamente la reproducción y la segmentación del contenido, mientras el equipo correspondiente finaliza el vídeo real. También se puede utilizar la imagen en caso de que falle la reproducción del vídeo.

Añadir la compatibilidad con una imagen en miniatura en el componente de vídeo permite al cliente añadir correctamente un componente válido en el canal, con contenido real, y realizar cualquier configuración de segmentación antes de que se envíe el vídeo.

>[!NOTE]
>La imagen en miniatura, si se establece en el componente de vídeo, se reproduce si hay un error de reproducción de vídeo en el reproductor. Este flujo de trabajo permite enviar el mensaje deseado a la audiencia (reproduciendo contenido) en lugar de omitirlo por completo.

La compatibilidad con miniaturas permite hacer lo siguiente:

* Prepare una experiencia de canal cuando los vídeos aún no estén listos o cuando no desee probar necesariamente una descarga de recursos grande en los reproductores

* Establezca un mecanismo de reserva en caso de que haya problemas de reproducción en el dispositivo.

## Uso de miniaturas en vídeos {#using-thumbnails}

>[!IMPORTANT]
>**Requisitos previos**
>Antes de aprender a utilizar miniaturas para vídeos, asegúrese de aprender a crear representaciones de vídeo para canales en proyectos as a Cloud Service de Screens. Consulte [Creación de representaciones de vídeo en Screens as a Cloud Service](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md).

Siga los pasos a continuación para utilizar las miniaturas en los vídeos:

1. Vaya a un canal de Screens existente o cree un canal.

   >[!NOTE]
   >Para obtener información sobre cómo crear un canal y añadir contenido a un canal, consulte [Creación y administración de un canal en Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en).

1. Seleccione el canal. En la barra de acciones, haga clic en **Editar** para abrir el editor.


   ![Botón Editar de la barra de acciones](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png).

1. Añada o edite un componente de vídeo existente, como se muestra en la figura siguiente.

   ![Imagen resaltada de un recurso de vídeo](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png).

1. Añada o edite un componente de vídeo existente, como se muestra en la figura siguiente.

1. Seleccione el vídeo y haga clic en Configurar (*llave*) icono para abrir las propiedades de vídeo.

   ![Imagen del recurso de vídeo seleccionado con una flecha que señala al icono Configurar, representada como una llave inglesa. en la barra de herramientas](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png).

1. El **Vídeo** se abrirá un cuadro de diálogo en el que podrá ver la **Miniatura** zona de colocación.

   ![Cuadro de diálogo de vídeo que muestra la imagen del recurso de vídeo y el cuadro desplegable Miniatura](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png).

1. Arrastre y suelte una imagen desde el selector de recursos hasta el **Miniatura** zona de colocación y haga clic en **Listo**.

   ![Selector de imagen de recurso que se muestra detrás del cuadro de diálogo Vídeo con el recurso de imagen en el cuadro desplegable Miniatura](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png).

1. Haga clic en **Vista previa**.

1. Si se establece un vídeo en el componente, se reproduce el vídeo. Si no es así, y la miniatura está configurada, la miniatura se reproduce. De lo contrario, el componente se considera no configurado y se omite.

## Casos de uso admitidos al usar la miniatura en vídeos {#understand-use-case}

La miniatura en vídeos admite los siguientes casos de uso:

* Se omite un componente de vídeo sin ninguna configuración.

* Un componente de vídeo solo con el conjunto de miniaturas reproduce la miniatura.

* Un componente de vídeo con el vídeo (si el vídeo tiene la representación correcta) y el conjunto de miniaturas reproduce el vídeo.

* Un componente de vídeo con el conjunto de vídeos reproduce la miniatura, si hay un error de reproducción, o pasa al siguiente elemento en caso de que la miniatura no esté configurada.
