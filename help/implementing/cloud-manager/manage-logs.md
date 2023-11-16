---
title: Acceder y administrar registros
description: Obtenga información sobre cómo acceder y administrar registros para ayudarle en el proceso de desarrollo en AEM as a Cloud Service.
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: 7272f6ebd1b9c4e67985cba0221d8cafbeb1560a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 79%

---


# Acceder y administrar registros {#manage-logs}

Obtenga información sobre cómo acceder y administrar registros para ayudarle en el proceso de desarrollo en AEM as a Cloud Service.

Puede acceder a una lista de archivos de registro disponibles para el entorno seleccionado mediante la tarjeta **Entornos** de la página **Información general** o de la página Detalles del entorno.

## Descargar registros {#download-logs}

Para descargar registros, haga lo siguiente:

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Navegue hasta la tarjeta **Entornos** de la página **Información general**.

1. Seleccione **Descargar registros** en el menú de los tres puntos.

   ![Elemento de menú Descargar registros](assets/download-logs1.png)

1. En el cuadro de diálogo **Descargar registros**, seleccione el **Servicio** apropiado del menú desplegable

   ![Cuadro de diálogo Descargar registros](assets/download-preview.png)

   En caso de [Regiones de publicación adicionales](/help/operations/additional-publish-regions.md) están habilitados para su entorno, podrá seleccionar cada región y descargar sus registros por separado, como se muestra a continuación:

   ![Descargar registros para regiones de publicación adicionales](assets/download-publish-region-logs.png)

1. Una vez seleccionado el servicio, haga clic en el icono de descarga situado junto al registro que desea recuperar.

También puede acceder a sus registros desde la página **Entornos**.

![Registros de la pantalla Entornos](assets/download-logs.png)



## Registros a través de la API {#logs-through-api}

Además de descargar registros a través de la interfaz de usuario, también están disponibles a través de la API y la interfaz de la línea de comandos.

Para descargar los archivos de registro para un entorno específico, el comando sería similar al siguiente.

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

Además, puede poner en cola los registros a través de la interfaz de línea de comandos.

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

Para obtener el ID de entorno (1884 en este ejemplo) y las opciones de servicio o nombre de registro disponibles, puede utilizar los siguientes comandos.

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

Consulte los siguientes recursos adicionales para obtener más información sobre la API de Cloud Manager y la CLI de Adobe I/O:

* [ Documentación de la API de Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/)
* [CLI de Adobe I/O](https://github.com/adobe/aio-cli-plugin-cloudmanager)

AEM Consulte los siguientes recursos adicionales para obtener más información sobre los archivos de registro en el as a Cloud Service de la:

* [AEM Cloud 5: Archivos de registro de](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/cloud-5/cloud5-aem-log-files.html)
* [AEM Depuración de registros as a Cloud Service con](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=es)
