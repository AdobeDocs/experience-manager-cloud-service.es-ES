---
title: Acceder y administrar registros
description: Obtenga información sobre cómo acceder y administrar registros para ayudarle en el proceso de desarrollo en AEM as a Cloud Service.
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 100%

---


# Acceder y administrar registros {#manage-logs}

Obtenga información sobre cómo acceder y administrar registros para ayudarle en el proceso de desarrollo en AEM as a Cloud Service.

Puede acceder a una lista de archivos de registro disponibles para el entorno seleccionado mediante la tarjeta **Entornos** de la página **Información general** o de la página Detalles del entorno.

## Descargar registros {#download-logs}

Siga estos pasos para descargar registros.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Navegue hasta la tarjeta **Entornos** de la página **Información general**.

1. Seleccione **Descargar registros** en el menú de los tres puntos.

   ![Elemento de menú Descargar registros](assets/download-logs1.png)

1. En el cuadro de diálogo **Descargar registros**, seleccione el **Servicio** apropiado del menú desplegable

   ![Cuadro de diálogo Descargar registros](assets/download-preview.png)

1. Una vez seleccionado el servicio, haga clic en el icono de descarga situado junto al registro que desea recuperar.

También puede acceder a sus registros desde la página **Entornos**.

![Registros de la pantalla Entornos](assets/download-logs.png)

## Registros a través de la API {#logs-through-api}

Además de descargar registros a través de la interfaz de usuario, también están disponibles a través de la API y la interfaz de la línea de comandos.

Para descargar los archivos de registro para un entorno específico, el comando sería similar al siguiente.

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

También puede rastrear registros a través de la interfaz de la línea de comandos.

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

Para obtener el Id. de entorno (1884 en este ejemplo) y las opciones de servicio o nombre de registro disponibles, puede utilizar los siguientes comandos.

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

* [ Documentación de la API de Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [CLI de Adobe I/O](https://github.com/adobe/aio-cli-plugin-cloudmanager)
