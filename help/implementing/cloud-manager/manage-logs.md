---
title: Acceder y administrar registros
description: Obtenga información sobre cómo acceder y administrar registros para ayudarle en el proceso de desarrollo en AEM as a Cloud Service.
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Developer
source-git-commit: 8f1bbbb30dad4c87a0f373117c0ca89afee98235
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 23%

---


# Acceso y administración de registros {#manage-logs}

Obtenga información sobre cómo acceder y administrar registros para apoyar el proceso de desarrollo en AEM as a Cloud Service.

Puede acceder a una lista de archivos de registro disponibles para el entorno seleccionado mediante la tarjeta **Entornos** de la página **Información general** o la página **Detalles del entorno**.

Los registros se conservan durante siete días.

## Descargar registros {#download-logs}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. Navegue hasta la tarjeta **Entornos** de la página **Información general**.

1. Seleccione **Descargar registros** en el menú de los tres puntos.

   ![Elemento de menú Descargar registros](assets/download-logs1.png)

1. En el cuadro de diálogo **Descargar registros**, seleccione el **servicio** apropiado en el menú desplegable.

   ![Cuadro de diálogo Descargar registros](assets/download-preview.png)

   Si hay [regiones de publicación adicionales](/help/operations/additional-publish-regions.md) habilitadas para su entorno, puede seleccionar cada región y descargar sus registros por separado, como se muestra a continuación:

   ![Descargar registros para regiones de publicación adicionales](assets/download-publish-region-logs.png)

1. Una vez seleccionado el servicio, haga clic en el icono de descarga situado junto al registro que desea recuperar.

También puede acceder a sus registros desde la página **Entornos**.

![Registros de la pantalla Entornos](assets/download-logs.png)

## Registros a través de la API {#logs-through-api}

Los registros están disponibles a través de la API y de la interfaz de línea de comandos, además de la interfaz de usuario.

Para descargar los archivos de registro para un entorno específico, utilice un comando similar al siguiente:

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

También puede acceder a los registros inmediatamente mediante la interfaz de línea de comandos.

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

Para obtener el ID de entorno (1884 en este ejemplo) y las opciones de servicio o nombre de registro disponibles, puede utilizar los siguientes comandos:

```shell
$ aio cloudmanager:list-environments
Environment Id Name                     Type  Description                          
1884           FoundationInternal_dev   dev   Foundation Internal Dev environment  
1884           FoundationInternal_stage stage Foundation Internal STAGE environment
1884           FoundationInternal_prod  prod  Foundation Internal Prod environment
 
 
$ aio cloudmanager:list-available-log-options 1884
Environment Id Service    Name         
1884           author     aemerror     
1884           author     aemrequest   
1884           author     aemaccess    
1884           publish    aemerror     
1884           publish    aemrequest   
1884           publish    aemaccess    
1884           dispatcher httpderror   
1884           dispatcher aemdispatcher
1884           dispatcher httpdaccess
```

### Recursos adicionales {#resources}

>[!TIP]
>
>Para obtener más información acerca de la depuración de AEM as a Cloud Service, vea [este recurso de vídeo](https://app.frame.io/reviews/28cdf463-b7fc-443b-a54a-93cb7da6567e/dbf158f1-568b-4efc-8fbc-3b241561cbab).

Para obtener más información sobre la API de Cloud Manager y la CLI de Adobe I/O, consulte los siguientes recursos adicionales:

* [Documentación de API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/)
* [CLI de Adobe I/O](https://github.com/adobe/aio-cli-plugin-cloudmanager)

Para obtener más información sobre los archivos de registro en AEM as a Cloud Service, consulte los siguientes recursos adicionales:

* [Archivos de registro de AEM de Cloud 5](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/expert-resources/cloud-5/cloud5-aem-log-files#)
* [Depuración de AEM as a Cloud Service mediante registros](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs#)
