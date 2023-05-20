---
title: Introducción a la herramienta de transferencia de contenido (heredada)
description: Introducción a la herramienta de transferencia de contenido
hide: true
hidefromtoc: true
exl-id: a6ee6996-510e-42d7-9a7c-f64732764f97
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 24%

---

# Introducción a la herramienta de transferencia de contenido (heredada) {#getting-started-content-transfer-tool}


## Disponibilidad {#availability}

La herramienta de transferencia de contenido se puede descargar como un archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) en la instancia de origen de Adobe Experience Manager AEM (). Asegúrese de descargar la última versión. Para obtener más información sobre la versión más reciente, consulte [Notas de versión](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

>[!NOTE]
>Descargue Content Transfer Tool desde el portal de [distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html).

## Conectividad del entorno de origen {#source-environment-connectivity}

AEM La instancia de origen puede estar ejecutándose detrás de un cortafuegos donde solo puede llegar a ciertos hosts que se han añadido a una Lista de permitidos. AEM Para ejecutar correctamente una extracción, será necesario poder acceder a los siguientes extremos desde la instancia que se está ejecutando:

* AEM El entorno as a Cloud Service de destino: `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* El servicio Azure Blob Storage: `*.blob.core.windows.net`
* Extremo de E/S de asignación de usuarios: `usermanagement.adobe.io`

AEM Para probar la conectividad con el entorno as a Cloud Service de destino, emita el siguiente comando cURL desde el shell de la instancia de origen (reemplazar `program_id`, `environment_id`, y `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>Si un `HTTP/2 200` AEM se ha recibido, la conexión con el as a Cloud Service se ha realizado correctamente.

## Ejecución de la herramienta de transferencia de contenido {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


Siga esta sección para aprender a utilizar la herramienta de transferencia de contenido para migrar el contenido a AEM as a Cloud Service (autor/publicación):

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Migración de contenido**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ctt01.png)

1. Seleccione el **Transferencia de contenido** opción de **Migración de contenido** asistente.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ctt02.png)


1. La consola siguiente aparece cuando crea el primer conjunto de migración. Haga clic en **Crear conjunto** de migración para crear un conjunto de migración nuevo.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >Si tiene conjuntos de migración existentes, la consola mostrará la lista de conjuntos de migración existentes con su estado actual.


1. Rellene los campos en **Crear conjunto de migración** como se describe a continuación.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt04.png)

   1. **Nombre**: introduzca el nombre del conjunto de migración.
      >[!NOTE]
      >No se permiten caracteres especiales para el nombre del conjunto de migración.

   1. **Configuración de Cloud Service**: introduzca la URL de Autor de destino de AEM as a Cloud Service.

      >[!NOTE]
      >Puede crear y mantener un máximo de diez conjuntos de migración a la vez durante la actividad de transferencia de contenido.
      >Además, debe crear una migración por separado para cada uno de los entornos específicos: *Fase*, *Desarrollo* o *Producción*.

   1. **Token de acceso**: introduzca el token de acceso.

      >[!NOTE]
      >Puede recuperar el token de acceso utilizando la variable **Abrir token de acceso** botón. Debe asegurarse de que pertenece al grupo &quot;Administradores&quot; en la instancia de Cloud Service de destino.

   1. **Parámetros**: seleccione los siguientes parámetros para crear el conjunto de migración:

      1. **Incluir versión**: seleccione la opción que desee. Cuando se incluyen versiones, la ruta `/var/audit` para migrar eventos de auditoría.

         ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

         >[!NOTE]
         >Si tiene intención de incluir versiones como parte de un conjunto de migración y realiza recargas con `wipe=false`, debe deshabilitar la depuración de versiones debido a una limitación actual en la herramienta de transferencia de contenido. Si prefiere mantener habilitada la depuración de versiones y realiza recargas en un conjunto de migración, debe realizar la ingesta como `wipe=true`.


      1. **Rutas que se incluyen**: utilice el explorador para seleccionar las rutas que deben migrarse. El selector de rutas acepta entradas escribiendo o seleccionando.

         >[!IMPORTANT]
         >Las siguientes rutas están restringidas al crear un conjunto de migración:
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (algunos `/etc` se permite seleccionar las rutas en CTT)


1. Haga clic en **Guardar** después de rellenar todos los campos en la variable **Crear conjunto de migración** pantalla de detalles.

1. Verá su conjunto de migración en la **Transferencia de contenido** asistente, como se muestra en la figura siguiente.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   Todos los conjuntos de migración existentes se muestran en la **Transferencia de contenido** asistente con su estado actual y la información de estado. Puede ver algunos de estos iconos que se describen a continuación.

   * La *nube roja* indica que no se puede completar el proceso de extracción.
   * A *nube verde* indica que se puede completar el proceso de extracción.
   * El *icono amarillo* indica que no se creó el conjunto de migración existente y que el específico lo crea otro usuario en la misma instancia.

1. Seleccione un conjunto de migración y haga clic en **Propiedades** para ver o editar las propiedades del conjunto de migración. Al editar las propiedades, no es posible cambiar la variable **Nombre del conjunto de migración** o el **URL de servicio**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png)

### Determinar el tamaño del conjunto de migración y el espacio en disco {#migration-set-size}

Después de crear un conjunto de migración, es muy recomendable ejecutar una comprobación de tamaño en el conjunto antes de iniciar un proceso de extracción.
Al realizar una comprobación de tamaño en el conjunto de migración, podrá:
* Determine si hay suficiente espacio en disco en la `crx-quickstart` subdirectorio para completar la extracción correctamente.
* Determine si el tamaño del conjunto de migración se encuentra dentro de los límites del producto admitido y evite las ingestas de contenido fallidas.

Siga los pasos a continuación para ejecutar una comprobación de tamaño:

1. Seleccione un conjunto de migración y haga clic en **Comprobar tamaño**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image1.png)

1. Esto abrirá el **Comprobar tamaño** diálogo.

   ![imagen](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image2.png)

1. Haga clic en **Comprobar tamaño** para iniciar el proceso. A continuación, volverá a la vista de lista del conjunto de migración y debería ver un mensaje que indique que **Comprobar tamaño** se está ejecutando.

   ![imagen](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image3.png)


1. Una **Comprobar tamaño** el proceso se ha completado, el estado cambiará a **FINALIZADO**. Seleccione el mismo conjunto de migración y haga clic en **Comprobar tamaño** para ver los resultados.

   ![imagen](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image4.png)

   A continuación se muestra un ejemplo de **Comprobar tamaño** resultados sin advertencias.

   ![imagen](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image5.png)

1. Si la variable **Comprobar tamaño** los resultados indican que no hay suficiente espacio en disco o que el conjunto de migración supera los límites del producto, **ADVERTENCIA** se mostrará el estado.

![imagen](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)

A continuación se muestra un ejemplo de **Comprobar tamaño** resultados con advertencias.

![imagen](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png)


## Siguientes pasos {#whats-next}

Una vez que haya aprendido a crear un conjunto de migración, ya puede obtener información sobre los procesos de extracción e ingesta en la herramienta de transferencia de contenido. Antes de aprender estos procesos, debe revisar [Gestión de repositorios de contenido grandes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) AEM para acelerar de forma significativa las fases de extracción e ingesta de la actividad de transferencia de contenido y mover el contenido a la ubicación as a Cloud Service de la.
