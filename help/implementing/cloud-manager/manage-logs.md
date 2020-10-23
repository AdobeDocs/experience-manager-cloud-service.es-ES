---
title: '"Administrar registros: Cloud Service"'
description: 'Administrar registros: Cloud Service'
translation-type: tm+mt
source-git-commit: 5a90db8791dd92cceb811b9ed2beda3ecb4a974d
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 22%

---


# Acceder y administrar registros {#manage-logs}

Los usuarios pueden acceder a una lista de los archivos de registro disponibles para el entorno seleccionado mediante la tarjeta de Entorno.  Los usuarios pueden acceder a una lista de archivos de registro para el entorno seleccionado.

Estos archivos se pueden descargar a través de la interfaz de usuario, ya sea desde la página **Información general** .

![](assets/manage-logs1.png)

O bien, la página **Entornos** :

![](assets/download-logs.png)

>[!NOTE]
>Independientemente de dónde se abra, aparece el mismo cuadro de diálogo y permite descargar un archivo de registro individual.

![](assets/manage-logs3.png)


## Registros a través de API {#logs-thorugh-api}

Además de descargar registros a través de la interfaz de usuario, los registros estarán disponibles a través de la API y la interfaz de la línea de comandos.

Por ejemplo, para descargar los archivos de registro de un entorno específico, el comando sería algo más que las líneas de

```java
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

El siguiente comando permite el ajuste de registros:

```java
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

Para obtener el ID de entorno (1884 en este caso) y las opciones de nombre de registro o servicio disponibles, puede utilizar:

```java
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

>[!NOTE]
>Mientras que las **descargas de registro** estarán disponibles a través de la interfaz de usuario y la API, el **Seguimiento de registros** es solo API/CLI.

### Recursos adicionales {#resources}

Consulte los siguientes recursos adicionales para obtener más información sobre la API de Cloud Manager y la CLI de E/S de Adobe:

* [Documentación de la API de Cloud Manager](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [CLI de E/S de Adobe](https://github.com/adobe/aio-cli-plugin-cloudmanager)