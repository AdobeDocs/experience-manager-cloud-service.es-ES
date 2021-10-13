---
title: Introducción a la herramienta de transferencia de contenido
description: Introducción a la herramienta de transferencia de contenido
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: bdcc5cfc229fd5b1fd1f70e37c7231ed3f727e72
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 32%

---

# Introducción a la herramienta de transferencia de contenido {#getting-started-content-transfer-tool}

## Disponibilidad {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Descargar"
>abstract="La herramienta de transferencia de contenido se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM). Asegúrese de descargar la última versión."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="Notas de la versión"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Portal de distribución de software"

La herramienta de transferencia de contenido se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM). Asegúrese de descargar la última versión. Para obtener más información sobre la versión más reciente, consulte [Notas de la versión](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

>[!NOTE]
>Descargue Content Transfer Tool desde el portal de [distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html).

## Ejecución de la herramienta de transferencia de contenido {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Ejecución de la herramienta de transferencia de contenido"
>abstract="Aprenda a utilizar la herramienta de transferencia de contenido para migrar el contenido a AEM as a Cloud Service (autor/publicación)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Consulte Demostración"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Tutorial: uso de la herramienta de transferencia de contenido"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Siga esta sección para aprender a utilizar la herramienta de transferencia de contenido para migrar el contenido a AEM as a Cloud Service (autor/publicación):

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Migración de contenido**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt01.png)

1. Seleccione la opción **Content Transfer** del asistente **Content Migration**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt02.png)


1. La consola siguiente aparece al crear el primer conjunto de migración. Haga clic en **Crear conjunto** de migración para crear un conjunto de migración nuevo.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >Si tiene conjuntos de migración existentes, la consola mostrará la lista de conjuntos de migración existentes con su estado actual.


1. Rellene los campos de la pantalla **Crear conjunto de migración** como se describe a continuación.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt04.png)

   1. **Nombre**: introduzca el nombre del conjunto de migración.
      >[!NOTE]
      >No se permiten caracteres especiales para el nombre del conjunto de migración.

   1. **Configuración de Cloud Service**: introduzca la URL de Autor de destino de AEM as a Cloud Service.

      >[!NOTE]
      >Puede crear y mantener un máximo de diez conjuntos de migración a la vez durante la actividad de transferencia de contenido.
      >Además, debe crear una migración por separado para cada uno de los entornos específicos: *Fase*, *Desarrollo* o *Producción*.

   1. **Token de acceso**: introduzca el token de acceso.

      >[!NOTE]
      >Puede recuperar el token de acceso mediante el botón **Open access token**. Debe asegurarse de pertenecer al grupo de administradores de AEM en la instancia de Cloud Service de destino.

   1. **Parámetros**: seleccione los siguientes parámetros para crear el conjunto de migración:

      1. **Incluir versión**: seleccione la opción que desee. Cuando se incluyen versiones, la ruta `/var/audit` se incluye automáticamente para migrar eventos de auditoría.

      ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt05.png)

      >[!NOTE]
      >Si tiene intención de incluir versiones como parte de un conjunto de migración y realiza complementos con `wipe=false`, debe desactivar la depuración de versiones debido a una limitación actual en la herramienta de transferencia de contenido. Si prefiere mantener habilitada la depuración de versiones y realiza recargas en un conjunto de migración, debe realizar la ingesta como `wipe=true`.

      1. **Incluir asignación de usuarios y grupos de IMS**: Seleccione la opción para incluir la asignación de Usuarios y grupos de IMS.
Consulte [Herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obtener más información.

      1. **Rutas que se incluyen**: utilice el explorador para seleccionar las rutas que deben migrarse. El selector de rutas acepta entradas mediante escritura o selección.

         >[!IMPORTANT]
         >Las siguientes rutas están restringidas al crear un conjunto de migración:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (se permite seleccionar algunas  `/etc` rutas en CTT)




1. Haga clic en **Guardar** después de rellenar todos los campos en la pantalla de detalles **Crear conjunto de migración**.

1. Verá el conjunto de migraciones en el asistente de **Transferencia de contenido**, como se muestra en la figura siguiente.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   Todos los conjuntos de migración existentes se muestran en el asistente de **Transferencia de contenido** con su estado actual y la información de estado. Puede ver algunos de estos iconos que se describen a continuación.

   * La *nube roja* indica que no se puede completar el proceso de extracción.
   * La *nube verde* indica que se puede completar el proceso de extracción.
   * El *icono amarillo* indica que no se creó el conjunto de migración existente y que el específico lo crea otro usuario en la misma instancia.

1. Seleccione un conjunto de migración y haga clic en **Properties** para ver o editar las propiedades del conjunto de migración. Durante la edición de propiedades, no es posible cambiar el **nombre del conjunto de migración** o la **URL del servicio**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ctt06.png)


## Siguientes pasos {#whats-next}

Una vez que haya aprendido a crear un conjunto de migración, ya está listo para obtener información sobre los procesos de extracción e ingesta en la herramienta de transferencia de contenido. Antes de conocer estos procesos, debe revisar [Gestión de repositorios de contenido grande](help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para acelerar de forma significativa las fases de extracción e ingesta de la actividad de transferencia de contenido para mover el contenido a AEM as a Cloud Service.
